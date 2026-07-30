---
name: lightspark-agent-payments
description: Provision an AI agent with scoped, policy-bound payment access on Lightspark Grid — create the agent, redeem its device code, let it quote and execute payments as a customer, and approve or reject the actions that need a human.
api: openapi/lightspark-grid-openapi-original.yml
base_url: https://api.lightspark.com/grid/2025-10-13
operations:
  - createAgent
  - listAgents
  - getAgentById
  - updateAgentPolicy
  - regenerateAgentDeviceCode
  - getAgentDeviceCodeStatus
  - redeemAgentDeviceCode
  - getAgentMe
  - agentCreateQuote
  - agentExecuteQuote
  - agentListActions
  - agentGetAction
  - listAgentApprovals
  - approveAgentAction
  - rejectAgentAction
  - deleteAgent
generated: '2026-07-19'
method: generated
source: openapi/lightspark-grid-openapi-original.yml
---

# Agentic payments on Grid

Grid has a first-class agent surface: agents get their own bearer credential, their own `/agents/me`
namespace, and a policy that decides which of their actions need platform approval before money
moves. This is the flow to wire an autonomous agent up safely.

## Two credentials, two roles

- **Platform** — HTTP Basic (`BasicAuth`, client id : client secret). Provisions agents, sets
  policy, approves actions. Never give this to the agent.
- **Agent** — HTTP Bearer (`AgentAuth`). The token is the `accessToken` returned by
  `redeemAgentDeviceCode`. It is **user-scoped**: every request is automatically bound to the
  agent's customer and constrained by the agent's policy. This is what the agent software holds.

## Provisioning (platform side)

1. `createAgent` (`POST /agents`) with the policy. Returns the agent plus a **device code**.
2. Hand the device code to the agent software; it calls `redeemAgentDeviceCode`
   (`POST /agents/device-codes/{code}/redeem`) to exchange it for an `accessToken`.
3. Poll `getAgentDeviceCodeStatus` (`GET /agents/device-codes/{code}/status`) to know when
   installation completed. `regenerateAgentDeviceCode` issues a fresh code if the first goes stale.
4. `updateAgentPolicy` (`PATCH /agents/{agentId}/policy`) to tighten or loosen what the agent may do
   without approval. `deleteAgent` revokes access immediately — connected agent software loses
   access at once.

## Operating (agent side, bearer token)

- `getAgentMe` (`GET /agents/me`) — who am I, what am I allowed to do.
- `agentListInternalAccounts` / `agentListExternalAccounts` / `agentCreateExternalAccount` — the
  agent's own account surface.
- `agentCreateQuote` (`POST /agents/me/quotes`) → `agentExecuteQuote`
  (`POST /agents/me/quotes/{quoteId}/execute`).
- `agentCreateTransferIn` / `agentCreateTransferOut` for same-currency movement.
- `agentListActions` / `agentGetAction` — the agent's own audit trail, including anything parked
  awaiting approval.

## Human-in-the-loop

When policy requires it, an action lands in `PENDING_APPROVAL` instead of executing and the
`agent-action` webhook fires.

1. `listAgentApprovals` (`GET /agents/approvals`), filterable by `agentId` or `customerId`.
2. `approveAgentAction` (`POST /agents/{agentId}/actions/{actionId}/approve`) — Grid then executes
   the underlying quote execution or transfer and the action moves to `APPROVED`.
3. `rejectAgentAction` (`POST /agents/{agentId}/actions/{actionId}/reject`).

An action must be in `PENDING_APPROVAL` to be actioned; otherwise you get `409`
`TRANSACTION_NOT_PENDING_PLATFORM_APPROVAL`.

## Rules for agents

- Send an `Idempotency-Key` on every execute. An agent that retries without one can double-spend.
- Scope the token to sandbox and read-only while developing. Lightspark says this explicitly for the
  MCP `execute` tool, and it applies equally to agent tokens.
- Treat `403 VELOCITY_LIMIT_EXCEEDED` and `403 COUNTERPARTY_NOT_ALLOWED` as policy decisions, not
  transient errors — do not retry them.
- The recommended execution contracts per operation are derived in
  `agentic-access/lightspark-agentic-access.yml`.

## Related surfaces

Lightspark also ships a hosted MCP server at `https://mcp.docs.lightspark.com/` (tools:
`search_docs`, `execute`) and a published Claude skill — `npx skills add lightsparkdev/grid-api`.
See `mcp/lightspark-mcp.yml`.
