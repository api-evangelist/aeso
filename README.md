# AESO (aeso)

The Alberta Electric System Operator (AESO) is the independent, not-for-profit system and market operator for Alberta's electricity system — a statutory Crown corporation created under Alberta's Electric Utilities Act that dispatches generation and operates the Alberta Interconnected Electric System twenty-four hours a day for roughly five million Albertans, plans the transmission system, administers grid connections, and runs Alberta's energy-only wholesale market including price settlement and market rules. It sits in the middle of the value chain: it does not own generation, wires or retail customers, it clears the pool, publishes the Pool Price, and holds the market-wide operational data every generator, retailer and trader in Alberta depends on.

Its API posture is the opposite of a compliance story. **No energy-data mandate applies to AESO at all.** Alberta has no Consumer Data Right, no Green Button regulation (that is Ontario's, by regulation, and Nova Scotia's), and no consumer energy-data obligation of any kind — and AESO, as a system operator, holds no retail customer usage or billing data to be obliged over. What it publishes, it publishes voluntarily.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/aeso/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/aeso/refs/heads/main/apis.yml)

## Tags

- Energy
- Canada
- Alberta
- Electricity
- Energy Markets
- Grid
- System Operator
- Market Operator
- Open Energy Data
- Wholesale Power
- Demand Response
- Renewables
- Utilities

## Timestamps

- **Created:** 2026-07-27
- **Modified:** 2026-07-27

## Access

| | |
|---|---|
| **Mandate regime** | none |
| **Mandate status** | not-applicable — AESO is structurally not a consumer data holder |
| **Data standard** | no standard reference found (proprietary JSON; OpenAPI 3.0.1 contracts) |
| **Consumer data API** | No |
| **Market data open** | Yes |
| **Access gate** | Self-serve |
| **Auth model** | API key — `API-KEY` request header, or `subscription-key` query parameter |
| **Home market** | Canada |

Two layers. The **Energy Trading System** report servlets at `ets.aeso.ca` are completely anonymous — add `contentType=csv` to a plain HTTP GET and real market CSV comes back, with no key, no account, no login and no licence click-through. The **fourteen JSON APIs** on the Azure API Management gateway need a key, but that key is free and self-serve: sign up at the developer portal with any email, confirm it, subscribe to the single "AESO Public API" product, and primary and secondary keys are generated immediately. The portal's own product metadata reports `approvalRequired: false`. The real constraint is legal, not technical — AESO's site terms permit non-commercial, personal or educational use only, and anything else needs written permission.

## APIs

### AESO Pool Price Report API

The hourly Alberta Pool Price — the settlement price of the province's energy-only wholesale electricity market — served as JSON for any date range back to 2000-01-01, up to one year per request. Returns UTC and Mountain Prevailing Time timestamps, pool price in CAD, forecast pool price, and the thirty-day rolling average.

