---
name: hilt-agent-bootstrap-setup
description: Let a coding agent prepare a Hilt Pay API integration end to end — free sandbox bootstrap, setup manifest, owner approval, readiness check — without ever holding live keys or payout control.
api: openapi/hilt-so-openapi.yml
operations:
  - create_agent_bootstrap_v1_access_agent_bootstrap_post
  - submit_agent_bootstrap_manifest_v1_access_agent_bootstrap__setup_intent_id__manifest_post
  - get_agent_bootstrap_status_v1_access_agent_bootstrap__setup_intent_id__status_post
  - approve_agent_bootstrap_v1_access_agent_bootstrap__setup_intent_id__approve_post
  - setup_readiness_v1_access_setup_readiness_get
  - create_sandbox_payment_session_v1_access_sandbox_payment_sessions_post
  - confirm_sandbox_payment_session_v1_access_sandbox_payment_sessions__sandbox_session_id__confirm_post
generated: '2026-09-19'
method: generated
source: openapi/hilt-so-openapi.yml + https://docs.hilt.so/developers/agent-setup + https://docs.hilt.so/developers/agent-builder-kit + mcp/hilt-so-mcp-tools-list.json (hilt_agent_bootstrap inputSchema)
---

# Bootstrap Hilt Pay API as an agent

Hilt's model: the agent prepares everything and proves it in sandbox; a human owner approves billing, live keys, payout wallet and emergency disable. The same flow is exposed as the MCP tool `hilt_agent_bootstrap` on `https://api.hilt.so/mcp` and as the A2A skill `bootstrap_hilt_sandbox`.

## Steps
1. **Create the setup intent (no key needed).** `POST /v1/access/agent-bootstrap` (`create_agent_bootstrap_v1_access_agent_bootstrap_post`) with `agent_name` (required), and optionally `agent_platform`, `requested_use_case`, `contact_email`, `external_reference`, `requested_permissions` (`access:read`, `access:write`, `access:webhooks`), `ttl_hours` (1–168), `metadata`. Response: `setup_intent_id`, a `setup_token`, a scoped **sandbox** key, and `owner_approval_url`.
2. **Submit the manifest.** `POST /v1/access/agent-bootstrap/{setup_intent_id}/manifest` (`submit_agent_bootstrap_manifest_…`) with the `setup_token` and a manifest naming the app, the product (`external_product_id`, `amount_minor_units`, `default_rail: solana_usdc`, `billing_model`, `renewal_mode`), `payment_protocol: "x402"`, `settlement_rail: "solana_usdc"`, the `protected_resource` (url, method, `customer_identity`), and the `webhook` (url, `subscribed_events`). Hilt returns a manifest evaluation and a `pricing_recommendation`.
3. **Prove it in sandbox.** With the sandbox key: `POST /v1/access/sandbox/payment-sessions` → `POST /v1/access/sandbox/payment-sessions/{sandbox_session_id}/confirm` → `POST /v1/access/entitlements/check` should return `has_access: true`. No money moves. No test wallets or signatures are published — use only what the sandbox responses give you.
4. **Hand off to the owner.** Send the human to `owner_approval_url`. Only the owner completes `POST /v1/access/agent-bootstrap/{setup_intent_id}/approve` (`approve_agent_bootstrap_…`); poll `POST /v1/access/agent-bootstrap/{setup_intent_id}/status` (`get_agent_bootstrap_status_…`) for the live key delivery.
5. **Check readiness before go-live.** `GET /v1/access/setup/readiness` (`setup_readiness_v1_access_setup_readiness_get`) lists the concrete production blockers; `setup_not_ready` is the error you get if you skip it.

## Boundaries
- Keep `HILT_API_KEY` server-side; never in a client bundle or `NEXT_PUBLIC_*`.
- Live activation is a paid, explicit step. Agents may alternatively prepay via the x402 tools `hilt_activate_starter|growth|scale` (`plans/hilt-so-plans-pricing.yml`), then `hilt_claim_api_key`.
- Do not claim Base/EVM/USDT settlement is live; the public rails are Solana USDC (x402, MPP, subscriptions) and native SOL (hosted sessions only).
