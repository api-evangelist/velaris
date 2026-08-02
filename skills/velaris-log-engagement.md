---
name: Log customer engagement (activities and notes)
description: Record meetings, calls, and notes against Velaris customer entities so health scoring and CSM timelines stay current.
api: openapi/velaris-openapi.yml
generated: '2026-07-21'
method: generated
operations: [getActivityTypes, createActivity, updateActivity, createNote]
---

# Log customer engagement (activities and notes)

## Auth
`Authorization: Bearer {access_token}` against `https://api.euw1.velaris.io` (see `authentication/velaris-authentication.yml`).

## Steps
1. **Discover activity types** — `getActivityTypes` (`GET /activity-type`) and use a real type id when creating activities.
2. **Create the activity** — `createActivity` (`POST /entity-action/activity`) attached to the target organization/account. Activities carry source/external ids: they can later be fetched by source id (`getActivityBySourceId`) or external id (`getActivityByExternalId`).
3. **Amend if needed** — `updateActivity` (`PUT /entity-action/activity`).
4. **Attach a note** — `createNote` (`POST /notes`). Notes also support external-id lookups and updates (`getNoteByExternalId`, `updateNoteWithExternalId`).

## Rules
- Use your system's stable identifier as the external id so re-syncs update instead of duplicating — there is no idempotency-key header (`conventions/velaris-conventions.yml`).
- Only Custom Objects operations document 404/406 responses; expect `401` for auth failures elsewhere (`errors/velaris-problem-types.yml`).
