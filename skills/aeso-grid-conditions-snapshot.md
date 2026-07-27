---
name: aeso-grid-conditions-snapshot
description: Build a live picture of Alberta's grid from AESO — supply and demand balance, generation mix by fuel, per-asset output, load forecast, and the generation and load outages behind it.
api: openapi/aeso-currentsupplydemand-api-v2-openapi.json, openapi/aeso-currentsupplydemand-api-v1-openapi.json, openapi/aeso-actualforecast-api-v1-openapi.json, openapi/aeso-aiesgencapacity-api-v1-openapi.json, openapi/aeso-loadoutageforecast-api-v1-openapi.json
operations:
  - getCSDSummaryDataReportv2
  - getCSDReportByAsset
  - getActualForecastReport
  - getAIESControlReport
  - getLoadOutageRangeReport
generated: '2026-07-27'
method: generated
source: openapi/*.json + conventions/aeso-conventions.yml + lifecycle/aeso-lifecycle.yml
---

# AESO grid conditions snapshot

Five operations, in order, take you from "what is the grid doing right now" to "why".

## Before you start

Authenticate with the `API-KEY` header (see `skills/aeso-market-price-analysis.md` for the sign-up
flow). All operations are `GET` and safe to retry.

## Step 1 — The headline balance

Operation `getCSDSummaryDataReportv2` — `GET /csd/summary/current` on
`https://apimgw.aeso.ca/public/currentsupplydemand-api/v2`. **No parameters.**

This is the JSON equivalent of the long-running ETS Current Supply Demand report: Alberta Total Net
Generation, Net Actual Interchange, Alberta Internal Load, contingency reserve, and the generation
mix broken out by fuel type.

> Version note: this is **v2**. The v1 *summary* endpoint was retired on 2025-09-30, and v2 changed
> the labelling of the `last_updated_datetime` field. Do not code against v1 summary.

## Step 2 — Break the mix down to individual assets

Operation `getCSDReportByAsset` — `GET /csd/generation/assets/current` on
`https://apimgw.aeso.ca/public/currentsupplydemand-api/v1` (this per-asset endpoint is still on v1).

| Parameter | In | Required | Notes |
|---|---|---|---|
| `assetIds` | query | no | narrow to specific assets; omit for every reporting asset |

Asset identifiers come from the Asset List API — see
`skills/aeso-asset-and-participant-reference.md`. Without that join, an asset ID is an opaque code.

## Step 3 — Put demand in context

Operation `getActualForecastReport` — `GET /load/albertaInternalLoad` on
`https://apimgw.aeso.ca/public/actualforecast-api/v1`.

| Parameter | In | Required | Notes |
|---|---|---|---|
| `startDate` | query | yes | `yyyy-MM-dd` |
| `endDate` | query | no | `yyyy-MM-dd`, after `startDate` |

Actual and forecast Alberta Internal Load. Compare the current AIL from step 1 against the forecast
series to see whether demand is running hot or cold against expectation.

## Step 4 — Supply-side outages

Operation `getAIESControlReport` — `GET /AIESGenCapacity` on
`https://apimgw.aeso.ca/public/aiesgencapacity-api/v1`. Takes `startDate` (required) and `endDate`
(optional), same `yyyy-MM-dd` format.

Generation capacity and generator outages submitted to AESO. This is what explains a tight supply
cushion.

> Field note: Coal and Dual Fuel fuel types were removed from this API on 2024-11-18 and Gas was
> split into subtypes on the CSD Summary API at the same time. Older client code that switches on
> `Coal` will silently never match.

## Step 5 — Demand-side outages

Operation `getLoadOutageRangeReport` — `GET /loadOutageReport` on
`https://apimgw.aeso.ca/public/loadoutageforecast-api/v1`. Takes `startDate` (required) and
`endDate` (optional).

Load outages submitted to AESO — the demand-side counterpart to step 4, used to model expected load
reductions.

## Rules that apply to every call

- Numeric fields (megawatts, prices) are JSON **strings**. Parse them.
- Timestamps arrive in both UTC and Mountain Prevailing Time on time-series reports.
- There is no pagination anywhere; range reports are bounded by documented date-range caps.
- `/current` operations are the only live surface — do not poll a range report with today's date to
  simulate one.
- Errors use the Azure APIM `{"statusCode", "message"}` envelope, not `application/problem+json`.
- No rate limits are published and no rate-limit headers are returned. Poll the `/current` endpoints
  no faster than the underlying report refreshes (minutes, not seconds), and back off on `503`.

## Anonymous fallback

`http://ets.aeso.ca/ets_web/ip/Market/Reports/CSDReportServlet` returns the same Current Supply
Demand report as CSV with no key at all.
