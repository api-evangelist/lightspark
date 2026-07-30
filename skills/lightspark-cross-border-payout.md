---
name: lightspark-cross-border-payout
description: Send a cross-currency payout from a Lightspark Grid internal account to an external bank account or wallet — quote it, review the rate, execute it, and reconcile the transaction.
api: openapi/lightspark-grid-openapi-original.yml
base_url: https://api.lightspark.com/grid/2025-10-13
operations:
  - createCustomer
  - createCustomerExternalAccount
  - lookupExternalAccount
  - createQuote
  - executeQuote
  - getQuoteById
  - listTransactions
  - getTransactionById
generated: '2026-07-19'
method: generated
source: openapi/lightspark-grid-openapi-original.yml
---

# Cross-border payout with Grid

Move money from a Grid internal account to an external bank account or crypto wallet in another
currency. Grid quotes the FX rate first; you execute the quote to move the funds.

## Auth

HTTP Basic — the API token id is the username, the client secret is the password.

```
curl -u "$GRID_CLIENT_ID:$GRID_CLIENT_SECRET" https://api.lightspark.com/grid/2025-10-13/...
```

Tokens are scoped to exactly one environment. Start in sandbox.

## Steps

1. **Ensure the customer exists.** `createCustomer` (`POST /customers`). If the customer already
   exists on your platform, `listCustomers` filtered by `platformCustomerId` avoids a `409 CONFLICT`.
2. **Register the destination.** `createCustomerExternalAccount`
   (`POST /customers/external-accounts`) with the country-appropriate identifier — CLABE for MX,
   PIX key for BR, IBAN for EUR, UPI for IN, account/routing for US.
3. **Validate before you quote.** `lookupExternalAccount`
   (`GET /receiver/external-account/{accountId}`) returns the receiver's capabilities and, where the
   rail supports it, a `beneficiaryVerificationStatus`. Treat `NOT_MATCHED` as a stop.
4. **Quote it.** `createQuote` (`POST /quotes`) with source account, destination external account
   and the sending amount. Show the returned rate and fees to the payer before executing — quotes
   expire and a stale one fails with `QUOTE_EXPIRED`.
5. **Execute.** `executeQuote` (`POST /quotes/{quoteId}/execute`). **Always send an
   `Idempotency-Key` header** with a client-generated UUID — retrying with the same key returns the
   original response instead of double-sending money.
6. **Reconcile.** `getQuoteById` (`GET /quotes/{quoteId}`) and `getTransactionById`
   (`GET /transactions/{transactionId}`); or `listTransactions` (`GET /transactions`) with
   `cursor`/`limit` for a sweep. Settlement is asynchronous — the `outgoing-payment` webhook is the
   authoritative signal, not the execute response.

## Rules

- **Idempotency:** `Idempotency-Key` is accepted on the mutating operations. Same key ⇒ same
  response as the first request. Never retry a payment without one.
- **Pagination:** cursor-based. Send `cursor` + `limit`; read `data`, `hasMore`, `nextCursor`,
  `totalCount`. Do not assume offsets.
- **Errors:** the envelope is `{status, code, message, details}` — not RFC 9457 problem+json. Branch
  on `code`, never on `message`. See `errors/lightspark-error-codes.yml` for all 80 codes.
- **Retryable vs terminal:** `QUOTE_REQUEST_FAILED` is explicitly retryable. `INVALID_RECEIVER`,
  `INVALID_BANK_ACCOUNT`, `SELF_PAYMENT` and `AMOUNT_OUT_OF_RANGE` are terminal — fix the input.
- **Rate limiting:** `429` returns code `RATE_LIMITED` and a `Retry-After` header. Back off, do not
  hot-loop.
- **Versioning:** the `2025-10-13` segment in the base URL is the major version and is pinned by you.

## Sandbox

The last three digits of the destination account number drive the outcome: `002` execution failed,
`003` long payment (~6 min), `004` counterparty delivery failed, `005` returned by receiving bank,
`006` user cancellation, `007` payout and refund failed, anything else succeeds. Fund the source
with `sandboxFundInternalAccount` (`POST /sandbox/internal-accounts/{accountId}/fund`).
Full table: `sandbox/lightspark-sandbox.yml`.
