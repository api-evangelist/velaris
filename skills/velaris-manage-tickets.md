---
name: Create and work customer tickets
description: Open Velaris support tickets, track them, and collaborate through threaded comments.
api: openapi/velaris-openapi.yml
generated: '2026-07-21'
method: generated
operations: [getAllTickets, createTicket, getTicketById, updateTicket, createComment]
---

# Create and work customer tickets

## Auth
`Authorization: Bearer {access_token}` against `https://api.euw1.velaris.io` (see `authentication/velaris-authentication.yml`).

## Steps
1. **Check the queue** — `getAllTickets` (`GET /ticketing/tickets`).
2. **Open a ticket** — `createTicket` (`POST /ticketing/tickets`).
3. **Track it** — `getTicketById` (`GET /ticketing/tickets/:ticketId`); update status/fields with `updateTicket` (`PUT /ticketing/tickets/:ticketId`).
4. **Comment** — `createComment` (`POST /ticketing/tickets/:ticketId/comments`); the thread is readable via `getAllComments` and individual comments via `getCommentById` or `getCommentByExternalId`.
5. **Recover** — deleted tickets can be restored with `restoreTicket` (`PUT /ticketing/tickets/:ticketId/restore`).

## Rules
- Use external ids on comments when mirroring another helpdesk so re-syncs are update-in-place — there is no idempotency-key header (`conventions/velaris-conventions.yml`).
- Expect `401` on auth failure; only Custom Objects ops document richer error codes (`errors/velaris-problem-types.yml`).