- **Human URL:** [https://developer-apim.aeso.ca/api-details#api=poolprice-api-v1-1](https://developer-apim.aeso.ca/api-details#api=poolprice-api-v1-1)
- **Base URL:** `https://apimgw.aeso.ca/public/poolprice-api/v1.1`
- **Properties:** [OpenAPI](openapi/aeso-poolprice-api-v1-1-openapi.json)

### AESO System Marginal Price Report API

The System Marginal Price — the real-time signal that sets the pool price over each settlement hour — as both a historical date-range report and a current-value endpoint.

- **Human URL:** [https://developer-apim.aeso.ca/api-details#api=systemmarginalprice-api-v1-1](https://developer-apim.aeso.ca/api-details#api=systemmarginalprice-api-v1-1)
- **Base URL:** `https://apimgw.aeso.ca/public/systemmarginalprice-api/v1.1`
- **Properties:** [OpenAPI](openapi/aeso-systemmarginalprice-api-v1-1-openapi.json)

### AESO Current Supply Demand API (v2)

The current summary of Alberta's supply and demand balance — total net generation, net actual interchange, Alberta Internal Load, contingency reserve, and the generation mix by fuel type.

- **Human URL:** [https://developer-apim.aeso.ca/api-details#api=currentsupplydemand-api-v2](https://developer-apim.aeso.ca/api-details#api=currentsupplydemand-api-v2)
- **Base URL:** `https://apimgw.aeso.ca/public/currentsupplydemand-api/v2`
- **Properties:** [OpenAPI](openapi/aeso-currentsupplydemand-api-v2-openapi.json)

### AESO Current Supply Demand API (v1)

The per-asset view of current generation — the generating assets currently online in Alberta with their current output.

- **Human URL:** [https://developer-apim.aeso.ca/api-details#api=currentsupplydemand-api-v1](https://developer-apim.aeso.ca/api-details#api=currentsupplydemand-api-v1)
- **Base URL:** `https://apimgw.aeso.ca/public/currentsupplydemand-api/v1`
- **Properties:** [OpenAPI](openapi/aeso-currentsupplydemand-api-v1-openapi.json)

### AESO Actual Forecast Report API

Actual and forecast Alberta Internal Load for a requested date range — the demand series behind every load forecast, price forecast and adequacy study in the Alberta market.

- **Human URL:** [https://developer-apim.aeso.ca/api-details#api=actualforecast-api-v1](https://developer-apim.aeso.ca/api-details#api=actualforecast-api-v1)
- **Base URL:** `https://apimgw.aeso.ca/public/actualforecast-api/v1`
- **Properties:** [OpenAPI](openapi/aeso-actualforecast-api-v1-openapi.json)

### AESO AIES Gen Capacity API

Generation capacity and generator outages on the Alberta Interconnected Electric System as submitted to the AESO.

- **Human URL:** [https://developer-apim.aeso.ca/api-details#api=aiesgencapacity-api-v1](https://developer-apim.aeso.ca/api-details#api=aiesgencapacity-api-v1)
- **Base URL:** `https://apimgw.aeso.ca/public/aiesgencapacity-api/v1`
- **Properties:** [OpenAPI](openapi/aeso-aiesgencapacity-api-v1-openapi.json)

### AESO Load Outage Forecast API

Load outages submitted to the AESO — the demand-side counterpart to the generation outage feed.

- **Human URL:** [https://developer-apim.aeso.ca/api-details#api=loadoutageforecast-api-v1](https://developer-apim.aeso.ca/api-details#api=loadoutageforecast-api-v1)
- **Base URL:** `https://apimgw.aeso.ca/public/loadoutageforecast-api/v1`
- **Properties:** [OpenAPI](openapi/aeso-loadoutageforecast-api-v1-openapi.json)

### AESO Intertie Public Reports API

Alberta's interties with British Columbia, Saskatchewan and Montana — interchange capability and flow, plus intertie outages.

- **Human URL:** [https://developer-apim.aeso.ca/api-details#api=itc-api-v1](https://developer-apim.aeso.ca/api-details#api=itc-api-v1)
- **Base URL:** `https://apimgw.aeso.ca/public/itc/v1`
- **Properties:** [OpenAPI](openapi/aeso-itc-api-v1-openapi.json)

### AESO Energy Merit Order Report API

A snapshot of the energy merit order — the stacked offers that determine which generation is dispatched and where the price clears.

- **Human URL:** [https://developer-apim.aeso.ca/api-details#api=energymeritorder-api-v1](https://developer-apim.aeso.ca/api-details#api=energymeritorder-api-v1)
- **Base URL:** `https://apimgw.aeso.ca/public/energymeritorder-api/v1`
- **Properties:** [OpenAPI](openapi/aeso-energymeritorder-api-v1-openapi.json)

### AESO Metered Volume Report API

Metered volume detail for the Alberta Interconnected Electric System — settlement-grade metering at market-asset granularity, not retail customer metering.

- **Human URL:** [https://developer-apim.aeso.ca/api-details#api=meteredvolume-api-v1](https://developer-apim.aeso.ca/api-details#api=meteredvolume-api-v1)
- **Base URL:** `https://apimgw.aeso.ca/public/meteredvolume-api/v1`
- **Properties:** [OpenAPI](openapi/aeso-meteredvolume-api-v1-openapi.json)

### AESO Operating Reserve Offer Control Report API

Operating reserve offer control data — who controls the offers for Alberta's ancillary-services reserve products.

- **Human URL:** [https://developer-apim.aeso.ca/api-details#api=operatingreserveoffercontrol-api-v1](https://developer-apim.aeso.ca/api-details#api=operatingreserveoffercontrol-api-v1)
- **Base URL:** `https://apimgw.aeso.ca/public/operatingreserveoffercontrol-api/v1`
- **Properties:** [OpenAPI](openapi/aeso-operatingreserveoffercontrol-api-v1-openapi.json)

### AESO Asset List API

The registry of market assets on the Alberta Interconnected Electric System — the reference data that gives every asset ID in every other AESO feed a name, type and pool participant.

- **Human URL:** [https://developer-apim.aeso.ca/api-details#api=assetlist-api-v1](https://developer-apim.aeso.ca/api-details#api=assetlist-api-v1)
- **Base URL:** `https://apimgw.aeso.ca/public/assetlist-api/v1`
- **Properties:** [OpenAPI](openapi/aeso-assetlist-api-v1-openapi.json)

### AESO Pool Participant API

The latest list of pool participants operating in the Alberta Interconnected Electric System.

- **Human URL:** [https://developer-apim.aeso.ca/api-details#api=poolparticipant-api-v1](https://developer-apim.aeso.ca/api-details#api=poolparticipant-api-v1)
- **Base URL:** `https://apimgw.aeso.ca/public/PoolParticipant-api/v1`
- **Properties:** [OpenAPI](openapi/aeso-poolparticipant-api-v1-openapi.json)

### AESO Unit Commitment Data API

Unit commitment directives issued by the AESO — the instructions that bring generating units online ahead of dispatch.

- **Human URL:** [https://developer-apim.aeso.ca/api-details#api=unitcommitmentdata-api-v2](https://developer-apim.aeso.ca/api-details#api=unitcommitmentdata-api-v2)
- **Base URL:** `https://apimgw.aeso.ca/public/unitcommitmentdata-api/v2`
- **Properties:** [OpenAPI](openapi/aeso-unitcommitmentdata-api-v2-openapi.json)

### AESO Energy Trading System (ETS) Public Reports

The fully anonymous half of AESO's data posture. Each report is a plain HTTP GET that accepts `contentType=csv` and returns machine-readable CSV with no key, no account, no login and no licence click-through. Confirmed live and anonymous on 2026-07-27 across Current Supply Demand, System Marginal Price, Daily Average Pool Price, Supply Surplus, Real Time Shift, Actual Forecast and Historical Pool Price. There is no OpenAPI, no schema and no formal reference for this surface — AESO documents the report URLs and nothing more — so it is recorded as a verified public data surface rather than a specified API.

- **Human URL:** [https://www.aeso.ca/market/market-and-system-reporting/](https://www.aeso.ca/market/market-and-system-reporting/)
- **Base URL:** `http://ets.aeso.ca/ets_web/ip/Market/Reports`

## Common Properties

- [Website](https://www.aeso.ca/)
- [Developer Portal](https://developer-apim.aeso.ca/)
- [Documentation](https://www.aeso.ca/market/market-and-system-reporting/aeso-application-programming-interface-api/)
- [Onboarding — APIM API Gateway Instructions (PDF)](https://www.aeso.ca/assets/downloads/external/api/API-Access-Instructions-APIM-API-Gateway.pdf)
- [Sign Up](https://developer-apim.aeso.ca/signup)
- [Sign In](https://developer-apim.aeso.ca/signin)
- [Products / Plans](https://developer-apim.aeso.ca/products)
- [Terms of Service](https://www.aeso.ca/legal)
- [Newsroom](https://www.aeso.ca/aeso/newsroom/)
- [LinkedIn](https://www.linkedin.com/company/25743)
- [Twitter](https://twitter.com/theaeso)

## Notes on the harvested OpenAPI documents

AESO's own OpenAPI export endpoint returns a syntactically valid OpenAPI 3.0.1 document whose `paths` object is **empty** — it carries only `info`, `servers` and `securitySchemes`. Rather than save fourteen empty shells, each document under `openapi/` was assembled verbatim from AESO's own anonymously served Azure API Management developer-portal metadata: `info`, `servers` and `securitySchemes` from the OpenAPI export; paths, methods, operation IDs, descriptions, parameters, response codes and response examples from the portal's operations endpoints; and `components.schemas` from the portal's schema documents. Nothing was invented or paraphrased. Every file carries an `x-provenance` block listing every source URL fetched, with the fetch date.

Also worth recording: the legacy documented host `api.aeso.ca` — still cited in third-party writeups as the AESO API documentation home — no longer resolves. It is a CNAME to `api.gtm.aeso.ca`, which returns SERVFAIL. The live surface is `developer-apim.aeso.ca` for documentation and `apimgw.aeso.ca` / `gateway-apim.aeso.ca` for traffic.

## Maintainers

- Kin Lane — kin@apievangelist.com
