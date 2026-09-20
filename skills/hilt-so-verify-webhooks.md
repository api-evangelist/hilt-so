---
name: hilt-verify-webhooks
description: Register a Hilt webhook endpoint, verify X-Hilt-Signature against the raw body, deduplicate by event id, and recover dead-letter deliveries with replay.
api: openapi/hilt-so-openapi.yml
operations:
  - create_webhook_endpoint_v1_webhooks_endpoints_post
  - create_webhook_v1_access_webhooks_post
  - test_webhook_endpoint_v1_webhooks_endpoints__endpoint_id__test_post
  - list_webhook_deliveries_v1_webhooks_deliveries_get
  - replay_owned_webhook_delivery_v1_webhooks_deliveries__delivery_id__replay_post
generated: '2026-09-19'
method: generated
source: openapi/hilt-so-openapi.yml + https://docs.hilt.so/developers/webhooks + asyncapi/hilt-so-webhooks-asyncapi.yml + github.com/Hiltpay/hilt-sdk-js/src/webhooks.ts
---

# Receive and verify Hilt webhooks

## Steps
1. **Register the endpoint.** Workspace: `POST /v1/webhooks/endpoints` (`create_webhook_endpoint_v1_webhooks_endpoints_post`, dashboard bearer token per the quickstart) with a label, URL and event list. Hilt Pay API: `POST /v1/access/webhooks` (`create_webhook_v1_access_webhooks_post`, `X-Hilt-Key`, `Idempotency-Key`). Store the returned signing secret server-side.
2. **Verify every delivery against the RAW body.** Header `X-Hilt-Signature: t=<unix_timestamp>,v1=<hex>`; recompute `HMAC-SHA256(secret, "<t>.<raw_json_body>")` and compare timing-safely. Parse JSON only after the compare passes. Failing this is `webhook_signature_failed`.
3. **Deduplicate by `id`.** Envelope fields: `id`, `type`, `api_version`, `created_at`, `livemode`, `data`. Treat deliveries as notifications from the source of truth, not permission to skip idempotency; payload order is not guaranteed.
4. **Return 2xx fast.** Anything else retries: immediate, 30 s, 2 min, 10 min, 30 min, 2 h, then dead_letter.
5. **Test before going live.** `POST /v1/webhooks/endpoints/{endpoint_id}/test` (`test_webhook_endpoint_…`) with `event_type` (e.g. `payment.confirmed`) sends a signed test event; CLI `hilt webhooks test ENDPOINT_ID --event payment.confirmed`.
6. **Recover.** `GET /v1/webhooks/deliveries?status=dead_letter` (`list_webhook_deliveries_…`), then `POST /v1/webhooks/deliveries/{delivery_id}/replay` (`replay_owned_webhook_delivery_…`).

## Event types (docs)
`payment.confirmed`, `payment.failed`, `receipt.created`, `membership.activated`, `membership.renewed`, `membership.entered_grace`, `membership.expired`, `membership.reapproval_required`, `delivery.failed`, `support.ticket.created`. Pay API subscriptions may also name `access.entitlement.activated` (SDK README); it is not enumerated on the docs page.

## Rule
Never unlock access from a webhook alone for metered work — the atomic consume (see `hilt-so-protect-metered-endpoint.md`) is the authority. Use `payment.confirmed` / `membership.*` to drive durable access and support state.
