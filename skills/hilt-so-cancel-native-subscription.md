---
name: hilt-cancel-native-subscription
description: Read and cancel a buyer-approved native Solana USDC subscription through Hilt Pay API, choosing between access-to-paid-through-date and immediate revoke.
api: openapi/hilt-so-openapi.yml
operations:
  - read_native_subscription_v1_access_native_subscriptions__authorization_id__get
  - create_native_subscription_cancel_intent_v1_access_native_subscriptions__authorization_id__cancel_intent_post
  - confirm_native_subscription_cancel_v1_access_native_subscriptions__authorization_id__cancel_confirm_post
generated: '2026-09-19'
method: generated
source: openapi/hilt-so-openapi.yml + https://docs.hilt.so/merchant/native-subscriptions + conventions/hilt-so-conventions.yml (reversibility)
---

# Cancel a native Solana USDC subscription

Cancellation is **period-aware**: it stops future collection; whether access ends now or at the paid-through date is the merchant's choice. Completed collections are on-chain and are not reversible by Hilt (`https://www.hilt.so/legal/refund`).

## Steps
1. **Read current state.** `GET /v1/access/native-subscriptions/{authorization_id}` (`read_native_subscription_…`) — confirm status, paid-through date and whether reapproval is pending (`subscription_requires_reapproval`).
2. **Create the cancel intent.** `POST /v1/access/native-subscriptions/{authorization_id}/cancel-intent` (`create_native_subscription_cancel_intent_…`). The response carries what the buyer's wallet must sign to revoke the on-chain authorization.
3. **Confirm.** `POST /v1/access/native-subscriptions/{authorization_id}/cancel-confirm` (`confirm_native_subscription_cancel_…`) with `Idempotency-Key`, the `cancel_tx_signature`, a `reason`, `immediate_revoke` (`false` = "keep access available until the current paid-through date"; `true` = end access now) and `verify_onchain`.
4. **React to the events.** Expect `membership.expired` (or continued `membership.*` state until paid-through) on your webhook endpoint; `subscription_cancelled` is the error future collection attempts return.

## Do not
- Do not treat cancellation as a refund; there is no refund route. Goodwill refunds are merchant-side.
- Do not retry step 3 with a new idempotency key; reuse the original.
