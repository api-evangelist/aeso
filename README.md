# AESO

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

The Alberta Electric System Operator (AESO) is the independent, not-for-profit system and market operator for Alberta's electricity system — a statutory body created under Alberta's Electric Utilities Act that dispatches generation and operates the Alberta Interconnected Electric System twenty-four hours a day for roughly five million Albertans, plans the transmission system, administers grid connections, and runs Alberta's energy-only wholesale market including price settlement and market rules. It sits in the middle of the value chain: it does not own generation, wires or retail customers, it clears the pool, publishes the Pool Price, and holds the market-wide operational data every generator, retailer and trader in Alberta depends on. Its API posture is unusually clean for the sector and is the exact opposite of a compliance story — there is no mandate on AESO at all. Alberta has no Consumer Data Right, no Green Button regulation (that is Ontario's, by regulation, and Nova Scotia's), and no consumer energy-data obligation of any kind, and AESO holds no retail customer usage or billing data, so the consumer-data half of this sector simply does not exist here. What AESO publishes voluntarily is a genuinely open market-data surface in two layers: the legacy Energy Trading System report servlets at ets.aeso.ca, which return real CSV and HTML market reports — current supply and demand, pool price, system marginal price, daily averages, outages — anonymously with no key, no account and no licence click-through; and a modern Azure API Management gateway at apimgw.aeso.ca fronting fourteen documented JSON APIs whose full reference, operations, schemas and OpenAPI export can be read anonymously from the public developer portal, and whose keys are issued self-serve — email confirmation, subscribe to the single "AESO Public API" product, keys generated instantly, no approval step. Authentication is a single API-KEY request header (or a subscription-key query parameter). The one real friction is legal rather than technical: AESO's site terms permit non-commercial, personal or educational use only, and any other use requires written permission.

**Areas:** Energy · Canada · Alberta · Electricity · Energy Markets · Grid · System Operator · Market Operator · Open Energy Data · Wholesale Power · Demand Response · Renewables

## AESO on APIs.io

