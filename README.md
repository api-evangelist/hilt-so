# Hilt

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

Hilt is a zero-custody Solana payments company operated in the United Kingdom by Paul Wild trading as Hilt (London). It ships four connected products: PayMe (a free receiving link and QR for an OAuth-verified X handle, sender pays a flat 2% fee), Direct Checkout (a no-account SOL / USDC / single-token checkout link), Hilt Pay Workspace (the merchant dashboard for hosted checkout, embeds, WooCommerce, receipts, memberships, native Solana USDC subscriptions and signed webhooks) and Hilt Pay API, the developer and agent product under /v1/access that turns an HTTP 402 into an operating record: x402 V2 payment requirement, Solana USDC or native SOL settlement, receipt, entitlement, atomic metered usage consumption, MPP payment channels and webhook trail. Hilt publishes an OpenAPI 3.1 contract (165 operations on api.hilt.so), a hosted MCP gateway and an OAuth-gated PayMe MCP connector, an A2A agent card, llms.txt on three hosts, TypeScript and Python SDKs, a CLI, Postman assets and a documented sandbox. Live pricing is $0/month plus 1% per successful settlement.

**Areas:** Payments · Solana · Stablecoins · USDC · Crypto Payments · Agentic Payments · x402 · Checkout · Subscription · Webhook · MCP · Entitlements

## Hilt on APIs.io

