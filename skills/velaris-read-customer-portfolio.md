---
name: Read and search the customer portfolio (V2)
description: Pull organizations, accounts, and contacts from the Velaris AI Customer Success Platform using the preferred V2 read/search surface.
api: openapi/velaris-openapi.yml
generated: '2026-07-21'
method: generated
operations: [getAllOrganizations, searchOrganization, getAllAccounts, searchAccounts, getAllContacts, searchContacts]
---

# Read and search the customer portfolio (V2)

Use the V2 endpoints for all reads. The provider's own docs say V1 (`/core/*`) list endpoints are restricted to a limited number of records; V2 has no such limit.

## Auth
Send `Authorization: Bearer {access_token}` — a user-scoped token created in-app under Profile > Security > Access token (see `authentication/velaris-authentication.yml`). Base URL: `https://api.euw1.velaris.io`.

## Steps
1. **List organizations** — `getAllOrganizations` (`GET /v2/organizations`). For filtered pulls use `searchOrganization` (`POST /v2/organizations/search`).
2. **List accounts** — `getAllAccounts` (`GET /v2/accounts`) or `searchAccounts` (`POST /v2/accounts/search`). Accounts sit under a parent organization (see `data-model/velaris-data-model.yml`).
3. **List contacts** — `getAllContacts` (`GET /v2/contacts`) or `searchContacts` (`POST /v2/contacts/search`). To resolve specific people, `getContactsByEmails` (`POST /v2/contacts/batch/read`) accepts a batch of email addresses.

## Rules
- Prefer V2 search over V1 custom-field query params.
- No idempotency keys exist — treat POST searches as safe/read-only, but never retry entity writes blindly (`conventions/velaris-conventions.yml`).
- Unauthenticated or bad-token calls return `401` from the gateway (`errors/velaris-problem-types.yml`).
