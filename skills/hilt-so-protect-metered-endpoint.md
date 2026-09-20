---
name: hilt-protect-metered-endpoint
description: Gate a per-request (metered) API route behind Hilt Pay API — consume one usage unit, answer HTTP 402 with Hilt's x402 V2 PAYMENT-REQUIRED when usage is missing, settle the buyer's PAYMENT-SIGNATURE, consume, then serve.
api: openapi/hilt-so-openapi.yml
operations:
  - consume_entitlement_usage_v1_access_entitlements_consume_post
  - create_payment_session_v1_access_payment_sessions_post
  - settle_x402_payment_v1_access_x402_settle_post
  - check_entitlement_v1_access_entitlements_check_post
generated: '2026-09-19'
method: generated
source: openapi/hilt-so-openapi.yml + https://docs.hilt.so/developers/protect-an-endpoint + https://docs.hilt.so/developers/agent-micropayments + the provider-published skills/hilt-so-hilt-pay-api-skill.md
---

# Protect a metered endpoint with Hilt Pay API

The runtime sequence Hilt publishes is **consume, challenge, pay, settle, consume, serve**. The payment is the middle of the request, not the end. Only the merchant server ever holds `X-Hilt-Key`; the buyer/agent only ever sees `PAYMENT-REQUIRED` and sends back `PAYMENT-SIGNATURE`.

## Before you start
- Base URL `https://api.hilt.so`; header `X-Hilt-Key: hk_live_...` (or `hk_sandbox_...` — see `sandbox/hilt-so-sandbox.yml`).
- Every write below takes an `Idempotency-Key` header (`conventions/hilt-so-conventions.yml`). Reuse the SAME key and the same stable request id on every retry of the same logical request; a different body under the same key returns `idempotency_conflict` (409).
- Settlement rail is Solana USDC for x402. Native SOL uses hosted payment sessions instead (out of scope here).

## Steps
1. **Try to consume one unit first.** `POST /v1/access/entitlements/consume` (`consume_entitlement_usage_v1_access_entitlements_consume_post`) with `external_product_id`, `external_customer_id`, the request id and `Idempotency-Key`. If the response says consumed, skip to step 5. Concurrent requests cannot consume the same final unit twice.
2. **Challenge when usage is missing.** Create a session with `POST /v1/access/payment-sessions` (`create_payment_session_v1_access_payment_sessions_post`, `payment_protocol: "x402"`, `settlement_rail: "solana_usdc"`) and return **HTTP 402** to the caller with Hilt's base64 requirement in the `PAYMENT-REQUIRED` header. Do not invent prices or routes; relay what Hilt returned.
3. **Buyer pays and retries.** The buyer validates the requirement, signs under its wallet policy, and retries the *same* request with a `PAYMENT-SIGNATURE` header. Nothing is served yet.
4. **Settle, then consume.** `POST /v1/access/x402/settle` (`settle_x402_payment_v1_access_x402_settle_post`) with the `PAYMENT-SIGNATURE` header value. On success Hilt returns `PAYMENT-RESPONSE`, a receipt and an active entitlement. Then call consume again (step 1) with the same request id. Settlement reconciliation is idempotent: a retry may reuse a finalized Solana transaction.
5. **Serve.** Return the billable result only after settlement *and* consumption both succeeded. Echo `PAYMENT-RESPONSE` on the 200.

## Rules the docs insist on
- Use `POST /v1/access/entitlements/check` (`check_entitlement_v1_access_entitlements_check_post`, `has_access`) only for durable/time-based access display and planning — never as the metered authority.
- Never grant access from a transaction hash, wallet signature, client claim, a webhook alone, or a pending payment session.
- Errors arrive as `{"detail": ...}`; codes `entitlement_missing`, `payment_failed`, `setup_not_ready`, `idempotency_*` and `rate_limited` are catalogued in `errors/hilt-so-problem-types.yml`. On 429 honour `Retry-After`.
- Make your own handler side effects idempotent by request id.

## SDK shortcut
`@hiltpay/sdk` `protectEndpoint({ client, externalProductId, handler })` (1.4.0+) and `hilt-sdk` `protect_request` implement steps 1–5 as one wrapper. Runnable examples: `examples/agent-micropayments` and `examples/hilt-access-fastapi` in github.com/Hiltpay/hilt-developer-assets.