Everything profiled for Hilt is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/hilt-so/](https://apis.io/providers/hilt-so/)** — or go straight to one of the APIs or properties below.

### APIs (21)

- [Hilt Pay Agent Gateway (MCP + A2A)](https://apis.io/apis/hilt-so/agent-gateway/) — Hosted MCP server at https://api.hilt.so/mcp (streamable HTTP, protocol 2025-06-18, server Hilt Pay Agent Gateway 1.1.0) exposing nine tools: free…
- [Hilt PayMe MCP Connector](https://apis.io/apis/hilt-so/payme-mcp/) — OAuth-gated remote MCP resource at https://api.hilt.so/mcp/pay-me for compatible AI clients: resolve a verified PayMe handle, start a wallet-approved SOL or…
- [Hilt Account API](https://apis.io/apis/hilt-so/hilt-so-account-api/) — The account API from Hilt — 7 operation(s) for account.
- [Hilt Agent Commerce API](https://apis.io/apis/hilt-so/hilt-so-agent-commerce-api/) — The Agent Commerce API from Hilt — 4 operation(s) for agent commerce.
- [Hilt API Keys API](https://apis.io/apis/hilt-so/hilt-so-api-keys-api/) — The api-keys API from Hilt — 2 operation(s) for api-keys.
- [Hilt Auth API](https://apis.io/apis/hilt-so/hilt-so-auth-api/) — The auth API from Hilt — 8 operation(s) for auth.
- [Hilt Billing API](https://apis.io/apis/hilt-so/hilt-so-billing-api/) — The billing API from Hilt — 5 operation(s) for billing.
- [Hilt Checkout API](https://apis.io/apis/hilt-so/hilt-so-checkout-api/) — The checkout API from Hilt — 12 operation(s) for checkout.
- [Hilt Checkout Domains API](https://apis.io/apis/hilt-so/hilt-so-checkout-domains-api/) — The checkout-domains API from Hilt — 1 operation(s) for checkout-domains.
- [Hilt Hilt Pay API](https://apis.io/apis/hilt-so/hilt-so-hilt-pay-api-api/) — The Hilt Pay API API from Hilt — 39 operation(s) for hilt pay api.
- [Hilt Hilt PayMe Connector API](https://apis.io/apis/hilt-so/hilt-so-hilt-payme-connector-api/) — The Hilt PayMe Connector API from Hilt — 6 operation(s) for hilt payme connector.
- [Hilt Integrations API](https://apis.io/apis/hilt-so/hilt-so-integrations-api/) — The integrations API from Hilt — 4 operation(s) for integrations.
- [Hilt Memberships API](https://apis.io/apis/hilt-so/hilt-so-memberships-api/) — The memberships API from Hilt — 11 operation(s) for memberships.
- [Hilt Pay Me API](https://apis.io/apis/hilt-so/hilt-so-pay-me-api/) — The pay-me API from Hilt — 21 operation(s) for pay-me.
- [Hilt Products API](https://apis.io/apis/hilt-so/hilt-so-products-api/) — The products API from Hilt — 9 operation(s) for products.
- [Hilt Receipt API](https://apis.io/apis/hilt-so/hilt-so-receipt-api/) — The Receipt API from Hilt — 10 operation(s) for receipt.
- [Hilt Solana API](https://apis.io/apis/hilt-so/hilt-so-solana-api/) — The Solana API from Hilt — 1 operation(s) for solana.
- [Hilt Support API](https://apis.io/apis/hilt-so/hilt-so-support-api/) — The Support API from Hilt — 3 operation(s) for support.
- [Hilt System API](https://apis.io/apis/hilt-so/hilt-so-system-api/) — The system API from Hilt — 2 operation(s) for system.
- [Hilt Testing API](https://apis.io/apis/hilt-so/hilt-so-testing-api/) — The testing API from Hilt — 3 operation(s) for testing.
- [Hilt Webhooks API](https://apis.io/apis/hilt-so/hilt-so-webhooks-api/) — The webhooks API from Hilt — 7 operation(s) for webhooks.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Hilt Webhooks](https://apis.io/asyncapis/hilt-so/hilt-so-webhooks-asyncapi/)

#### Event channels (10)

Individual events and webhooks the provider emits.

- [delivery.failed](https://apis.io/channels/hilt-so/delivery-failed/)
- [membership.activated](https://apis.io/channels/hilt-so/membership-activated/)
- [membership.entered_grace](https://apis.io/channels/hilt-so/membership-entered-grace/)
- [membership.expired](https://apis.io/channels/hilt-so/membership-expired/)
- [membership.reapproval_required](https://apis.io/channels/hilt-so/membership-reapproval-required/)
- [membership.renewed](https://apis.io/channels/hilt-so/membership-renewed/)
- [payment.confirmed](https://apis.io/channels/hilt-so/payment-confirmed/)
- [payment.failed](https://apis.io/channels/hilt-so/payment-failed/)
- [receipt.created](https://apis.io/channels/hilt-so/receipt-created/)
- [support.ticket.created](https://apis.io/channels/hilt-so/support-ticket-created/)

#### MCP servers (2)

Model Context Protocol servers that expose the API to agents.

- [Hilt Pay Agent Gateway](https://apis.io/servers/hilt-so/hilt-pay-agent-gateway/)
- [Hilt PayMe](https://apis.io/servers/hilt-so/hilt-payme/)

#### Overlays (20)

OpenAPI overlays, including conversational phrasing for each operation.

- [Hilt So Account Api Phrasing Overlay](https://apis.io/overlays/hilt-so/hilt-so-account-api-phrasing-overlay/)
- [Hilt So Agent Commerce Api Phrasing Overlay](https://apis.io/overlays/hilt-so/hilt-so-agent-commerce-api-phrasing-overlay/)
- [Hilt So Api Keys Api Phrasing Overlay](https://apis.io/overlays/hilt-so/hilt-so-api-keys-api-phrasing-overlay/)
- [Hilt So Auth Api Phrasing Overlay](https://apis.io/overlays/hilt-so/hilt-so-auth-api-phrasing-overlay/)
- [Hilt So Billing Api Phrasing Overlay](https://apis.io/overlays/hilt-so/hilt-so-billing-api-phrasing-overlay/)
- [Hilt So Checkout Api Phrasing Overlay](https://apis.io/overlays/hilt-so/hilt-so-checkout-api-phrasing-overlay/)
- [Hilt So Checkout Domains Api Phrasing Overlay](https://apis.io/overlays/hilt-so/hilt-so-checkout-domains-api-phrasing-overlay/)
- [Hilt So Hilt Pay Api Api Phrasing Overlay](https://apis.io/overlays/hilt-so/hilt-so-hilt-pay-api-api-phrasing-overlay/)
- [Hilt So Hilt Payme Connector Api Phrasing Overlay](https://apis.io/overlays/hilt-so/hilt-so-hilt-payme-connector-api-phrasing-overlay/)
- [Hilt So Integrations Api Phrasing Overlay](https://apis.io/overlays/hilt-so/hilt-so-integrations-api-phrasing-overlay/)
- [Hilt So Memberships Api Phrasing Overlay](https://apis.io/overlays/hilt-so/hilt-so-memberships-api-phrasing-overlay/)
- [Hilt So Openapi Overlay](https://apis.io/overlays/hilt-so/hilt-so-openapi-overlay/)
- [Hilt So Pay Me Api Phrasing Overlay](https://apis.io/overlays/hilt-so/hilt-so-pay-me-api-phrasing-overlay/)
- [Hilt So Products Api Phrasing Overlay](https://apis.io/overlays/hilt-so/hilt-so-products-api-phrasing-overlay/)
- [Hilt So Receipt Api Phrasing Overlay](https://apis.io/overlays/hilt-so/hilt-so-receipt-api-phrasing-overlay/)
- [Hilt So Solana Api Phrasing Overlay](https://apis.io/overlays/hilt-so/hilt-so-solana-api-phrasing-overlay/)
- [Hilt So Support Api Phrasing Overlay](https://apis.io/overlays/hilt-so/hilt-so-support-api-phrasing-overlay/)
- [Hilt So System Api Phrasing Overlay](https://apis.io/overlays/hilt-so/hilt-so-system-api-phrasing-overlay/)
- [Hilt So Testing Api Phrasing Overlay](https://apis.io/overlays/hilt-so/hilt-so-testing-api-phrasing-overlay/)
- [Hilt So Webhooks Api Phrasing Overlay](https://apis.io/overlays/hilt-so/hilt-so-webhooks-api-phrasing-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Hilt So Authentication](https://apis.io/security/hilt-so/hilt-so-authentication/)
- [Hilt So Domain Security](https://apis.io/security/hilt-so/hilt-so-domain-security/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Hilt So Scopes](https://apis.io/scopes/hilt-so/hilt-so-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Hilt So Plans Pricing](https://apis.io/plans/hilt-so/hilt-so-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Hilt So Rate Limits](https://apis.io/rate-limits/hilt-so/hilt-so-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.hilt.so/)
- [Documentation](https://docs.hilt.so/developers)
- [Getting started](https://docs.hilt.so/developers/quickstart)
- [API reference](https://api.hilt.so/v1/docs)
- [Pricing](https://www.hilt.so/developers/pricing)
- [Sign up](https://app.hilt.so/register)
- [Support](https://docs.hilt.so/merchant/support)
- [Changelog](https://www.hilt.so/updates)
- [Blog](https://www.hilt.so/articles)
- [Terms of service](https://www.hilt.so/legal/terms)
- [Privacy policy](https://www.hilt.so/legal/privacy)
- [GitHub](https://github.com/Hiltpay)
- [Status](https://www.hilt.so/status)

## API Evangelist rating

**Kin Score 72.4** — exemplar · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 52.6 |
| Contract governance | 18.2 |
| Operational transparency | 65.8 |
| Developer ergonomics | 90.5 |
| Access clarity | 76.3 |

**Agent readiness 61.8** — agent-native

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | verified |
| MCP Server | documented (partial credit) |
| Auth Clarity | served (partial credit) |
| Idempotency | verified |
| Error Semantics | verified |
| OpenAPI Examples | partial |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | derived (partial credit) |
| Agent Skills | yes |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | yes |
| Agentic Commerce | — |
| Pagination Ratio | partial |
| Operation Distinctiveness | distinct |

**Regulatory alignment 34.8** — Payments

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/hilt-so/](https://apis.io/providers/hilt-so/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Hilt: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/hilt-so/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
