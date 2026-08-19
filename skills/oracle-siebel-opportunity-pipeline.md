---
name: oracle-siebel-opportunity-pipeline
description: >-
  Read and advance the Siebel sales pipeline — list an account's opportunities,
  create a new one, and move it through sales stages — over the Siebel REST API.
generated: '2026-08-13'
method: generated
source: >-
  openapi/oracle-siebel-opportunities-api-openapi.yml,
  openapi/oracle-siebel-accounts-api-openapi.yml,
  conventions/oracle-siebel-conventions.yml,
  data-model/oracle-siebel-data-model.yml
api: Oracle Siebel REST API
base: 'https://{siebel-server}/siebel/v1.0'
operations:
  - listOpportunities
  - listAccountOpportunities
  - createOpportunity
  - getOpportunity
  - upsertOpportunity
  - deleteOpportunity
  - listAccounts
---

# Work the Siebel opportunity pipeline

## Before you start

Read the shared rules in `oracle-siebel-account-onboarding.md` first: templated base URL, server-decided auth scheme, `Content-Type` drives the response format, `PageSize` max 100, HTTP 204 means empty, and there is no idempotency key.

One extra rule matters here: **what you can see depends on who you are.** Siebel authorises by responsibilities, position and organization, refined per call by `ViewMode`. A pipeline query run as one user legitimately returns a different set than the same query run as another. Never report a Siebel result as "the pipeline" without saying whose visibility produced it.

## 1. Scope the pipeline

Whole-instance view (subject to your visibility):

`listOpportunities` — `GET /data/Opportunity/Opportunity`

```
GET /data/Opportunity/Opportunity?searchspec=([Sales Stage]<>'Closed/Lost' AND [Sales Stage]<>'Closed/Won')&PageSize=100&ViewMode=All
```

Per account — the more useful shape, because Account is the hub of the Siebel data model:

`listAccountOpportunities` — `GET /data/Account/Account/{AccountId}/Opportunity`

Get the `{AccountId}` from `listAccounts` with a `searchspec` on `[Name]`.

Page by incrementing `StartRowNum`; stop on 204. There is no total, so never report a count from a single page.

## 2. Create an opportunity

`createOpportunity` — `POST /data/Opportunity/Opportunity`

Only `Name` is required, but an opportunity with no account is orphaned in the graph — always set `Account`.

```json
{
  "Name": "Acme Manufacturing — Field Service Expansion",
  "Account": "Acme Manufacturing",
  "Sales Stage": "01 - Qualification",
  "Close Date": "12/31/2026",
  "Revenue": 250000,
  "Win Probability": 20,
  "Description": "Expansion of field service licences across two plants."
}
```

Guard this with a `listOpportunities` search on `[Name]` and `[Account]` first. POST is not idempotent and a timed-out create that actually succeeded will otherwise become two deals in the forecast.

`Sales Stage` values are deployment-configured Lists of Values. Do not invent them — read the valid set from `describeBusinessComponent` (see `oracle-siebel-metadata-discovery.md`).

## 3. Advance the stage

`upsertOpportunity` — `PUT /data/Opportunity/Opportunity/{OpportunityId}`

```json
{
  "Sales Stage": "04 - Negotiation",
  "Win Probability": 70,
  "Revenue": 265000
}
```

PUT is an upsert and is safe to repeat, so this is the operation to retry on a timeout — unlike the create in step 2.

## 4. Read one back

`getOpportunity` — `GET /data/Opportunity/Opportunity/{OpportunityId}`

The response carries `Account Id`, which resolves back to the account with `getAccount`. Note the asymmetry: an Opportunity resolves to its Account, but a Service Request or Activity carries only the contact's NAME, with no `Contact Id` — those references cannot be resolved programmatically.

## 5. Remove

`deleteOpportunity` — `DELETE /data/Opportunity/Opportunity/{OpportunityId}`

Destructive and not soft. Confirm with `getOpportunity` before calling, and prefer setting `Sales Stage` to a closed-lost value over deleting — the record usually needs to stay for reporting.

## Reporting honestly

- Revenue arrives as a number without a currency field on Opportunity. Currency is on Order (`Currency Code`), not here. Do not assume USD.
- `Close Date` is formatted per the Siebel deployment's locale settings, commonly `MM/DD/YYYY`, not ISO 8601. Parse defensively.
- A single page is at most 100 records. Aggregate across pages before reporting any total.
