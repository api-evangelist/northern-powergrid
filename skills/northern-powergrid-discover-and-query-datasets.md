---
name: Discover and query the Northern Powergrid open data catalogue
description: >-
  Find the right dataset among Northern Powergrid's 102 published datasets, learn its schema, and
  query it with ODSQL — the orientation skill every other use of this API depends on. Covers
  catalogue search, faceting, per-dataset schema discovery, filtering, aggregation and the
  records-gated datasets that need a free account.
api: openapi/northern-powergrid-open-data-explore-api-v2-1-openapi.json
base_url: https://northernpowergrid.opendatasoft.com/api/explore/v2.1
operations:
  - getDatasets
  - getDatasetsFacets
  - getDataset
  - getRecords
  - getRecord
  - getRecordsFacets
  - getDatasetAttachments
auth: optional
generated: '2026-07-27'
method: generated
---

# Discover and query the catalogue

Northern Powergrid's open data portal published 102 datasets when this skill was written. They cover
the network side of a distribution network operator: live faults, operational metering at grid supply
points and primaries, embedded capacity registers, network capacity headroom, LV and HV feeder
geometry, connection queues, flexibility dispatch, aggregated smart meter consumption, long term
development statements, and the portal's own data roadmap.

The single most important habit on this API: **resolve the dataset, then read its fields, then
query.** Per-dataset schemas are runtime data. The OpenAPI describes the envelope, not the columns.

## Step 1 — Orient by theme (`getDatasetsFacets`)

Faster than reading 102 titles.

```
GET /catalog/facets?facet=theme
```

At capture time this returned `Network` (77), `Net Zero Future` (21) and `Connecting Generation`
(19), among others. Facet on `keyword`, `publisher` or `modified` the same way.

## Step 2 — Search the catalogue (`getDatasets`)

```
GET /catalog/datasets?limit=100&select=dataset_id
GET /catalog/datasets?where=search(%22capacity%22)&limit=20
GET /catalog/datasets?refine=theme%3A%22Network%22&limit=100
```

`total_count` is the catalogue size. Keep `select` tight — the full dataset objects are large.

Two flags on each dataset decide whether you can actually read it:

- `has_records` — whether the dataset has rows at all (some are document or metadata records).
- `data_visible` — whether **you** can read those rows. Roughly 44 of the 102 datasets are
  metadata-visible but records-gated to anonymous callers, and will return `total_count: 0` rather
  than a 403. If a dataset you expected to have rows returns zero, this is almost always why.

## Step 3 — Read the schema (`getDataset`)

```
GET /catalog/datasets/{dataset_id}
```

Read `fields[]` — each entry has `name`, `label`, `type` and `annotations`. Types you will meet
include `text`, `int`, `double`, `date`, `datetime`, `geo_point_2d` and `geo_shape`. The geo types
are what make the network datasets map-renderable.

Also read `metas.default` for title, description, licence, modified date and record count, and
`attachments` for any files hanging off the dataset (`getDatasetAttachments` lists them).

## Step 4 — Query with ODSQL (`getRecords`)

One grammar covers the whole API. Compose rather than post-process:

```
GET /catalog/datasets/{dataset_id}/records?select=field_a,field_b&where=field_a>100&order_by=field_b%20desc&limit=100
GET /catalog/datasets/{dataset_id}/records?select=count(*)%20as%20n,avg(field_b)%20as%20mean&group_by=field_a
GET /catalog/datasets/{dataset_id}/records?refine=field_a%3A%22value%22&limit=100
```

Clauses: `select`, `where`, `group_by`, `order_by`, `refine`, `exclude`, `limit`, `offset`, `lang`,
`timezone`. `select` can compute labelled expressions (`select=size * 2 as bigger_size`).

Paging caps: `limit` ≤ 100 without a `group_by` with `offset + limit` < 10,000; `limit` ≤ 20,000
with a `group_by`. Anything larger belongs in an export — see the bulk export skill.

## Step 5 — Narrow before you page (`getRecordsFacets`)

```
GET /catalog/datasets/{dataset_id}/facets?facet=some_field
```

Returns each value with its match count, so you can size a query before you run it.

## Step 6 — Address a single row (`getRecord`)

```
GET /catalog/datasets/{dataset_id}/records/{record_id}
```

Use the `_id` returned on a record from `getRecords`.

## Getting past the gate

If a dataset you need is records-gated, register free at
https://northernpowergrid.opendatasoft.com/signup/, generate an API key, and send it as a header:

```
Authorization: Apikey <API_KEY>
```

The query-parameter form (`?apikey=<key>`) also works but is discouraged — it lands in browser
history and server logs. A free account also raises the daily request allowance above the anonymous
5,000. For third-party applications acting on behalf of a portal user there is a full OAuth 2.0
authorization-code flow at `/oauth2/authorize/` and `/oauth2/token/`, with exactly one scope: `all`.

## Failure handling

- `400 ODSQLSyntaxError` / `ODSQLError` — the message names the clause and character offset. Fix the
  query; do not retry unchanged.
- `401` — restricted resource, no valid credential. Register and send an API key.
- `404 NotFoundResource` — the `dataset_id` is wrong. Re-resolve it through `getDatasets`.
- `429` — daily quota exhausted. Back off to `X-RateLimit-Reset`.
- `500` — retry with backoff; the API is read-only so retries are always safe.

## Licence

Everything here is published under the Northern Powergrid Open Data Licence v1.0
(https://northernpowergrid.opendatasoft.com/p/opendatalicence/) — a bespoke licence, not OGL v3.0.
Check it before redistributing.
