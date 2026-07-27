---
name: aeso-dispatch-and-intertie-transparency
description: Read the offer stack, ancillary-services offer control, unit commitment directives and intertie interchange and outages that explain how Alberta's price cleared.
api: openapi/aeso-energymeritorder-api-v1-openapi.json, openapi/aeso-operatingreserveoffercontrol-api-v1-openapi.json, openapi/aeso-unitcommitmentdata-api-v2-openapi.json, openapi/aeso-itc-api-v1-openapi.json
operations:
  - getMeritOrderReport
  - getOperatingReserveOfferControlReport
  - getUnitCommitmentDataReportV11ForDateRange
  - getReportByRange
  - getOutages
generated: '2026-07-27'
method: generated
source: openapi/*.json + conventions/aeso-conventions.yml
---

# AESO dispatch and intertie transparency

Price is the output. This skill reads the inputs: the offer stack, who controls the reserve offers,
which units were told to come online, and what the interties were doing. Bid-and-offer transparency
of this depth is unusual — most system operators publish it only on a long lag.

## Before you start

`API-KEY` header on every request; all operations are `GET`.

## Step 1 — The energy merit order

Operation `getMeritOrderReport` — `GET /meritOrder/energy` on
`https://apimgw.aeso.ca/public/energymeritorder-api/v1`.

| Parameter | In | Required | Notes |
|---|---|---|---|
| `startDate` | query | yes | `yyyy-MM-dd`. This operation takes no `endDate` — it is a snapshot report |

The stacked offers that determine which generation is dispatched and where the price clears. Cross
the clearing point against the System Marginal Price from
`skills/aeso-market-price-analysis.md` to see the marginal unit.

## Step 2 — Operating reserve offer control

Operation `getOperatingReserveOfferControlReport` — `GET /operatingReserveOfferControl` on
`https://apimgw.aeso.ca/public/operatingreserveoffercontrol-api/v1`. Takes `startDate` (required),
no `endDate`.

Who controls the offers for Alberta's ancillary-services reserve products — the concentration
picture behind the reserve market.

## Step 3 — Unit commitment directives

Operation `getUnitCommitmentDataReportV11ForDateRange` — `GET /unitCommitment` on
`https://apimgw.aeso.ca/public/unitcommitmentdata-api/v2`. Both `startDate` and `endDate` are
optional here.

The directives that bring generating units online ahead of dispatch. Columns are Asset ID, Issued
Time, Begin Time, Operation Start Time, Operation End Time.

> Two things will break naive code. **(a)** This API is **v2 only** — v1 was retired on 2025-07-30.
> **(b)** As of the 2025-04-16 ETS update, the columns `Unit Commitment Start Time` and
> `Unit Commitment End Time` were replaced by `Operation Start Time` and `Operation End Time`.
> Directives publish 60 days after the Unit Commitment End Time, so this is a retrospective feed.

## Step 4 — Intertie interchange

Operation `getReportByRange` — `GET /interchange` on `https://apimgw.aeso.ca/public/itc/v1`. This is
the most parameterised operation on the whole AESO surface.

| Parameter | In | Required |
|---|---|---|
| `startDate` | query | yes |
| `endDate` | query | yes |
| `startHE` | query | yes |
| `endHE` | query | yes |
| `version` | query | yes |
| `dataType` | query | no |
| `intertieOrFlowgate` | query | no |
| `transferType` | query | no |

`startHE` / `endHE` are hour-ending values, and `version` selects the transfer-data version — all
four are **required**, so a call with dates alone will `400`. Alberta's interties run to British
Columbia, Saskatchewan and Montana.

## Step 5 — Intertie outages

Operation `getOutages` — `GET /outage` on the same `https://apimgw.aeso.ca/public/itc/v1` host.

| Parameter | In | Required |
|---|---|---|
| `startDate` | query | yes |
| `endDate` | query | yes |
| `affectedIntertieOrFlowgate` | query | no |

Outages affecting transfer capability on interties and flowgates — the reason a transfer limit
dropped.

## Rules

- Required-parameter discipline matters more here than anywhere else in the AESO surface: `/outage`
  requires **both** dates and `/interchange` requires five parameters. A `400` on these operations is
  almost always a missing required parameter, not a bad value.
- Snapshot reports (`/meritOrder/energy`, `/operatingReserveOfferControl`) take `startDate` only —
  passing `endDate` is not supported.
- Values are JSON strings; timestamps come in UTC and Mountain Prevailing Time.
- No pagination, no rate-limit headers, no `Sunset` headers. Watch
  <https://www.aeso.ca/market/market-updates> for retirements.
- Use of this data is limited to non-commercial, personal or educational purposes under
  <https://www.aeso.ca/legal/>.
