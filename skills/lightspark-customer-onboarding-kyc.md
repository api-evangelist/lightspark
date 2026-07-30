---
name: lightspark-customer-onboarding-kyc
description: Onboard an individual or business customer onto Lightspark Grid — create the customer, verify email and phone, collect beneficial owners and documents, and run KYC/KYB to an approved state.
api: openapi/lightspark-grid-openapi-original.yml
base_url: https://api.lightspark.com/grid/2025-10-13
operations:
  - createCustomer
  - listCustomers
  - getCustomerById
  - updateCustomerById
  - sendCustomerEmailVerification
  - confirmCustomerEmailVerification
  - sendCustomerPhoneVerification
  - confirmCustomerPhoneVerification
  - createBeneficialOwner
  - listBeneficialOwners
  - uploadDocument
  - createVerification
  - getVerification
  - listVerifications
  - createCustomerKycLink
generated: '2026-07-19'
method: generated
source: openapi/lightspark-grid-openapi-original.yml
---

# Customer onboarding and KYC/KYB

Grid will not move money for a customer until verification reaches an approved state. This is the
gate in front of every other flow.

## Steps

1. **Create the customer.** `createCustomer` (`POST /customers`) with `type` `INDIVIDUAL` or
   `BUSINESS` and your own `platformCustomerId`. A collision on `platformCustomerId` against an
   existing active customer returns `409 CONFLICT` — call `listCustomers` (`GET /customers`) first
   if you may be re-running.
2. **Verify contact details.** `sendCustomerEmailVerification` /
   `confirmCustomerEmailVerification` and `sendCustomerPhoneVerification` /
   `confirmCustomerPhoneVerification`. Resends are rate-limited — `429 RATE_LIMITED` with a
   `Retry-After` header — so do not loop.
3. **Business customers: add beneficial owners.** `createBeneficialOwner`
   (`POST /beneficial-owners`) for each owner; `listBeneficialOwners` to confirm the set.
4. **Attach documents.** `uploadDocument` (`POST /documents`), then `getDocument` /
   `replaceDocument` if a document is rejected. Document rejection surfaces as `LOW_QUALITY`,
   `DATA_MISMATCH`, `EXPIRED`, `SUSPECTED_FRAUD`, `UNSUITABLE_DOCUMENT` or `INCOMPLETE` — each one
   tells the customer exactly what to re-submit.
5. **Run verification.** `createVerification` (`POST /verifications`). Poll `getVerification`
   (`GET /verifications/{verificationId}`) or, better, subscribe to the `verification-update`
   webhook. `MISSING_MANDATORY_USER_INFO` means the customer record is incomplete — patch it with
   `updateCustomerById` and retry.
6. **Hosted alternative.** `createCustomerKycLink`
   (`POST /customers/{customerId}/kyc-link`) returns a hosted KYC link you can hand to the end user
   instead of collecting documents yourself. This operation accepts an `Idempotency-Key`.

## Gating

Until verification is approved, payment operations fail with `USER_NOT_READY` (403). Other states
worth handling: `CUSTOMER_DELETED` (410), `ACCOUNT_LOCKED` (423), `VELOCITY_LIMIT_EXCEEDED` (403)
and `COUNTERPARTY_NOT_ALLOWED` (403).

## Bulk

For migrations, `uploadCustomersCsv` (`POST /customers/bulk/csv`) accepts a CSV; track it with
`getBulkCustomerImportJob` (`GET /customers/bulk/jobs/{jobId}`) or the `bulk-upload` webhook.

## Sandbox

Verification outcomes are driven by magic suffixes — no waiting on real review:

- Business KYB: last 3 digits of `businessInfo.registrationNumber` — `001` PENDING, `002` REJECTED,
  anything else APPROVED.
- Individual KYC: last 3 characters of `personalInfo.lastName` — `001` PENDING, `002` REJECTED,
  anything else APPROVED.
