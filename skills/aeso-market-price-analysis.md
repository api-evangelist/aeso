---
name: aeso-market-price-analysis
description: Pull Alberta wholesale electricity prices from AESO — hourly Pool Price with forecast and 30-day rolling average, and the System Marginal Price that sets it, both historically and live.
api: openapi/aeso-poolprice-api-v1-1-openapi.json, openapi/aeso-systemmarginalprice-api-v1-1-openapi.json
operations:
  - getPoolPriceDateRangeReport
  - getSystemMarginalPriceReportForDateRange
  - getCurrentSystemMarginalPriceReport
generated: '2026-07-27'
method: generated
source: openapi/*.json + conventions/aeso-conventions.yml + errors/aeso-problem-types.yml
---

# AESO market price analysis

Alberta runs an energy-only wholesale market. Two prices matter and AESO publishes both.

- **System Marginal Price (SMP)** is the real-time price, changing as dispatch changes within the hour.
- **Pool Price** is the settlement price for the hour — the time-weighted average of the SMP over that
  settlement hour. It is what generators are paid and what load pays.

## Before you start

- Get a key: sign up at <https://developer-apim.aeso.ca/signup>, confirm the email, subscribe to the
  **AESO Public API** product on the Products page. Keys appear instantly on your Profile page. No
  approval step.
- Send the key on every request as the `API-KEY` header. (A `subscription-key` query parameter also
  works but puts the key in logs and referrers — prefer the header.)
- Every operation is a `GET`. There are no writes, so every call is safe to retry.
- Read AESO's terms first: <https://www.aeso.ca/legal/> permits non-commercial, personal or
  educational use only. Anything else needs AESO's written permission.

## Step 1 — Pull the hourly Pool Price for a date range

Operation `getPoolPriceDateRangeReport` — `GET /price/poolPrice` on
`https://apimgw.aeso.ca/public/poolprice-api/v1.1`.

| Parameter | In | Required | Notes |
|---|---|---|---|
| `startDate` | query | yes | `yyyy-MM-dd`, any date from `2000-01-01` to today |
| `endDate` | query | no | `yyyy-MM-dd`, after `startDate`. Omit it and you get only `startDate`'s completed settlement hours |

```
GET https://apimgw.aeso.ca/public/poolprice-api/v1.1/price/poolPrice?startDate=2026-07-01&endDate=2026-07-27
API-KEY: <your key>
```

The API returns **at most one year of data per request**. For longer histories, walk the range in
one-year windows yourself — there is no pagination, no cursor and no `limit` parameter.

Each row of `Pool Price Report` carries `begin_datetime_utc`, `begin_datetime_mpt`, `pool_price`,
`forecast_pool_price` and `rolling_30day_avg`.

## Step 2 — Pull the System Marginal Price for the same window

Operation `getSystemMarginalPriceReportForDateRange` — `GET /price/systemMarginalPrice` on
`https://apimgw.aeso.ca/public/systemmarginalprice-api/v1.1`. Same `startDate` / `endDate`
convention.

Join the two series on `begin_datetime_utc`. SMP moves within an hour; Pool Price is one value per
settlement hour, so expect many SMP rows per Pool Price row.

## Step 3 — Read the live price

Operation `getCurrentSystemMarginalPriceReport` — `GET /price/systemMarginalPrice/current`. No
parameters. Use this for a live dashboard rather than polling the range report with today's date.

To get the latest *Pool Price*, call `getPoolPriceDateRangeReport` with `startDate` set to today; only
completed settlement hours are returned.

## Rules that apply to every call

- **Types.** Prices come back as JSON **strings**, not numbers. Parse before you arithmetic.
- **Timezones.** Every row carries both `begin_datetime_utc` and `begin_datetime_mpt` (Mountain
  Prevailing Time). Settlement hours are defined in MPT. Do arithmetic in UTC, present in MPT.
- **Errors.** Not RFC 9457 — the Azure APIM gateway returns `{"statusCode": …, "message": "…"}`.
  `401` means no key was sent, `403` means the key is not subscribed to the product (regenerate it
  from the Profile page), `400` almost always means a date failed the `yyyy-MM-dd` pattern or fell
  outside the supported range. See `errors/aeso-problem-types.yml`.
- **Rate limits.** None are published and no rate-limit headers are returned. Be conservative:
  batch by date range rather than polling per hour, and back off on `503`.
- **Versioning.** The version is in the path (`/v1.1`). AESO announces retirements as dated posts in
  <https://www.aeso.ca/market/market-updates> — there are no `Sunset` headers, so watch that stream.

## If you do not want a key

The same price series is available as anonymous CSV from the legacy ETS report servlet
`http://ets.aeso.ca/ets_web/ip/Market/Reports/SMPriceReportServlet` (append `contentType=csv`). No
key, no account. Use it for exploration; use the API for anything scheduled.
