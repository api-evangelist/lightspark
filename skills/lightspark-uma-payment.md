---
name: lightspark-uma-payment
description: Send and receive payments to a Universal Money Address ($user@domain) through the Lightspark Grid API — resolve the address, quote the corridor, execute, and handle incoming UMA payments.
api: openapi/lightspark-grid-openapi-original.yml
base_url: https://api.lightspark.com/grid/2025-10-13
operations:
  - lookupUma
  - getAvailableUmaProviders
  - getExchangeRates
  - createQuote
  - executeQuote
  - getTransactionById
  - sandboxReceive
generated: '2026-07-19'
method: generated
source: openapi/lightspark-grid-openapi-original.yml
---

# UMA payments with Grid

A Universal Money Address looks like `$alice@example.com`. Grid resolves it, negotiates the UMA
protocol version with the counterparty VASP, quotes the corridor, and settles.

## Steps

1. **Resolve the address.** `lookupUma` (`GET /receiver/uma/{receiverUmaAddress}`). This performs
   the LNURLP lookup, fetches and validates the counterparty's certificate chain and public key, and
   returns the currencies the receiver accepts and any mandatory payee data the counterparty requires.
2. **Optionally check coverage first.** `getAvailableUmaProviders` (`GET /uma-providers`) lists the
   VASPs reachable from your platform; `getExchangeRates` (`GET /exchange-rates`) gives indicative
   FX before you commit to a quote.
3. **Quote.** `createQuote` (`POST /quotes`) with the receiver UMA address and the sending amount
   and currency. The quote carries the locked rate, the fees, and an expiry.
4. **Execute.** `executeQuote` (`POST /quotes/{quoteId}/execute`) with an `Idempotency-Key`. If the
   source is an embedded wallet, this call additionally requires a `Grid-Wallet-Signature` header
   over the returned `payloadToSign`, plus the matching `Request-Id`.
5. **Confirm.** `getTransactionById` (`GET /transactions/{transactionId}`). Prefer the
   `outgoing-payment` webhook for terminal status.

## Receiving

Incoming UMA payments arrive as the `incoming-payment` webhook, which doubles as an approval
mechanism — your platform can approve or reject before Grid credits the account. Verify the
`X-Grid-Signature` header (P-256 over SHA-256 of the raw body) before acting on any webhook.
See `asyncapi/lightspark-grid-webhooks.yml`.

## UMA-specific errors

These are distinct from ordinary payout failures and mostly describe the *counterparty*:

- `INVALID_UMA_ADDRESS` — the address is malformed.
- `UNSUPPORTED_UMA_VERSION` (412) / `NO_COMPATIBLE_UMA_VERSION` (424) — protocol negotiation failed.
- `CERT_CHAIN_INVALID`, `CERT_CHAIN_EXPIRED`, `INVALID_PUBKEY_FORMAT` — counterparty trust failure.
- `MISSING_REQUIRED_UMA_PARAMETERS`, `UNRECOGNIZED_MANDATORY_PAYEE_DATA_KEY` (501) — the receiver
  demands payee data you did not supply, or a key Grid does not implement.
- `LNURLP_REQUEST_FAILED`, `PARSE_LNURLP_RESPONSE_ERROR`, `PAYREQ_REQUEST_FAILED`,
  `INVALID_PAYREQ_RESPONSE`, `PARSE_PAYREQ_RESPONSE_ERROR` (424) — counterparty is unreachable or
  non-conformant. Retryable.
- `SENDER_NOT_ACCEPTED` — the receiving VASP declined your platform as a sender.
- `SELF_PAYMENT` — sending to your own address.

## Sandbox

Send to these published test addresses:

| Address | Behavior |
|---|---|
| `$success.usd@sandbox.uma.money` | succeeds (USD) |
| `$success.eur@sandbox.uma.money` | succeeds (EUR) |
| `$success.mxn@sandbox.uma.money` | succeeds (MXN) |
| `$pending.long.usd@sandbox.uma.money` | long-pending payment |
| `$fail.compliance.usd@sandbox.uma.money` | compliance check failure |

Simulate an inbound payment to one of your users with `sandboxReceive`
(`POST /sandbox/uma/receive`).
