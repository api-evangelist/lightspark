---
name: lightspark-webhook-verification
description: Receive and cryptographically verify Lightspark Grid webhooks — validate the X-Grid-Signature P-256 signature, route the twelve event types, and use the sandbox test webhook to prove the endpoint works.
api: openapi/lightspark-grid-openapi-original.yml
base_url: https://api.lightspark.com/grid/2025-10-13
operations:
  - sendTestWebhook
  - getPlatformConfig
  - updatePlatformConfig
generated: '2026-07-19'
method: generated
source: openapi/lightspark-grid-openapi-original.yml
---

# Grid webhook verification

Webhooks are the authoritative signal for anything asynchronous in Grid — payment settlement, KYC
outcomes, card events, agent approvals. Never treat a 2xx from an execute call as final state.

## Verify before you trust

Every webhook carries an `X-Grid-Signature` header: a secp256r1 (P-256) asymmetric signature over a
SHA-256 hash of the **raw request body**.

1. Get your Grid webhook public key (PEM) from the dashboard at `https://app.lightspark.com` under
   Developers → webhook settings.
2. Read `X-Grid-Signature`. It is JSON of the form `{"v": "1", "s": "<base64 signature>"}`; a bare
   base64 string is also accepted, so parse defensively.
3. Base64-decode `s`, SHA-256 the raw body, and verify with the public key.
4. Reject with `401` if verification fails. Only then parse the payload.

Verify against the **raw bytes**, not a re-serialized JSON object — any middleware that reparses and
re-stringifies the body will break the signature.

Grid also publishes its egress IPs, so you can allowlist as defense in depth:
`52.42.15.30`, `34.216.87.164`, `44.226.21.146`. Lightspark notifies the account contact email
before changing them.

## The twelve event types

| Event | Meaning |
|---|---|
| `incoming-payment` | Inbound payment — also the approval mechanism, you may reject before credit |
| `outgoing-payment` | Outbound payment status transition (terminal settlement signal) |
| `agent-action` | An agent action is parked in `PENDING_APPROVAL` |
| `customer-update` | Customer status change |
| `verification-update` | KYC/KYB verification status change |
| `internal-account-status` | Internal account status change |
| `invitation-claimed` | An invitation was claimed |
| `bulk-upload` | Bulk customer CSV import finished |
| `card-state-change` | Card state transition |
| `card-funding-source-change` | Card funding source changed |
| `card-transaction` | Card authorization / clearing / return |
| `test-webhook` | Integration verification only |

Payment payload `type` fields are prefixed — branch on `INCOMING_PAYMENT.` and `OUTGOING_PAYMENT.`
rather than matching whole strings, so new subtypes do not break routing.

## Handling rules

- **Be idempotent on receipt.** Redelivery is normal; key on the event id and make replays no-ops.
- **Ack fast, work async.** Return `200` as soon as the signature checks out; do the work off the
  request thread.
- **Tolerate unknown fields and unknown enum values.** Grid ships new response fields, enum values
  and webhook event types inside the current dated version without a version bump.
- Configuration problems surface on the API side as `WEBHOOK_ENDPOINT_NOT_SET` and
  `WEBHOOK_DELIVERY_ERROR` (400).

## Test it

`sendTestWebhook` (`POST /sandbox/webhooks/test`) delivers a `test-webhook` event to your configured
endpoint — the fastest way to prove signature verification works end to end before real money is
involved. Confirm or change the endpoint with `getPlatformConfig` (`GET /config`) and
`updatePlatformConfig` (`PATCH /config`).