Everything profiled for AESO is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/aeso/](https://apis.io/providers/aeso/)** — or go straight to one of the APIs or properties below.

### APIs (14)

- [AESO Energy Trading System (ETS) Public Reports](https://apis.io/apis/aeso/aeso-ets-public-reports/) — AESO's long-running Energy Trading System report servlets — the fully anonymous half of its data posture, and the reason market_data_open is true for AESO…
- [AESO AIES Gen Capacity API](https://apis.io/apis/aeso/aeso-aiesgencapacity-api/) — The AIESGenCapacity API from AESO — 1 operation(s) for aiesgencapacity.
- [AESO Csd API](https://apis.io/apis/aeso/aeso-csd-api/) — The Csd API from AESO — 2 operation(s) for csd.
- [AESO Interchange API](https://apis.io/apis/aeso/aeso-interchange-api/) — The Interchange API from AESO — 1 operation(s) for interchange.
- [AESO Load API](https://apis.io/apis/aeso/aeso-load-api/) — The Load API from AESO — 1 operation(s) for load.
- [AESO Load Outage Report API](https://apis.io/apis/aeso/aeso-loadoutagereport-api/) — The LoadOutageReport API from AESO — 1 operation(s) for loadoutagereport.
- [AESO Merit Order API](https://apis.io/apis/aeso/aeso-meritorder-api/) — The MeritOrder API from AESO — 1 operation(s) for meritorder.
- [AESO Meteredvolume API](https://apis.io/apis/aeso/aeso-meteredvolume-api/) — The Meteredvolume API from AESO — 1 operation(s) for meteredvolume.
- [AESO Operating Reserve Offer Control API](https://apis.io/apis/aeso/aeso-operatingreserveoffercontrol-api/) — The OperatingReserveOfferControl API from AESO — 1 operation(s) for operatingreserveoffercontrol.
- [AESO Outage API](https://apis.io/apis/aeso/aeso-outage-api/) — The Outage API from AESO — 1 operation(s) for outage.
- [AESO Poolparticipantlist API](https://apis.io/apis/aeso/aeso-poolparticipantlist-api/) — The Poolparticipantlist API from AESO — 1 operation(s) for poolparticipantlist.
- [AESO Price API](https://apis.io/apis/aeso/aeso-price-api/) — The Price API from AESO — 3 operation(s) for price.
- [AESO Unit Commitment API](https://apis.io/apis/aeso/aeso-unitcommitment-api/) — The UnitCommitment API from AESO — 1 operation(s) for unitcommitment.
- [AESO Asset List API](https://apis.io/apis/aeso/aeso-asset-list-api/) — The Asset List API from AESO — 1 operation(s) for asset list.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### Arazzo workflows (3)

Multi-step workflows that chain operations into a business task.

- [AESO asset drilldown](https://apis.io/arazzos/aeso/aeso-asset-drilldown/)
- [AESO live market snapshot](https://apis.io/arazzos/aeso/aeso-market-snapshot/)
- [AESO price formation trace](https://apis.io/arazzos/aeso/aeso-price-formation/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [aeso-mcp.yml](https://apis.io/servers/aeso/aeso-mcp-yml/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Aeso Agentic Access](https://apis.io/agentic-access/aeso/aeso-agentic-access/)

#### Collections (14)

Postman and Open Collection request collections.

- [Actual Forecast Report](https://apis.io/collections/aeso/open-aeso-actualforecast-api-v1/)
- [AIES Gen Capacity API](https://apis.io/collections/aeso/open-aeso-aiesgencapacity-api-v1/)
- [Asset List API](https://apis.io/collections/aeso/open-aeso-assetlist-api-v1/)
- [Current Supply Demand](https://apis.io/collections/aeso/open-aeso-currentsupplydemand-api-v1/)
- [Current Supply Demand](https://apis.io/collections/aeso/open-aeso-currentsupplydemand-api-v2/)
- [Energy Merit Order Report](https://apis.io/collections/aeso/open-aeso-energymeritorder-api-v1/)
- [Intertie Public Reports](https://apis.io/collections/aeso/open-aeso-itc-api-v1/)
- [Load Outage Forecast API](https://apis.io/collections/aeso/open-aeso-loadoutageforecast-api-v1/)
- [Metered Volume Report](https://apis.io/collections/aeso/open-aeso-meteredvolume-api-v1/)
- [Operating Reserve Offer Control Report](https://apis.io/collections/aeso/open-aeso-operatingreserveoffercontrol-api-v1/)
- [Pool Participant API](https://apis.io/collections/aeso/open-aeso-poolparticipant-api-v1/)
- [Pool Price Report](https://apis.io/collections/aeso/open-aeso-poolprice-api-v1-1/)
- [System Marginal Price Report](https://apis.io/collections/aeso/open-aeso-systemmarginalprice-api-v1-1/)
- [Unit Commitment Data API](https://apis.io/collections/aeso/open-aeso-unitcommitmentdata-api-v2/)

#### Overlays (14)

OpenAPI overlays, including conversational phrasing for each operation.

- [Aeso Actualforecast Api V1 Overlay](https://apis.io/overlays/aeso/aeso-actualforecast-api-v1-overlay/)
- [Aeso Aiesgencapacity Api V1 Overlay](https://apis.io/overlays/aeso/aeso-aiesgencapacity-api-v1-overlay/)
- [Aeso Assetlist Api V1 Overlay](https://apis.io/overlays/aeso/aeso-assetlist-api-v1-overlay/)
- [Aeso Currentsupplydemand Api V1 Overlay](https://apis.io/overlays/aeso/aeso-currentsupplydemand-api-v1-overlay/)
- [Aeso Currentsupplydemand Api V2 Overlay](https://apis.io/overlays/aeso/aeso-currentsupplydemand-api-v2-overlay/)
- [Aeso Energymeritorder Api V1 Overlay](https://apis.io/overlays/aeso/aeso-energymeritorder-api-v1-overlay/)
- [Aeso Itc Api V1 Overlay](https://apis.io/overlays/aeso/aeso-itc-api-v1-overlay/)
- [Aeso Loadoutageforecast Api V1 Overlay](https://apis.io/overlays/aeso/aeso-loadoutageforecast-api-v1-overlay/)
- [Aeso Meteredvolume Api V1 Overlay](https://apis.io/overlays/aeso/aeso-meteredvolume-api-v1-overlay/)
- [Aeso Operatingreserveoffercontrol Api V1 Overlay](https://apis.io/overlays/aeso/aeso-operatingreserveoffercontrol-api-v1-overlay/)
- [Aeso Poolparticipant Api V1 Overlay](https://apis.io/overlays/aeso/aeso-poolparticipant-api-v1-overlay/)
- [Aeso Poolprice Api V1 1 Overlay](https://apis.io/overlays/aeso/aeso-poolprice-api-v1-1-overlay/)
- [Aeso Systemmarginalprice Api V1 1 Overlay](https://apis.io/overlays/aeso/aeso-systemmarginalprice-api-v1-1-overlay/)
- [Aeso Unitcommitmentdata Api V2 Overlay](https://apis.io/overlays/aeso/aeso-unitcommitmentdata-api-v2-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Aeso Authentication](https://apis.io/security/aeso/aeso-authentication/)
- [Aeso Domain Security](https://apis.io/security/aeso/aeso-domain-security/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Aeso Plans](https://apis.io/plans/aeso/aeso-plans/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.aeso.ca/)
- [Documentation](https://www.aeso.ca/market/market-and-system-reporting/aeso-application-programming-interface-api/)
- [Getting started](https://www.aeso.ca/assets/downloads/external/api/API-Access-Instructions-APIM-API-Gateway.pdf)
- [API reference](https://developer-apim.aeso.ca/apis)
- [Pricing](https://developer-apim.aeso.ca/developer/products?api-version=2022-04-01-preview)
- [Sign up](https://developer-apim.aeso.ca/signup)
- [Blog](https://www.aeso.ca/aeso/newsroom/)
- [Terms of service](https://www.aeso.ca/legal/)
- [Privacy policy](https://www.aeso.ca/privacy/)

## API Evangelist rating

**Kin Score 43.0** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 78.6 |
| Contract quality | 16.3 |
| Contract governance | 4.5 |
| Operational transparency | 15.8 |
| Developer ergonomics | 66.1 |
| Access clarity | 65.8 |

**Agent readiness 28.3** — agent-aware

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | na |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | na |
| Error Semantics | derived (partial credit) |
| OpenAPI Examples | verified |
| Rate Limit Signal | — |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | na |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | distinct |

**Regulatory alignment 27.0** — Energy & Utilities

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/aeso/](https://apis.io/providers/aeso/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for AESO: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/aeso/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
