---
name: Bulk export Northern Powergrid datasets and federate the catalogue
description: >-
  Pull whole Northern Powergrid datasets without paging — CSV, Parquet, GeoJSON, GPX — and harvest
  the entire 102-dataset catalogue as DCAT-AP RDF/XML for federation into another data portal or
  catalogue. Use this for analytics loads, GIS work, and open data portal harvesting.
api: openapi/northern-powergrid-open-data-explore-api-v2-1-openapi.json
base_url: https://northernpowergrid.opendatasoft.com/api/explore/v2.1
operations:
  - listExportFormats
  - exportDatasets
  - exportCatalogCSV
  - exportCatalogDCAT
  - listDatasetExportFormats
  - exportRecords
  - exportRecordsCSV
  - exportRecordsParquet
  - exportRecordsGPX
auth: optional
generated: '2026-07-27'
method: generated
---

# Bulk export and federate

The record endpoints cap results (100 rows without a `group_by`, `offset + limit` under 10,000). The
export endpoints do not cap anything. If you are paging to get a whole dataset, you are using the
wrong endpoint — the provider says so explicitly in the spec description.

## Exporting one dataset

Ask what formats it supports first:

```
GET /catalog/datasets/{dataset_id}/exports
```

Then pull it (`exportRecords`, or one of the format shorthands):

```
GET /catalog/datasets/{dataset_id}/exports/json
GET /catalog/datasets/{dataset_id}/exports/csv          # exportRecordsCSV
GET /catalog/datasets/{dataset_id}/exports/parquet      # exportRecordsParquet
GET /catalog/datasets/{dataset_id}/exports/geojson
GET /catalog/datasets/{dataset_id}/exports/gpx          # exportRecordsGPX
```

Format notes worth knowing before you write a loader:

- **Parquet** is the one to reach for on anything analytical — it is a first-class export here, not
  an afterthought, and it keeps types.
- **CSV** takes a `delimiter` parameter (default `;`, also `,`, tab, `|`) and emits a byte order mark
  by default since v2.1. Strip or expect the BOM.
- **GeoJSON** is the right choice for the network geometry datasets — LV and HV feeders, underground
  cables, substation areas, boundary sets — which carry `geo_point_2d` and `geo_shape` fields.
  Datetimes in GeoJSON exports are ISO-format strings since v2.1 (they were integer timestamps in
  v2.0).
- **GPX** exists for track/waypoint consumers.

ODSQL still applies to exports. Filter and aggregate server-side rather than downloading everything
and discarding most of it:

```
GET /catalog/datasets/{dataset_id}/exports/parquet?where=year(date_field)%3D2026
GET /catalog/datasets/{dataset_id}/exports/csv?select=field_a,field_b&where=field_a>0
```

Since v2.1 the `group_by` clause is available on export endpoints too, so a pre-aggregated export is
a single call.

## Harvesting the whole catalogue

List the catalogue-level formats (`listExportFormats`):

```
GET /catalog/exports
```

Then export it (`exportDatasets` / `exportCatalogCSV`):

```
GET /catalog/exports/csv
GET /catalog/exports/{format}
```

For federation into another open data portal or catalogue, use DCAT-AP RDF/XML
(`exportCatalogDCAT`) — this is the standards-based path and the reason this catalogue can be
harvested by CKAN, data.gov.uk-style aggregators and linked-data tooling:

```
GET /catalog/exports/dcat
GET /catalog/exports/dcat{dcat_ap_format}
```

This endpoint is already wired as the `Catalog` property on the provider record, and it is the
single highest-leverage call on the whole API for anyone building a downstream catalogue.

## Budget and etiquette

- Exports are still requests: each one costs a unit of the 5,000/day anonymous allowance. Exporting
  102 datasets is 102 requests plus discovery — comfortably inside the budget, but do not loop.
- Register a free account (https://northernpowergrid.opendatasoft.com/signup/) for a larger daily
  allowance and to reach the roughly 44 datasets whose records are gated to anonymous callers. Send
  the key as `Authorization: Apikey <API_KEY>`.
- Cache. Most of these datasets change on a slow cadence — check `metas.default.modified` on the
  dataset (via `getDataset`) and re-export only when it moves. Live power cuts are the exception.
- On `429`, back off to the `X-RateLimit-Reset` timestamp; the window is daily.
- Everything is a GET, so a failed export is always safe to retry.

## Licence

Exported data carries the Northern Powergrid Open Data Licence v1.0
(https://northernpowergrid.opendatasoft.com/p/opendatalicence/). It is a bespoke licence rather than
OGL v3.0 — read it before you redistribute or republish, especially if you are federating the
catalogue into a portal with its own licence defaults.
