# Lightspark

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
