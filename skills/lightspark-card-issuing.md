---
name: lightspark-card-issuing
description: Issue, fund, reveal and manage payment cards on Lightspark Grid, and simulate the full authorization / clearing / return lifecycle in sandbox.
api: openapi/lightspark-grid-openapi-original.yml
base_url: https://api.lightspark.com/grid/2025-10-13
operations:
  - createCard
  - listCards
  - getCardById
  - updateCardById
  - revealCard
  - sandboxSimulateCardAuthorization
  - sandboxSimulateCardClearing
  - sandboxSimulateCardReturn
generated: '2026-07-19'
method: generated
source: openapi/lightspark-grid-openapi-original.yml
---

# Card issuing on Grid

Cards sit on top of a verified customer and a funded internal account. Verification must be approved
first — an unverified customer fails with `403 USER_NOT_READY`.

## Steps

1. **Issue.** `createCard` (`POST /cards`) against the cardholder customer and a funding source.
2. **Inspect.** `listCards` (`GET /cards`) with `cursor`/`limit`; `getCardById` (`GET /cards/{id}`).
3. **Manage state.** `updateCardById` (`PATCH /cards/{id}`) — freeze, unfreeze, close, or change the
   funding source.
4. **Reveal PAN.** `revealCard` (`POST /cards/{id}/reveal`) returns sensitive card data. Treat the
   response as PCI-scope: never log it, never persist it, render it client-side only and let it
   expire.

## Events

Three of the twelve Grid webhooks are card events — `card-state-change`,
`card-funding-source-change` and `card-transaction`. The `card-transaction` event is how you learn
about authorizations, clearings and returns; the API is not a polling surface for spend. Verify
`X-Grid-Signature` first — see `skills/lightspark-webhook-verification.md`.

## Sandbox

As of the July 2026 changelog, the full card lifecycle can be exercised in sandbox without touching
production. Drive it with the three simulation operations:

- `sandboxSimulateCardAuthorization` (`POST /sandbox/cards/{id}/simulate/authorization`)
- `sandboxSimulateCardClearing` (`POST /sandbox/cards/{id}/simulate/clearing`)
- `sandboxSimulateCardReturn` (`POST /sandbox/cards/{id}/simulate/return`)

Fund the backing internal account first with `sandboxFundInternalAccount`
(`POST /sandbox/internal-accounts/{accountId}/fund`).

## Rules

- Send an `Idempotency-Key` on `createCard` — a retried issue without one can mint a second card.
- Errors use the `{status, code, message, details}` envelope; branch on `code`.
- Card state changes are asynchronous — the webhook, not the PATCH response, is the terminal signal.
