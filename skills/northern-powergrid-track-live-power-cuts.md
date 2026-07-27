---
name: Track live power cuts on the Northern Powergrid network
description: >-
  Read Northern Powergrid's live power cut incidents — open faults, affected areas, estimated
  restoration times — from the open data Explore API, with no credential, and aggregate them by
  category or area. Use this for outage monitoring, situational awareness, or joining incident data
  to geography.
api: openapi/northern-powergrid-open-data-explore-api-v2-1-openapi.json
base_url: https://northernpowergrid.opendatasoft.com/api/explore/v2.1
dataset: live-power-cuts-data
operations:
  - getDataset
  - getRecords
  - getRecordsFacets
  - exportRecords
auth: none
generated: '2026-07-27'
method: generated
---

# Track live power cuts

Northern Powergrid publishes its live incident feed as an ordinary open dataset. There is no special
outage API and no credential — the same read-only Explore API that serves the catalogue serves the
faults, refreshed continuously. At the time this skill was written the dataset held 242 open
incidents.

## Before you start

- No API key needed. Anonymous callers get 5,000 requests per day.
- Everything here is a GET. Nothing you do can change anything, and every call is safe to retry.
- Read `conventions/northern-powergrid-conventions.yml` for the ODSQL grammar and paging caps, and
  `errors/northern-powergrid-problem-types.yml` for the error envelope.

## Step 1 — Learn the record shape (`getDataset`)

Per-dataset field definitions are runtime data, not part of the OpenAPI contract. Always read them
before composing a query.

```
GET /catalog/datasets/live-power-cuts-data
```

Read `fields[]` from the response. The incident record carries, among others: `reference`,
`incidentid`, `powercutcategory`, `natureofoutage`, `type` (voltage level, e.g. `LV`), `area`,
`postcode`, `lat`, `lng`, `loggedtime`, `estimatedtimetillresolution`, `elapsedtime`,
`totalconfirmedpowercut`, `totalpredictedpowercut`, `numberofcalls`, `priority`, `incidentstatus`,
`reason` and `customerstagesequencemessage`.

Do not hard-code this list. Re-read `fields[]` on each run; the guarantee the provider gives is that
keys are added, never renamed or removed — but that guarantee is about the API envelope, not about
a dataset's columns.

## Step 2 — Read the open incidents (`getRecords`)

```
GET /catalog/datasets/live-power-cuts-data/records?limit=100
```

`total_count` on the response is the number of open incidents. `limit` maxes at 100 without a
`group_by`, and `offset + limit` must stay under 10,000, so page with `offset` in steps of 100.

Narrow with ODSQL rather than filtering client-side:

```
GET /catalog/datasets/live-power-cuts-data/records?where=area%3D%22Yorkshire%22&limit=100
GET /catalog/datasets/live-power-cuts-data/records?where=type%3D%22LV%22&order_by=loggedtime%20desc&limit=20
```

## Step 3 — Aggregate server-side (`getRecords` with `group_by`)

Do not pull every row to count things. `group_by` runs on the server and lifts the row cap to 20,000.

```
GET /catalog/datasets/live-power-cuts-data/records?select=count(*)%20as%20incidents&group_by=area
GET /catalog/datasets/live-power-cuts-data/records?select=count(*)%20as%20incidents&group_by=powercutcategory
```

## Step 4 — Enumerate the dimensions (`getRecordsFacets`)

To discover what values a field actually takes before filtering on it:

```
GET /catalog/datasets/live-power-cuts-data/facets?facet=area
```

## Step 5 — Bulk or geospatial pull (`exportRecords`)

The record paging caps do not apply to exports. For a full snapshot, or for map rendering off the
`lat`/`lng` and any geo fields:

```
GET /catalog/datasets/live-power-cuts-data/exports/json
GET /catalog/datasets/live-power-cuts-data/exports/geojson
```

## Polling rules

- This is live operational data, but you have a **daily** budget of 5,000 requests, not a per-second
  one. Polling every 30 seconds costs 2,880 requests a day — over half the anonymous allowance for
  one dataset. Poll at the cadence your use case genuinely needs, and register a free account
  (https://northernpowergrid.opendatasoft.com/signup/) for a larger allowance if you need more.
- Read `X-RateLimit-Remaining` off every response and stop before it hits zero.
- On `429`, back off until the `X-RateLimit-Reset` timestamp. That is a daily boundary — retrying in
  a few seconds will not help.
- On `400` with `error_code: ODSQLSyntaxError`, the message names the failing clause and character
  offset. Fix the query; do not retry it unchanged.
- Watch the `ODS-Explore-API-Deprecation` response header for feature-level deprecation notices.

## What this data is not

These are network incidents, not customer records. Northern Powergrid is a distribution network
operator — it moves electricity and holds no retail accounts — so there is no consumer, billing or
consumption-per-household surface here, and no consumer data right in Great Britain that would
create one.
