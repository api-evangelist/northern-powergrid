# Northern Powergrid (northern-powergrid)

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
