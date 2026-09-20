---
name: hilt-mpp-metered-channel
description: Run a stream of metered Solana USDC work through one MPP payment channel — create, authorize, reserve deliveries, commit cumulative vouchers, settle once.
api: openapi/hilt-so-openapi.yml
operations:
  - create_mpp_metered_session_v1_access_metered_sessions_post
  - authorize_mpp_metered_session_v1_access_metered_sessions__session_id__authorize_post
  - create_mpp_metered_delivery_v1_access_metered_sessions__session_id__deliveries_post
  - commit_mpp_metered_delivery_v1_access_metered_sessions__session_id__commits_post
  - read_mpp_metered_session_v1_access_metered_sessions__session_id__get
  - settle_mpp_metered_session_v1_access_metered_sessions__session_id__settle_post
generated: '2026-09-19'
method: generated
source: openapi/hilt-so-openapi.yml + https://docs.hilt.so/developers/payment-channels (September 2026; SDK 1.5.0 methods)
---

# Meter a stream of work through an MPP channel

Use this instead of one x402 payment per request when a payer will make many calls. The payer opens **one** escrow deposit on the Solana channel program `CHNLxYvVA28MJP9PrFuDXccuoGXAx7jBacfLEkahyGsX`; Hilt enforces the metering ceiling; the merchant settles the highest accepted voucher once.

## Steps (merchant server, `X-Hilt-Key` + `Idempotency-Key` on every write)
1. **Create the session.** `POST /v1/access/metered-sessions` (`create_mpp_metered_session_…`). Expiry window is five minutes to 24 hours; the cap must be a whole number of product units; standard products carry a $50 fee cap, so one channel authorizes at most 5,000 USDC.
2. **Challenge the payer.** Answer the payer's request with `WWW-Authenticate: Payment` carrying the channel terms; the payer returns `Authorization: Payment <MPP credential>`. Validate it with `POST /v1/access/metered-sessions/{session_id}/authorize` (`authorize_mpp_metered_session_…`).
3. **Reserve each delivery.** `POST /v1/access/metered-sessions/{session_id}/deliveries` (`create_mpp_metered_delivery_…`) with a stable delivery id and `ttl_seconds`. Reusing the delivery id with the same amount returns the existing reservation; different terms fail with 409.
4. **Commit the voucher.** `POST /v1/access/metered-sessions/{session_id}/commits` (`commit_mpp_metered_delivery_…`) to the reservation's `commitUrl` with the payer's **cumulative** voucher. A later voucher replaces the earlier ceiling — it is never added. Commitments above the Hilt metering ceiling are rejected regardless of deposit size. Serve the work only after the commit is accepted; return `Payment-Receipt`.
5. **Inspect.** `GET /v1/access/metered-sessions/{session_id}` (`read_mpp_metered_session_…`) for evidence of what has been accepted.
6. **Settle once.** `POST /v1/access/metered-sessions/{session_id}/settle` (`settle_mpp_metered_session_…`) at the highest accepted voucher. Retrying with the same key is safe. The channel program pays the developer wallet and the Hilt fee (1% on Live pricing) directly from escrow; unused USDC returns to the payer through the channel close flow; a recovery worker runs at session expiry.

## Notes
- MPP channels are Solana USDC only.
- Postman folder "MPP metered payment channels" in `postman/hilt-so-postman-collection.json` carries the same six calls with environment variables `mppSessionId`, `mppChallenge`, `mppAuthorization`, `mppDeliveryId`, `mppCumulativeAmount`, `mppVoucherSignature`.
