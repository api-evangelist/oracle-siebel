---
name: oracle-siebel-service-request-handling
description: >-
  Open, triage, update and close Siebel service requests, and log the activities
  against them, over the Siebel REST API.
generated: '2026-08-13'
method: generated
source: >-
  openapi/oracle-siebel-service-requests-api-openapi.yml,
  openapi/oracle-siebel-activities-api-openapi.yml,
  conventions/oracle-siebel-conventions.yml,
  errors/oracle-siebel-problem-types.yml
api: Oracle Siebel REST API
base: 'https://{siebel-server}/siebel/v1.0'
operations:
  - listServiceRequests
  - createServiceRequest
  - getServiceRequest
  - upsertServiceRequest
  - deleteServiceRequest
  - listActivities
  - createActivity
  - getActivity
  - upsertActivity
---

# Handle a Siebel service request

## Before you start

Shared rules are in `oracle-siebel-account-onboarding.md`. The one that bites hardest in case management: **there is no idempotency key**, and a duplicated service request is visible to the customer.

Note the path. The Business Object and Business Component names contain a space and must be URL-encoded:

```
/data/Service%20Request/Service%20Request
```

## 1. Look before you open

`listServiceRequests` — `GET /data/Service Request/Service Request`

Search for an existing open case on the same account before creating a new one:

```
GET /data/Service%20Request/Service%20Request?searchspec=([Account]='Acme Manufacturing' AND [Status]<>'Closed')&PageSize=100
```

204 means nothing open. 200 means triage the existing case instead of opening a second one.

## 2. Open the request

`createServiceRequest` — `POST /data/Service Request/Service Request`

`Abstract` is the only required field. Fill severity and priority anyway — they drive Siebel's own assignment and escalation rules.

```json
{
  "Abstract": "Field service portal returns 500 on work order submit",
  "Description": "Reproducible on submit for any work order with more than 20 line items.",
  "Status": "Open",
  "Priority": "2-High",
  "Severity": "2-High",
  "Type": "Error/Bug",
  "Account": "Acme Manufacturing"
}
```

- HTTP 201: created. The response carries `Id` and `SR Number`. **`SR Number` is the human-facing identifier** — quote that to a customer, not the opaque `Id`.
- HTTP 400: a picklist value is not configured in this deployment. `Status`, `Priority`, `Severity`, `Type` and `Sub-Type` are all Lists of Values and all deployment-specific.
- On a timeout, re-run step 1 before retrying.

## 3. Log activities against the case

`createActivity` — `POST /data/Activity/Activity`

`Type` and `Description` are required.

```json
{
  "Type": "Call - Outbound",
  "Description": "Called Dana Reyes to confirm reproduction steps.",
  "Status": "Done",
  "Priority": "2-High",
  "Account": "Acme Manufacturing"
}
```

Be aware of a real modelling gap: Activity carries `Account Id`, but it links to a contact only through the denormalised `Contact First Name` / `Contact Last Name` pair — there is **no `Contact Id`**. The same is true of Service Request. Do not build anything that assumes those names resolve to a contact record.

List what has already been done with `listActivities`, and correct an entry with `upsertActivity` (`PUT /data/Activity/Activity/{ActivityId}`), which is safe to repeat.

## 4. Update the case

`upsertServiceRequest` — `PUT /data/Service Request/Service Request/{ServiceRequestId}`

```json
{
  "Status": "Pending",
  "Sub-Status": "Awaiting Customer",
  "Priority": "3-Medium"
}
```

Upsert, so this is the retry-safe operation. Use it for every state transition including closure:

```json
{ "Status": "Closed", "Sub-Status": "Resolved" }
```

## 5. Read back

`getServiceRequest` — `GET /data/Service Request/Service Request/{ServiceRequestId}`

Confirm `Status` and `Sub-Status` landed. `Created` is set by Siebel and is not writable.

## Do not delete

`deleteServiceRequest` exists (`DELETE /data/Service Request/Service Request/{ServiceRequestId}`) but closing a case is almost always correct and deleting one almost never is: the record is service history and usually feeds SLA reporting. Only delete a case you created in error, in the same session, before anyone has seen it.

## Errors

Same table as the other Siebel skills. Two specific to this flow:

- **404 on a path that looks right** — check the URL encoding of `Service Request`. An un-encoded space produces a 404 that reads like a missing record.
- **500 with text in the body** — Siebel Object Manager errors surface here, often about a workflow or assignment-manager rule firing on the record. Capture the body; there is no error code to branch on.
