---
name: Track and manage customer risks
description: Surface, create, and resolve churn-risk records on Velaris accounts and organizations.
api: openapi/velaris-openapi.yml
generated: '2026-07-21'
method: generated
operations: [getAllRisks, searchRisks, createRisk, updateRisk, archiveRisk]
---

# Track and manage customer risks

## Auth
`Authorization: Bearer {access_token}` against `https://api.euw1.velaris.io` (see `authentication/velaris-authentication.yml`).

## Steps
1. **Review open risks** — `getAllRisks` (`GET /v2/risks`) for the portfolio, or `searchRisks` (`POST /v2/risks/search`) to filter (V2 is the preferred read surface).
2. **Raise a risk** — `createRisk` (`POST /core/risks`) against the at-risk entity.
3. **Update as it evolves** — `updateRisk` (`PUT /core/risks/:riskId`).
4. **Close it out** — `archiveRisk` (`PUT /core/risks/:riskId/archive`); a mistaken archive is reversible with `restoreRisks` (`PUT /core/risks/:riskId/restore`).

## Rules
- Reads on V2, writes on the V1 `/core/risks` surface — that is the shape the provider publishes.
- No idempotency keys: check for an existing risk (search) before creating to avoid duplicates (`conventions/velaris-conventions.yml`).
