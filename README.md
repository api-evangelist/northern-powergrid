# Northern Powergrid (northern-powergrid)

Northern Powergrid is the electricity distribution network operator (DNO) for the North East of England, Yorkshire and northern Lincolnshire, owning and running the poles, wires, substations and low-voltage network that deliver power to 4 million homes and businesses across roughly 10,000 square miles. It is a Berkshire Hathaway Energy company and it does not sell electricity — it moves it, so it holds no retail customer accounts and no billing relationship. Its API posture reflects that split exactly: the market and network side is genuinely open, with a live Opendatasoft-hosted open data portal publishing 102 datasets under the Northern Powergrid Open Data Licence v1.0 and a fully documented Explore REST API that answers anonymously at 5,000 requests a day, including live power cut incidents, operational metering, embedded capacity registers, network capacity headroom and aggregated smart meter consumption; the consumer side is empty, because Britain has no energy consumer data right equivalent to the Australian Consumer Data Right and a DNO would not be the obligated party if it did. The open data programme exists because Ofgem's Data Best Practice Guidance is a licence condition under the RIIO-ED2 price control, and unlike many mandates in this sector it is visibly implemented rather than merely claimed. Roughly 44 of the 102 datasets are metadata-visible but records-gated to anonymous callers and require a free self-serve portal registration to read.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/northern-powergrid/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/northern-powergrid/refs/heads/main/apis.yml)

## Tags

- Energy
- United Kingdom
- Utilities
- Electricity
- Grid
- Open Data
- Distribution Network Operator
- Smart Metering
- Network Capacity
- Flexibility
- DER
- Renewables

## Timestamps

- **Created:** 2026-07-27
- **Modified:** 2026-07-27

## APIs

### Northern Powergrid Open Data Explore API

The current Opendatasoft Explore REST API (v2.1) over Northern Powergrid's open data portal. Read only, GET only, JSON only, driven by the Opendatasoft Query Language (ODSQL). Sixteen documented paths cover catalog search, dataset metadata, facets, record retrieval, attachments, DCAT-AP catalogue export and per-dataset exports to CSV, Parquet and GPX. Confirmed answering anonymously on 2026-07-27 — the catalog reports 102 datasets and the live power cuts dataset returned 229 open incidents in real time. Anonymous callers get 5,000 requests per day; an optional `apikey` query parameter from a free portal account raises the allowance and unlocks the datasets whose records are hidden from anonymous callers.

