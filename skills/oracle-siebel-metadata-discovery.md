---
name: oracle-siebel-metadata-discovery
description: >-
  Discover what a specific Siebel deployment actually exposes — Business
  Objects, Business Components, fields, business services and repository objects
  — using the describe endpoints, before calling anything else. Run this FIRST
  against any Siebel instance you have not seen.
generated: '2026-08-13'
method: generated
source: >-
  openapi/oracle-siebel-metadata-api-openapi.yml,
  openapi/oracle-siebel-business-services-api-openapi.yml,
  openapi/oracle-siebel-repository-api-openapi.yml,
  conventions/oracle-siebel-conventions.yml
api: Oracle Siebel REST API
base: 'https://{siebel-server}/siebel/v1.0'
operations:
  - describeBusinessComponent
  - describeBusinessServices
  - describeBusinessService
  - describeWorkspace
  - getRepositoryObject
  - invokeBusinessService
---

# Discover what this Siebel instance exposes

## Why this skill runs first

Every Siebel deployment is configured differently. Custom Business Components, custom fields, and customer-specific Lists of Values mean **no published document describes any particular Siebel instance**. Oracle does not ship a canonical Siebel OpenAPI, and that is a consequence of the deployment model rather than a gap.

What Siebel does give you is better than a file: a running instance describes itself, and can emit that description as an OpenAPI 2.0 or 3.0 document. Treat the describe output as the contract, and treat the specs in `openapi/` as a map of the base product only.

## 1. Enumerate the data surface

`GET /data/describe`

Returns every Business Object exposed as a Base Integration Object. This is the list of `{BusinessObject}` path segments that will work on this instance.

## 2. Describe one Business Component

`describeBusinessComponent` — `GET /data/{BusinessObject}/{BusinessComponent}/describe`

```
GET /data/Account/Account/describe
```

This is the highest-value call in the whole API. It returns the attributes, actions and links of the resource — which is how you find:

- the **real field list**, including this customer's custom fields, which will not be in any spec;
- which fields are required and writable;
- the valid values behind picklist fields such as `Account Type`, `Industry`, `Sales Stage`, `Status`, `Priority` and `Severity`.

Never hard-code a picklist value. Read it from here, or you will collect HTTP 400s that look like malformed JSON but are actually rejected List of Values entries.

## 3. Enumerate business services

`describeBusinessServices` — `GET /service/describe`

Returns every Siebel business service name with links to each.

`describeBusinessService` — `GET /service/{ServiceName}/describe`

Returns the methods defined on one service and their arguments.

## 4. Invoke a business service — carefully

`invokeBusinessService` — `POST /service/{ServiceName}/{MethodName}`

This is the most powerful operation Siebel exposes over REST. It runs server-side business logic, including integration-object operations and anything the customer has written in eScript. It is not CRUD and it is not bounded by the resource model.

Treat it as privileged:

- Call `describeBusinessService` first and use only documented methods with documented arguments.
- Do not call a service you cannot name a business reason for.
- It has no idempotency guarantee whatsoever — an invocation may write, send, or trigger a workflow. Never blind-retry one.

Oracle's own MCP framework, Siebel AI Connectors, exists precisely to constrain this: it exposes a *selected* set of operations as tools rather than handing an agent the whole surface. Follow the same principle here.

## 5. Inspect repository (design-time) objects

`describeWorkspace` — `GET /workspace/{WorkspaceName}/describe`

```
GET /workspace/MAIN/describe
```

Lists repository types and links to their children.

`getRepositoryObject` — `GET /workspace/{WorkspaceName}/{RepositoryObject}/{ObjectName}`

Returns a single applet, view, business component definition or other repository object. This is configuration metadata, not customer data — useful for understanding a deployment, not for answering business questions.

## 6. Turn it into a spec

Siebel can return the describe output as an OpenAPI document. Persist that per deployment and diff it after each monthly Siebel update — there is no API changelog, so a describe-to-describe diff is the only reliable way to detect that the surface moved. See `changelog/oracle-siebel-changelog.yml`.

## Reminders

- `Content-Type: application/json` on every call, including these GETs.
- 401 means the auth scheme does not match the server's configured `Authentication type`.
- 404 on a describe path usually means the Business Object or Business Component name is wrong, not that describe is unsupported. Go back to `/data/describe`.
