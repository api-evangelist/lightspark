# Lightspark

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Lightspark builds global money-movement infrastructure on open payment networks. Its developer product is the Grid API — a dated-version REST API (OpenAPI 3.1, 104 paths, 564 schemas, 12 webhooks) for cross-border payouts, on/off-ramps, stablecoins, embedded wallets, card issuing, KYC/KYB verification and payments to Universal Money Addresses ($user@domain). Grid is unusually agent-native: it ships a first-class agent surface with device-code credentials, per-agent policy and human-in-the-loop approvals, a hosted MCP server, a published Claude agent skill, an open-source CLI, and generated TypeScript and Kotlin SDKs. Lightspark also operates the Spark and UMA protocol stacks and is backed by a16z, Matrix Partners, Paradigm and Ribbit Capital.

**Areas:** Company · Payments · Cross-Border Payments · Stablecoins · Bitcoin · Lightning Network · Embedded Finance · Agentic Payments · Cards · KYC · Financial Services · Foreign Exchange

## Lightspark on APIs.io

Everything profiled for Lightspark is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/lightspark/](https://apis.io/providers/lightspark/)** — or go straight to one of the APIs or properties below.

### APIs (23)

- [Lightspark Agent Management API](https://apis.io/apis/lightspark/lightspark-agent-management-api/) — Endpoints for creating and managing agents (experimental), called by the partner's backend using platform credentials. Covers the full agent lifecycle:…
- [Lightspark Agent Operations API](https://apis.io/apis/lightspark/lightspark-agent-operations-api/) — Endpoints called by the agent itself using its own credentials (obtained via device code redemption). Scoped to the agent's associated customer — all…
- [Lightspark API Tokens API](https://apis.io/apis/lightspark/lightspark-api-tokens-api/) — Endpoints to programmatically manage API tokens
- [Lightspark Available UMA Providers API](https://apis.io/apis/lightspark/lightspark-available-uma-providers-api/) — The Available UMA Providers API from Lightspark — 1 operation(s) for available uma providers.
- [Lightspark Cards API](https://apis.io/apis/lightspark/lightspark-cards-api/) — Card management endpoints. Issue debit cards against an internal account, freeze / unfreeze, close, manage card funding sources, and list card transactions.
- [Lightspark Contact Verification API](https://apis.io/apis/lightspark/lightspark-contact-verification-api/) — Endpoints for verifying a customer's email and phone via one-time codes. Required only for customers whose payment provider mandates contact verification…
- [Lightspark Cross-Currency Transfers API](https://apis.io/apis/lightspark/lightspark-cross-currency-transfers-api/) — Endpoints for creating and confirming quotes for cross-currency transfers
- [Lightspark Customers API](https://apis.io/apis/lightspark/lightspark-customers-api/) — Customer management endpoints for creating and updating customer information
- [Lightspark Discoveries API](https://apis.io/apis/lightspark/lightspark-discoveries-api/) — Endpoints for discovering available payment rails, banks, and providers for a given country and currency corridor.
- [Lightspark Documents API](https://apis.io/apis/lightspark/lightspark-documents-api/) — Endpoints for uploading and managing verification documents for customers and beneficial owners. Supports KYC and KYB document requirements.
- [Lightspark Embedded Wallet Auth API](https://apis.io/apis/lightspark/lightspark-embedded-wallet-auth-api/) — Endpoints for registering and verifying end-user authentication credentials (email OTP, OAuth, passkey) used to sign Embedded Wallet actions.
- [Lightspark Exchange Rates API](https://apis.io/apis/lightspark/lightspark-exchange-rates-api/) — Endpoints for retrieving cached foreign exchange rates. Rates are cached for approximately 5 minutes and include platform-specific fees.
- [Lightspark External Accounts API](https://apis.io/apis/lightspark/lightspark-external-accounts-api/) — External account management endpoints for creating and managing external bank accounts
- [Lightspark Internal Accounts API](https://apis.io/apis/lightspark/lightspark-internal-accounts-api/) — Internal account management endpoints for creating and managing internal accounts
- [Lightspark Invitations API](https://apis.io/apis/lightspark/lightspark-invitations-api/) — Endpoints for creating, claiming and managing UMA invitations
- [Lightspark KYC/KYB Verifications API](https://apis.io/apis/lightspark/lightspark-kyc-kyb-verifications-api/) — Endpoints for Know Your Customer (KYC) and Know Your Business (KYB) verification, including managing beneficial owners and triggering verification for…
- [Lightspark Platform Configuration API](https://apis.io/apis/lightspark/lightspark-platform-configuration-api/) — Platform configuration endpoints for managing global settings. You can also configure these settings in the Grid dashboard.
- [Lightspark Same-Currency Transfers API](https://apis.io/apis/lightspark/lightspark-same-currency-transfers-api/) — Endpoints for transferring funds between internal and external accounts with the same currency
- [Lightspark Sandbox API](https://apis.io/apis/lightspark/lightspark-sandbox-api/) — Endpoints to trigger test cases in sandbox
- [Lightspark Stablecoins API](https://apis.io/apis/lightspark/lightspark-stablecoins-api/) — Stablecoin issuance endpoints. Link provider accounts, register provider-created stablecoins, create mint/burn quotes, execute them, and track the resulting…
- [Lightspark Strong Customer Authentication API](https://apis.io/apis/lightspark/lightspark-strong-customer-authentication-api/) — Endpoints for authorizing money-movement operations that require Strong Customer Authentication. Relevant only for customers in a region where SCA is…
- [Lightspark Transactions API](https://apis.io/apis/lightspark/lightspark-transactions-api/) — Endpoints for retrieving transaction information
- [Lightspark Webhooks API](https://apis.io/apis/lightspark/lightspark-webhooks-api/) — Webhook endpoints and configuration for receiving notifications

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Lightspark Grid Webhooks](https://apis.io/asyncapis/lightspark/lightspark-grid-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [lightspark-mcp.yml](https://apis.io/servers/lightspark/lightspark-mcp-yml/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Lightspark Agentic Access](https://apis.io/agentic-access/lightspark/lightspark-agentic-access/)

#### JSON Schema (78)

The data models the API reads and writes.

- [Agent](https://apis.io/schemas/lightspark/lightspark-agent/)
- [AgentAction](https://apis.io/schemas/lightspark/lightspark-agent-action/)
- [AgentActionListResponse](https://apis.io/schemas/lightspark/lightspark-agent-action-list-response/)
- [AgentDeviceCode](https://apis.io/schemas/lightspark/lightspark-agent-device-code/)
- [AgentDeviceCodeRedeemResponse](https://apis.io/schemas/lightspark/lightspark-agent-device-code-redeem-response/)
- [AgentPolicyUpdateRequest](https://apis.io/schemas/lightspark/lightspark-agent-policy-update-request/)
- [ApiToken](https://apis.io/schemas/lightspark/lightspark-api-token/)
- [ApiTokenCreateRequest](https://apis.io/schemas/lightspark/lightspark-api-token-create-request/)
- [ApprovePaymentRequest](https://apis.io/schemas/lightspark/lightspark-approve-payment-request/)
- [Auth Credential Challenge Request](https://apis.io/schemas/lightspark/lightspark-auth-credential-challenge-request/)
- [Auth Method Response](https://apis.io/schemas/lightspark/lightspark-auth-method-response/)
- [Authentication Session](https://apis.io/schemas/lightspark/lightspark-auth-session/)
- [Authentication Signed Request Challenge](https://apis.io/schemas/lightspark/lightspark-auth-signed-request-challenge/)
- [BeneficialOwner](https://apis.io/schemas/lightspark/lightspark-beneficial-owner/)
- [BeneficialOwnerCreateRequest](https://apis.io/schemas/lightspark/lightspark-beneficial-owner-create-request/)
- [BeneficialOwnerListResponse](https://apis.io/schemas/lightspark/lightspark-beneficial-owner-list-response/)
- [BeneficiaryTrustConfirmRequest](https://apis.io/schemas/lightspark/lightspark-beneficiary-trust-confirm-request/)
- [BulkCustomerImportJob](https://apis.io/schemas/lightspark/lightspark-bulk-customer-import-job/)
- [Card](https://apis.io/schemas/lightspark/lightspark-card/)
- [CardCreateRequest](https://apis.io/schemas/lightspark/lightspark-card-create-request/)
- [CardListResponse](https://apis.io/schemas/lightspark/lightspark-card-list-response/)
- [CardRevealResponse](https://apis.io/schemas/lightspark/lightspark-card-reveal-response/)
- [Card Transaction](https://apis.io/schemas/lightspark/lightspark-card-transaction/)
- [CardUpdateRequest](https://apis.io/schemas/lightspark/lightspark-card-update-request/)
- [ConfirmReceiptDeliveryRequest](https://apis.io/schemas/lightspark/lightspark-confirm-receipt-delivery-request/)
- …and 53 more published on APIs.io

#### JSON-LD (1)

Linked-data contexts for the provider's vocabulary.

- [Lightspark Context](https://apis.io/jsonld/lightspark/lightspark-context/)

#### Collections (44)

Postman and Open Collection request collections.

- [Grid Agent Management API](https://apis.io/collections/lightspark/open-lightspark-agent-management-api/)
- [Grid Agent Management Agent Operations API](https://apis.io/collections/lightspark/open-lightspark-agent-operations-api/)
- [Grid Agent Management API Tokens API](https://apis.io/collections/lightspark/open-lightspark-api-tokens-api/)
- [Grid Agent Management Available UMA Providers API](https://apis.io/collections/lightspark/open-lightspark-available-uma-providers-api/)
- [Grid Agent Management Cards API](https://apis.io/collections/lightspark/open-lightspark-cards-api/)
- [Grid Agent Management Contact Verification API](https://apis.io/collections/lightspark/open-lightspark-contact-verification-api/)
- [Grid Agent Management Cross-Currency Transfers API](https://apis.io/collections/lightspark/open-lightspark-cross-currency-transfers-api/)
- [Grid Agent Management Customers API](https://apis.io/collections/lightspark/open-lightspark-customers-api/)
- [Grid Agent Management Discoveries API](https://apis.io/collections/lightspark/open-lightspark-discoveries-api/)
- [Grid Agent Management Documents API](https://apis.io/collections/lightspark/open-lightspark-documents-api/)
- [Grid Agent Management Embedded Wallet Auth API](https://apis.io/collections/lightspark/open-lightspark-embedded-wallet-auth-api/)
- [Grid Agent Management Exchange Rates API](https://apis.io/collections/lightspark/open-lightspark-exchange-rates-api/)
- [Grid Agent Management External Accounts API](https://apis.io/collections/lightspark/open-lightspark-external-accounts-api/)
- [Grid Agent Management Internal Accounts API](https://apis.io/collections/lightspark/open-lightspark-internal-accounts-api/)
- [Grid Agent Management Invitations API](https://apis.io/collections/lightspark/open-lightspark-invitations-api/)
- [Grid Agent Management KYC/KYB Verifications API](https://apis.io/collections/lightspark/open-lightspark-kyc-kyb-verifications-api/)
- [Grid Agent Management Platform Configuration API](https://apis.io/collections/lightspark/open-lightspark-platform-configuration-api/)
- [Grid Agent Management Same-Currency Transfers API](https://apis.io/collections/lightspark/open-lightspark-same-currency-transfers-api/)
- [Grid Agent Management Sandbox API](https://apis.io/collections/lightspark/open-lightspark-sandbox-api/)
- [Grid Agent Management Stablecoins API](https://apis.io/collections/lightspark/open-lightspark-stablecoins-api/)
- [Grid Agent Management Strong Customer Authentication API](https://apis.io/collections/lightspark/open-lightspark-strong-customer-authentication-api/)
- [Grid Agent Management Transactions API](https://apis.io/collections/lightspark/open-lightspark-transactions-api/)
- [Grid Agent Management API](https://apis.io/collections/lightspark/postman-lightspark-agent-management-api/)
- [Grid Agent Management Agent Operations API](https://apis.io/collections/lightspark/postman-lightspark-agent-operations-api/)
- [Grid Agent Management API Tokens API](https://apis.io/collections/lightspark/postman-lightspark-api-tokens-api/)
- …and 19 more published on APIs.io

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Lightspark Grid Overlay](https://apis.io/overlays/lightspark/lightspark-grid-overlay/)

#### Governance rules (3)

Spectral rulesets for the provider's contracts.

- [Lightspark — grid api rules](https://apis.io/rules/lightspark/lightspark-grid-api-spectral-rules/)
- [Lightspark — grid spectral rules](https://apis.io/rules/lightspark/lightspark-grid-spectral/)
- [Lightspark API Rules](https://apis.io/rules/lightspark/lightspark-rules/)

#### Security (4)

Authentication, trust centre, and vulnerability disclosure.

- [Lightspark Authentication](https://apis.io/security/lightspark/lightspark-authentication/)
- [Lightspark Domain Security](https://apis.io/security/lightspark/lightspark-domain-security/)
- [Lightspark Trust Center](https://apis.io/security/lightspark/lightspark-trust-center/)
- [Lightspark Vulnerability Disclosure](https://apis.io/security/lightspark/lightspark-vulnerability-disclosure/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Lightspark Plans Pricing](https://apis.io/plans/lightspark/lightspark-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Lightspark Rate Limits](https://apis.io/rate-limits/lightspark/lightspark-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://lightspark.com)
- [Documentation](https://docs.lightspark.com/)
- [Getting started](https://docs.lightspark.com/global-p2p/quickstart)
- [API reference](https://docs.lightspark.com/api-reference/authentication)
- [Sign up](https://app.lightspark.com)
- [Support](https://www.lightspark.com/contact)
- [Changelog](https://docs.lightspark.com/changelog)
- [Blog](https://www.lightspark.com/news)
- [Security](https://www.lightspark.com/news/lightspark/expanding-our-bug-bounty-program)
- [Terms of service](https://www.lightspark.com/terms-of-use)
- [Privacy policy](https://www.lightspark.com/privacy-policy)
- [GitHub](https://github.com/lightsparkdev)
- [Status](https://status.lightspark.com/)

## API Evangelist rating

**Kin Score 67.3** — exemplar · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 75.9 |
| Contract governance | 35.6 |
| Operational transparency | 68.4 |
| Developer ergonomics | 81.5 |
| Access clarity | 36.8 |

**Agent readiness 46.4** — agent-native

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | documented (partial credit) |
| MCP Server | platform (partial credit) |
| Auth Clarity | bearer (partial credit) |
| Idempotency | verified |
| Error Semantics | verified |
| OpenAPI Examples | partial |
| Rate Limit Signal | verified |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | partial |
| Operation Distinctiveness | mostly |

**Regulatory alignment 32.1** — Payments

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/lightspark/](https://apis.io/providers/lightspark/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Lightspark: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/lightspark/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
