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

- Website: https://www.hilt.so/
- Docs: https://docs.hilt.so/developers
- OpenAPI: https://api.hilt.so/openapi.json (saved at openapi/hilt-so-openapi.yml)
- MCP gateway: https://api.hilt.so/mcp · PayMe MCP connector: https://api.hilt.so/mcp/pay-me
- A2A agent card: https://api.hilt.so/.well-known/agent-card.json
- llms.txt: https://www.hilt.so/llms.txt

Enriched 2026-09-19 (local pass). Artifacts under openapi/, mcp/, a2a/, well-known/, llms/, skills/, conventions/, errors/, lifecycle/, authentication/, scopes/, conformance/, sandbox/, packages/, cli/, components/, changelog/, plans/, rate-limits/, asyncapi/, data-model/, overlays/, regulatory/, security/, postman/.
