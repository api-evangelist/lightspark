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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Lightspark builds global money-movement infrastructure on open payment networks. Its developer
product is the **Grid API** — a dated-version REST API for cross-border payouts, on/off-ramps,
stablecoins, embedded wallets, card issuing, KYC/KYB verification and payments to Universal Money
Addresses (`$user@domain`).

- Website: https://lightspark.com
- Docs: https://docs.lightspark.com/
- Base URL: `https://api.lightspark.com/grid/2025-10-13`
- Spec source: https://github.com/lightsparkdev/grid-api

Backed by a16z, Matrix Partners, Paradigm and Ribbit Capital.

## What is in this repo

| Area | Artifact |
|---|---|
| OpenAPI | `openapi/lightspark-grid-openapi-original.yml` — OpenAPI 3.1, 104 paths, 564 schemas, 12 native webhooks |
| Governance rules | `rules/lightspark-grid-spectral.yaml` — Lightspark's own published Spectral ruleset |
| Overlay | `overlays/lightspark-grid-overlay.yaml` |
| Errors | `errors/lightspark-error-codes.yml` (80 codes), `errors/lightspark-problem-types.yml` |
| Conventions | `conventions/lightspark-conventions.yml` — idempotency, cursor pagination, tracing, versioning |
| Lifecycle | `lifecycle/lightspark-lifecycle.yml` |
| Changelog | `changelog/lightspark-changelog.yml` |
| Sandbox | `sandbox/lightspark-sandbox.yml` — published magic suffixes and UMA test addresses |
| Webhooks | `asyncapi/lightspark-grid-webhooks.yml` — 12 events, P-256 `X-Grid-Signature` |
| Auth | `authentication/lightspark-authentication.yml` |
| Security | `security/` — domain security probe, bug bounty, compliance posture |
| Data model | `data-model/lightspark-data-model.yml` |
| Packages | `packages/lightspark-packages.yml` — TS, Kotlin, Python, Go, Rust, Dart |
| CLI | `cli/lightspark-cli.yml` — the open-source `grid` CLI |
| MCP | `mcp/lightspark-mcp.yml` — hosted `mcp.docs.lightspark.com` + `@lightsparkdev/grid-mcp` |
| Agent skills | `skills/` — Lightspark's own published skill plus six packaged flows |
| Agentic access | `agentic-access/lightspark-agentic-access.yml` — 132 classified operations |
| llms.txt | `llms/lightspark-llms.txt` |

## Notable

**Grid is one of the more agent-native payment APIs in the network.** It exposes agents as
first-class API objects: `POST /agents` issues a device code, the agent redeems it for a user-scoped
bearer token, every agent call is bound to its customer and constrained by a policy, and actions
that exceed policy park in `PENDING_APPROVAL` for a human to approve or reject. That is paired with
a hosted MCP server, a published agent skill (`npx skills add lightsparkdev/grid-api`), an
open-source CLI, and generated SDKs.

**Gaps worth noting.** No `/.well-known/security.txt` on any host, no dedicated trust center or
security page (compliance is announced via blog posts), no RFC 8594 `Sunset`/`Deprecation` headers,
no published rate-limit quota headers, no public roadmap, and errors use a proprietary
`{status, code, message, details}` envelope rather than RFC 9457 problem+json.
