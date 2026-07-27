---
name: aeso-asset-and-participant-reference
description: Resolve AESO asset IDs and pool participant IDs into names, types and ownership, then use them to filter metered volumes and settlement-grade data.
api: openapi/aeso-assetlist-api-v1-openapi.json, openapi/aeso-poolparticipant-api-v1-openapi.json, openapi/aeso-meteredvolume-api-v1-openapi.json
operations:
  - getAssetListData
  - getPoolParticipantListData
  - getMeteredVolumeReport
generated: '2026-07-27'
method: generated
source: openapi/*.json + data-model/aeso-data-model.yml
---

# AESO asset and participant reference data

Every other AESO feed is full of opaque codes. Two registries turn them into meaning, and they are
the join keys for the whole surface:

- `asset_ID` — issued by the **Asset List API**, used by metered volume, per-asset generation, gen
  capacity and unit commitment.
- `pool_participant_ID` — issued by the **Pool Participant API**, used by the asset list and metered
  volume.

Load both registries once, cache them, and resolve locally. They change rarely — new assets are
announced in <https://www.aeso.ca/market/market-updates>.

## Step 1 — Load the asset registry

Operation `getAssetListData` — `GET /assetlist` on
`https://apimgw.aeso.ca/public/assetlist-api/v1`. Every parameter is optional, so an unfiltered call
returns the whole registry.

| Parameter | In | Required |
|---|---|---|
| `asset_ID` | query | no |
| `pool_participant_ID` | query | no |
| `operating_status` | query | no |
| `asset_type` | query | no |

```
GET https://apimgw.aeso.ca/public/assetlist-api/v1/assetlist
API-KEY: <your key>
```

Filter by `pool_participant_ID` to get one participant's fleet, or by `asset_type` /
`operating_status` to scope to, say, operating wind assets.

## Step 2 — Load the participant registry

Operation `getPoolParticipantListData` — `GET /poolparticipantlist` on
`https://apimgw.aeso.ca/public/PoolParticipant-api/v1`. Note the mixed-case `PoolParticipant`
segment in the path — it is genuinely capitalised that way on the gateway.

| Parameter | In | Required |
|---|---|---|
| `pool_participant_ID` | query | no |
| `pool_participant_name` | query | no |

Build a `pool_participant_ID → name` map and enrich every asset from step 1.

## Step 3 — Pull metered volumes for the assets you care about

Operation `getMeteredVolumeReport` — `GET /meteredvolume/details` on
`https://apimgw.aeso.ca/public/meteredvolume-api/v1`.

| Parameter | In | Required | Notes |
|---|---|---|---|
| `startDate` | query | yes | `yyyy-MM-dd` |
| `endDate` | query | no | `yyyy-MM-dd`, after `startDate` |
| `asset_ID` | query | no | from step 1 |
| `pool_participant_ID` | query | no | from step 2 |

This is settlement-grade metering at **market-asset** granularity. It is not retail metering — AESO
holds no household usage or billing data, and there is no consumer energy-data obligation in
Alberta.

## Rules

- All three operations are `GET`; retries are safe.
- Values come back as JSON strings.
- No pagination — an unfiltered asset list is returned in one response. Cache it.
- `400` means a malformed date or filter value; `403` means the key is not subscribed to the AESO
  Public API product.
- Terms of use are non-commercial, personal or educational only:
  <https://www.aeso.ca/legal/>. Redistributing the registries commercially requires AESO's written
  permission.
