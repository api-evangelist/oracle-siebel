---
name: oracle-siebel-account-onboarding
description: >-
  Create a Siebel Account and attach its contacts, then verify the result —
  safely, on an API that has no idempotency key. Use when onboarding a new
  customer organisation into Siebel CRM over the REST API.
generated: '2026-08-13'
method: generated
source: >-
  openapi/oracle-siebel-accounts-api-openapi.yml,
  openapi/oracle-siebel-contacts-api-openapi.yml,
  conventions/oracle-siebel-conventions.yml,
  errors/oracle-siebel-problem-types.yml
api: Oracle Siebel REST API
base: 'https://{siebel-server}/siebel/v1.0'
operations:
  - listAccounts
  - createAccount
  - getAccount
  - upsertAccount
  - listAccountContacts
  - upsertAccountContact
  - createContact
---

# Onboard an account into Siebel

## Before you start

- The base URL is your own Siebel Application Interface host. There is no shared Oracle endpoint.
- Send `Authorization: Basic <base64>` if the server's `Authentication type` is `Basic` or `SSO`; send `Authorization: Bearer <token>` if it is `OAuth`. You cannot choose — it is a server-wide setting.
- Send `Content-Type: application/json` on every call, including GET. Siebel selects the response format from `Content-Type`, not `Accept`.
- **There is no `Idempotency-Key`.** A retried `createAccount` creates a second account. Every create in this skill is preceded by a search.

## 1. Check whether the account already exists

`listAccounts` — `GET /data/Account/Account`

Search on the natural key Siebel actually uses, which is Name plus Location:

```
GET /data/Account/Account?searchspec=([Name]='Acme Manufacturing' AND [Location]='Chicago')&PageSize=10
```

- HTTP 200 with records: the account exists. Take `Id` and skip to step 3.
- HTTP 204: no match. Proceed to step 2. **204 is not an error** — it is Siebel's empty result.
- HTTP 401: the Authorization header is wrong for the configured auth type, or the bearer token failed introspection at the external OAuth provider.

## 2. Create the account

`createAccount` — `POST /data/Account/Account`

Only `Name` is required. Field names are Siebel field names, with spaces:

```json
{
  "Name": "Acme Manufacturing",
  "Location": "Chicago",
  "Account Type": "Customer",
  "Industry": "Industrial Manufacturing",
  "Main Phone Number": "+1 312 555 0100",
  "Home Page": "https://example.com"
}
```

- HTTP 201: created. Read `Id` from the response body.
- HTTP 400: a field name or picklist value is wrong. Siebel validates `Account Type` and `Industry` against Lists of Values configured in that deployment — the valid set is deployment-specific, so read it from `describeBusinessComponent` rather than assuming.
- **If the call times out, do not blind-retry.** Re-run the step 1 search first. Without an idempotency key that search is the only thing standing between you and a duplicate account.

## 3. List the contacts already on the account

`listAccountContacts` — `GET /data/Account/Account/{AccountId}/Contact`

```
GET /data/Account/Account/1-ABC123/Contact?PageSize=100
```

`PageSize` maxes out at 100 and defaults to 10. There is no total count and no next link, so page by incrementing `StartRowNum` by `PageSize` until you get a 204.

## 4. Attach a contact

`upsertAccountContact` — `PUT /data/Account/Account/{AccountId}/Contact`

PUT in Siebel is an **upsert**, which makes it the safe verb: re-running it does not duplicate. Prefer it over `createContact` whenever you have the account id.

```json
{
  "First Name": "Dana",
  "Last Name": "Reyes",
  "Job Title": "Head of Procurement",
  "Email Address": "dana.reyes@example.com",
  "Work Phone #": "+1 312 555 0142"
}
```

`First Name` and `Last Name` are both required. HTTP 200 means updated, 201 means created.

Use `createContact` (`POST /data/Contact/Contact`) only for a contact with no account — and guard it with a `listContacts` search first, for the same reason as step 2.

## 5. Verify

`getAccount` — `GET /data/Account/Account/{AccountId}`

Re-read the account and re-run step 3. If you created something twice, this is where you will see it; delete the surplus with `deleteAccount` / `deleteContact`.

## Corrections

`upsertAccount` — `PUT /data/Account/Account/{AccountId}` — updates in place and is safe to repeat.

## Failure modes worth knowing

| Status | What it usually means here |
|---|---|
| 204 | Empty result set. Not a failure. |
| 401 | Wrong scheme for the configured auth type, or token introspection failed. |
| 404 | Bad record id **or** a misspelled Business Object / Business Component in the path. |
| 415 | You sent something other than `application/json` or `application/xml`. |
| 500 | Object Manager error, often carrying the real message in the body. Back off exponentially — there is no `Retry-After`. |

There is no 429 and no rate-limit header. If the deployment saturates you will see 500s and timeouts, so keep concurrency low and honour the 100-record ceiling.