- **Human URL:** [https://northernpowergrid.opendatasoft.com/api/explore/v2.1/console](https://northernpowergrid.opendatasoft.com/api/explore/v2.1/console)
- **Base URL:** `https://northernpowergrid.opendatasoft.com/api/explore/v2.1`

#### Tags

- Open Data
- Energy
- Electricity
- Grid
- Network Capacity
- Outages
- Geospatial

#### Properties

- [OpenAPI](openapi/northern-powergrid-open-data-explore-api-v2-1-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [API Reference](https://northernpowergrid.opendatasoft.com/api/explore/v2.1/console)
- [API Console](https://northernpowergrid.opendatasoft.com/api-console/explore/v2.1/)
- [Portal](https://northernpowergrid.opendatasoft.com/)
- [Explore](https://northernpowergrid.opendatasoft.com/explore/)
- [Documentation](https://northernpowergrid.opendatasoft.com/pages/tutorial_page/)
- [External Documentation](https://help.huwise.com/apis/ods-explore-v2/)
- [License](https://northernpowergrid.opendatasoft.com/p/opendatalicence/)
- [Catalog](https://northernpowergrid.opendatasoft.com/api/explore/v2.1/catalog/exports/dcat)

### Northern Powergrid Open Data Explore API v2.0

The previous major version of the Opendatasoft Explore REST API, still served and still publishing its own OpenAPI 3.0.3 description at `/api/explore/v2.0/swagger.json`. Byte-identical to the document served at the legacy `/api/v2/swagger.json` alias. Same sixteen paths and same read-only, GET-only, ODSQL-driven shape as v2.1.

- **Human URL:** [https://northernpowergrid.opendatasoft.com/api/explore/v2.0/console](https://northernpowergrid.opendatasoft.com/api/explore/v2.0/console)
- **Base URL:** `https://northernpowergrid.opendatasoft.com/api/explore/v2.0`

#### Tags

- Open Data
- Energy
- Electricity
- Legacy

#### Properties

- [OpenAPI](openapi/northern-powergrid-open-data-explore-api-v2-0-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [API Reference](https://northernpowergrid.opendatasoft.com/api/explore/v2.0/console)
- [Portal](https://northernpowergrid.opendatasoft.com/)
- [External Documentation](https://help.huwise.com/apis/ods-explore-v2/)

### Northern Powergrid Open Data Search API v1

The original Opendatasoft Search API, still live on the portal and still carrying its own interactive console. Confirmed anonymously on 2026-07-27 — `GET /api/datasets/1.0/search/?rows=1` returned `nhits` 102, matching the v2.1 catalog count. No OpenAPI description is published by the platform for this generation of the API, so none was saved and none was written.

- **Human URL:** [https://northernpowergrid.opendatasoft.com/api/v1/console](https://northernpowergrid.opendatasoft.com/api/v1/console)
- **Base URL:** `https://northernpowergrid.opendatasoft.com/api/datasets/1.0`

#### Tags

- Open Data
- Energy
- Search
- Legacy

#### Properties

- [API Reference](https://northernpowergrid.opendatasoft.com/api/v1/console)
- [Portal](https://northernpowergrid.opendatasoft.com/)

## Common Properties

- [Website](https://www.northernpowergrid.com/)
- [Portal](https://northernpowergrid.opendatasoft.com/)
- [Documentation](https://northernpowergrid.opendatasoft.com/pages/tutorial_page/)
- [API Console](https://northernpowergrid.opendatasoft.com/api-console/explore/v2.1/)
- [License](https://northernpowergrid.opendatasoft.com/p/opendatalicence/)
- [Explore](https://northernpowergrid.opendatasoft.com/explore/)
- [Map](https://northernpowergrid.opendatasoft.com/map/)
- [Dashboards](https://northernpowergrid.opendatasoft.com/pages/portal_dashboards/)
- [GitHub Organization](https://github.com/northernpowergrid)
- [LinkedIn](https://www.linkedin.com/company/northern-powergrid/)
- [Parent Company](https://www.brkenergy.com/our-businesses/northern-powergrid)

## Mandate and Access Posture

| Dimension | Finding |
| --- | --- |
| Home market | United Kingdom |
| Tier | Network distributor (DNO) |
| Mandate regime | Ofgem Data Best Practice Guidance, a licence condition under the RIIO-ED2 price control |
| Mandate status | **Live and implemented** — verified by fetching the OpenAPI document and querying the live catalog and live power-cut records anonymously on 2026-07-27, not from a compliance page |
| Consumer data API | **No.** Britain has no energy consumer data right; a DNO holds no retail account or billing relationship |
| Market data open | **Yes.** 102 datasets, 58 fully anonymous, including live outage and operational metering feeds |
| Data standard | No consumer data standard. IEC CIM appears as LTDS Stage 2 CIM files; OpenAPI 3.0.3 and DCAT-AP are published; queries use ODSQL |
| Access gate | Self-serve — anonymous for 58 datasets at 5,000 requests/day; free portal registration issues an `apikey` for the remaining 44 and a higher allowance |
| Auth model | None required for open data; optional API key passed as the `apikey` query parameter. No OAuth, no OpenID Connect (`/.well-known/openid-configuration` returns 404) |

Full evidence, including every URL probed with its HTTP status, is in [review.yml](review.yml).

## Maintainers

- Kin Lane — kin@apievangelist.com
