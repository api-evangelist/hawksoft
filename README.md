# HawkSoft (hawksoft)

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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

HawkSoft is an insurance agency management system (AMS) for independent property and casualty agencies, covering client management, policy tracking, documentation, accounting, and workflow automation. HawkSoft operates a **gated Partner API** program that lets vetted third-party technology vendors and agencies read agency, office, client, contact, policy, coverage, vehicle, driver, and log data, and (with 2-way integration) write activities back into HawkSoft as log notes, attachments, and payment receipts.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/hawksoft/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/hawksoft/refs/heads/main/apis.yml)

## Access Model — Read This First

The HawkSoft Partner API is **gated**, though its documentation is **public**:

- **Documentation is publicly readable** (no NDA) at [partner.hawksoft.app](https://partner.hawksoft.app/) for both V1.8 and V3.0.
- **Credentials are private.** HawkSoft issues API credentials only to vetted, approved API Partners. Prospective partners contact `opportunities@hawksoft.com`.
- **Agencies must opt in.** A partner can only access an agency's data after that agency, an active HawkSoft subscriber, opts in to share it. Access is revocable.
- **Base URL:** `https://integration.hawksoft.app`
- **Auth:** HTTP Basic (partner user + password). V3.0 requests require a `version=3.0` query parameter.
- **Partner fee:** HawkSoft's API Terms state a **$3,000/year API fee**, payable in advance, which may be waived with prior written consent.

Because the API is gated, the endpoint **paths, methods, and base URL** in `openapi/hawksoft-openapi.yml` are taken directly from HawkSoft's public documentation and are real, but the **request/response schemas are modeled** from the documentation rather than exercised against a live account. This is flagged in `review.yml` (`endpointsModeled: true`).

## APIs

The Partner API surface is grouped here into four logical APIs. All share the `https://integration.hawksoft.app` base URL and the `/vendor/...` path prefix.

### HawkSoft Agencies and Offices API

List the agencies that have authorized a partner and enumerate each agency's offices — the entry point that resolves the `agencyId` before requesting client data.

- `GET /vendor/agencies`
- `GET /vendor/agency/{agencyId}/offices`

### HawkSoft Clients API

Read client records. In V3.0 a client payload consolidates contacts, policies and coverages, vehicles, and drivers under the HawkSoft 6 cloud data model.

- `GET /vendor/agency/{agencyId}/clients` — clients changed since a timestamp (incremental sync)
- `POST /vendor/agency/{agencyId}/clients` — batch fetch by id (up to 200 client ids)
- `GET /vendor/agency/{agencyId}/clients/search` — search clients
- `GET /vendor/agency/{agencyId}/client/{clientId}` — single client

### HawkSoft Log Entries API

Write activities back into a client's log — the core of HawkSoft's 2-way integration.

- `POST /vendor/agency/{agencyId}/client/{clientId}/log`

### HawkSoft Attachments and Receipts API

Write documents and payment records to a client.

- `POST /vendor/agency/{agencyId}/client/{clientId}/attachment`
- `POST /vendor/agency/{agencyId}/client/{clientId}/receipts` (V3.0)

## Realtime / WebSocket

HawkSoft does **not** expose a documented public WebSocket API. The Partner API is request/response REST over HTTPS; partners keep data in sync by polling the changed-clients endpoint with a `since` timestamp, not by subscribing to a realtime stream. See `review.yml`.

## Pricing

- **HawkSoft AMS (agency):** per-seat subscription — reported around a base fee plus ~$94 per user per month, starting near $250/month, plus one-time setup and training. Custom-quoted; HawkSoft does not publish exact figures.
- **Partner API (vendor):** $3,000/year (waivable). See `plans/hawksoft-plans-pricing.yml`.

## Tags

- Insurance
- Agency Management System
- AMS
- InsurTech
- Property and Casualty
- Partner API
- Gated API

## Timestamps

- **Created:** 2026-07-10
- **Modified:** 2026-07-10

## Supporting Artifacts

- [OpenAPI](openapi/hawksoft-openapi.yml)
- [Plans / Pricing](plans/hawksoft-plans-pricing.yml)
- [Rate Limits](rate-limits/hawksoft-rate-limits.yml)
- [FinOps](finops/hawksoft-finops.yml)
- [Review](review.yml)

## Common Properties

- [Website](https://www.hawksoft.com)
- [LinkedIn](https://www.linkedin.com/company/hawksoft-inc-)
- [Partner API Documentation](https://partner.hawksoft.app/)
- [Partner Program / Sign Up](https://www.hawksoft.com/about/partners/)
- [API Terms of Service](https://www.hawksoft.com/terms/api/)
- [Blog](https://blog.hawksoft.com/)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
