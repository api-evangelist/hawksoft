# HawkSoft (hawksoft)

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
