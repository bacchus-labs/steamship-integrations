# Hapag-Lloyd — API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only — not verified with live API testing. API catalog obtained from publicly accessible `https://api-portal.hlag.com/v1/apis` endpoint. OpenAPI specification analyzed from portal response and community-generated client libraries. No credentials were used.
> **Researched by**: agent (audit/hapag-lloyd)
> **Date**: 2026-02-11
> **Last verified**: 2026-02-11

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | Hapag-Lloyd AG |
| **SCAC Code** | HLCU |
| **Parent Company** | Hapag-Lloyd AG (independent, publicly traded on Frankfurt Stock Exchange) |
| **Alliance** | Gemini Cooperation (with Maersk) — launched February 2025; Hapag-Lloyd left THE Alliance in January 2025 |
| **Primary Services** | Container shipping |
| **Market Position** | 5th largest container shipping line globally |
| **Headquarters** | Hamburg, Germany |
| **Website** | [https://www.hapag-lloyd.com](https://www.hapag-lloyd.com) |

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | Yes |
| **Developer portal URL** | [https://api-portal.hlag.com](https://api-portal.hlag.com) |
| **API documentation URL(s)** | Embedded in developer portal (Vue.js SPA, requires login for full docs) |
| **Documentation quality** | Good — DCSA-aligned OpenAPI specs, FAQs, tutorials with example requests; some APIs lack path detail in public listing |
| **OpenAPI/Swagger spec available?** | Yes — full TNT v2.2.4 spec available via portal's public `/v1/apis` endpoint; Rate Sheet spec on [GitHub](https://github.com/Hapag-Lloyd/customer-api-definitions) |
| **Sandbox/test environment?** | Yes — mock server at `https://mock.api-portal.hlag.com/v2/events` ([TNT API docs](https://api-portal.hlag.com)). **⚠️ Caveat**: Mock server returns data in an older v1.x-style event format (flat `eventTypeCode` instead of separate `equipmentEventTypeCode`/`transportEventTypeCode`; simple `transportCallID` instead of embedded `transportCall` objects). Do not rely on mock response structure for production code — see [Gotchas](#known-issues--gotchas) |
| **Developer registration** | Free self-service registration at [api-portal.hlag.com](https://api-portal.hlag.com) |
| **Developer support channels** | Contact form via API portal; general: [api-portal.hlag.com](https://api-portal.hlag.com) |
| **Community/third-party libraries** | Python: [`hapag-lloyd-sdk`](https://pypi.org/project/hapag-lloyd-sdk/) v0.2.1 (PyPI; source repo [`gedankenfabrik/hapag_lloyd_sdk`](https://github.com/gedankenfabrik/hapag_lloyd_sdk) on GitHub is unavailable — returns 404, deleted or private as of Feb 2026); Ruby: [`hapag-lloyd_client`](https://github.com/Cellpap/hapag-lloyd_client) (GitHub, auto-generated from OpenAPI); Java/GitHub: [customer-api-definitions](https://github.com/Hapag-Lloyd/customer-api-definitions) — Rate Sheet notification callback spec only (defines the endpoint customers must implement to receive rate sheet push notifications from HL; not a general API client library; `com.hlag.api:openapi-specs` is not published on Maven Central as of Feb 2026) |
| **API changelog / release notes** | TNT changelog in API description: v2.2.2 May 2025 (Pilot Test); no separate changelog URL found |

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | Yes — **founding member** (April 2019, [source](https://dcsa.org/about-us/)) |
| **DCSA APIs implemented** | TNT (Track & Trace), CS (Commercial Schedules), OVS (Operational Vessel Schedules) |
| **DCSA TNT version** | v2.2.4 (based on DCSA Information Model v3.3) — **BETA** ([API portal](https://api-portal.hlag.com)) |
| **DCSA Commercial Schedules version** | v1.0.1 (Point-to-Point Routes + Vessel Schedules) ([API portal](https://api-portal.hlag.com)) |
| **DCSA OVS version** | v3.0.7 (Operational Vessel Schedules) ([API portal](https://api-portal.hlag.com)) |
| **DCSA Booking version** | N/A — not listed in API catalog as of Feb 2026 |
| **DCSA eDocumentation version** | N/A — not listed in API catalog as of Feb 2026 |
| **Known DCSA deviations** | ShipmentEvent `shipmentEventTypeCode` limited to `ISSU` and `CONF` only (DCSA standard includes additional codes: RECE, DRFT, PENA, APPR, CANC, REJE, RELS, PENU). DocumentTypeCode limited to `BKG` and `TRD` (missing `SHI` for Shipping Instructions). TNT API explicitly labeled BETA — data may differ from website. See [Gotchas](#known-issues--gotchas) |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Yes | Standard for major carriers; HL supports EDI messaging for booking/tracking |
| **INTTRA integration** | Yes | Hapag-Lloyd is connected to INTTRA/E2open platform |
| **BIC (Bureau International des Containers)** | Yes | Equipment references follow BIC ISO Container Identification Number (ISO 6346) per API spec |
| **UN/LOCODE** | Yes | Used throughout API for location identification (`UNLocationCode` field) |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | API Key (Client ID + Client Secret via IBM API Connect headers) |
| **Auth documentation** | [api-portal.hlag.com](https://api-portal.hlag.com) (within portal, requires login) |
| **Registration process** | 1. Go to [api-portal.hlag.com](https://api-portal.hlag.com) → Register. 2. Create an Application to get Client ID + Client Secret. 3. Subscribe the Application to desired API product (e.g., Track & Trace). 4. Use credentials in API calls |
| **Registration URL** | [https://api-portal.hlag.com](https://api-portal.hlag.com) |
| **Partner program required?** | No — Track & Trace, Schedules, and Prices APIs are publicly available to all registered users. HL LIVE and Live Position require separate commercial contracts |
| **Credential type** | Client ID + Client Secret |
| **Token refresh supported?** | N/A — API Key auth (no token refresh needed). Legacy Authentication API (v1.0.37) exists for older systems that need token-based auth |
| **Token lifetime** | N/A — API keys are persistent |
| **Access tiers** | **Tryout**: 100 calls/day, 10 calls/min; **Default**: 6,000 calls/day, 10 calls/min; **Premium**: 100,000 calls/day, 150 calls/min ([TNT API docs](https://api-portal.hlag.com)) |
| **IP whitelisting required?** | Unknown — not documented in public API spec |

### Authentication Headers

```http
X-IBM-Client-Id: <your-client-id>
X-IBM-Client-Secret: <your-client-secret>
```

The API runs on IBM API Connect infrastructure (indicated by `X-IBM-Client-*` headers).

### Access Requirements Summary for SSL

Registration at [api-portal.hlag.com](https://api-portal.hlag.com) is free and self-service. SSL should register an account, create an Application, and subscribe to the Track & Trace API (starts on Tryout tier: 100 calls/day). The Default tier (6,000 calls/day) and Premium tier (100,000 calls/day, 150 calls/min) likely require contacting Hapag-Lloyd through the portal. No separate business relationship or partnership agreement appears to be required for basic Track & Trace access. For HL LIVE (reefer monitoring) or Live Position APIs, SSL would need to purchase a separate API contract through their Hapag-Lloyd sales representative.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field must have a row.
> ✅ = Available | ❌ = Not available | ⚠️ = Partial / limited | ❓ = Unknown

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint / API Product | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-------------------------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ✅ | DCSA Commercial Schedules API v1.0.1 + OVS v3.0.7 | Vessel schedules, port calls, ETAs/ETDs | DCSA CS v1 + OVS v3 | Two separate APIs: Commercial Schedules for customer-facing, OVS for liner-to-liner |
| 1.2 | Point-to-Point Route Options | ✅ | DCSA Commercial Schedules API v1.0.1 | Point-to-Point routing endpoint | DCSA CS v1 `point-to-point-routes` | Provides end-to-end routing options with legs, transit times |
| 1.3 | Booking Lifecycle | ⚠️ | TNT v2.2.4 (ShipmentEvent with `documentTypeCode=BKG`) | `shipmentEventTypeCode`: ISSU, CONF | DCSA TNT ShipmentEvent | Limited: only ISSU and CONF status codes. Missing RECE, DRFT, PENA, REJE, CANC. No standalone Booking API |
| 1.4 | Shipping Instructions | ⚠️ | TNT v2.2.4 (ShipmentEvent with `documentTypeCode=TRD`) | `shipmentEventTypeCode`: ISSU, CONF for Transport Docs | DCSA TNT ShipmentEvent | Indirect: only doc issuance/confirmation events. No Shipping Instructions (`SHI`) document type. No dedicated eDocumentation API |
| 1.5 | Rates | ✅ | Prices API v2.1.2 | Real-time pricing, quotations | Proprietary (not DCSA) | Proprietary API for prices/quotations |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❓ | Not found in TNT spec | — | `ECP` | May be in Commercial Schedules API (not publicly exposed in spec) or booking confirmation |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❓ | Not found in TNT spec | — | `EFC` | May be in Commercial Schedules API or booking confirmation |
| 2.3 | Documentation Cutoff | DCO | ❓ | Not found in TNT spec | — | `DCO` | Likely in Commercial Schedules point-to-point response (spec not publicly detailed) |
| 2.4 | VGM Cutoff | VCO | ❓ | Not found in TNT spec | — | `VCO` | Likely in Commercial Schedules response |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ❓ | Not found in TNT spec | — | `FCO` | Likely in Commercial Schedules response |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❓ | Not found in TNT spec | — | `LCO` | Likely in Commercial Schedules response |

> **Note on Cutoffs**: The DCSA Commercial Schedules API v1.0.1 standard includes `cutOffTimes[]` in point-to-point route responses. However, the public API listing did not expose the full endpoint paths/schemas for the Commercial Schedules API. Cutoff data is likely available but needs verification with authenticated access.

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ⚠️ | `GET /` (TNT Events) | Inferred from first EquipmentEvent with matching booking ref | Inferred from first EquipmentEvent | No explicit assignment event; inferred from first equipment event |
| 3.2 | Empty Container Gate-Out (Pickup) | ✅ | `GET /` (TNT Events) | `equipmentEventTypeCode: GTOT` + `emptyIndicatorCode: EMPTY` | `GTOT` + `EMPTY` | Supported per DCSA standard |
| 3.3 | Full Container Gate-In | ✅ | `GET /` (TNT Events) | `equipmentEventTypeCode: GTIN` + `emptyIndicatorCode: LADEN` | `GTIN` + `LADEN` | Supported per DCSA standard |
| 3.4 | Container Loaded on Vessel | ✅ | `GET /` (TNT Events) | `equipmentEventTypeCode: LOAD` + `emptyIndicatorCode: LADEN` | `LOAD` + `LADEN` | Core milestone |
| 3.5 | Container Discharged at Transshipment | ✅ | `GET /` (TNT Events) | `equipmentEventTypeCode: DISC` + `emptyIndicatorCode: LADEN` at transshipment port | `DISC` + `LADEN` + transshipment | Distinguish via `transportCall.UNLocationCode` against route |
| 3.6 | Container Loaded at Transshipment | ✅ | `GET /` (TNT Events) | `equipmentEventTypeCode: LOAD` + `emptyIndicatorCode: LADEN` at transshipment port | `LOAD` + `LADEN` + transshipment | New vessel in `transportCall.vessel` |
| 3.7 | Container Discharged at Destination | ✅ | `GET /` (TNT Events) | `equipmentEventTypeCode: DISC` + `emptyIndicatorCode: LADEN` at destination | `DISC` + `LADEN` | Core milestone |
| 3.8 | Full Container Gate-Out (Delivery) | ✅ | `GET /` (TNT Events) | `equipmentEventTypeCode: GTOT` + `emptyIndicatorCode: LADEN` | `GTOT` + `LADEN` | |
| 3.9 | Empty Container Returned | ✅ | `GET /` (TNT Events) | `equipmentEventTypeCode: GTIN` + `emptyIndicatorCode: EMPTY` | `GTIN` + `EMPTY` | |

> **Note**: The TNT API also supports `STUF` (Stuffed) and `STRP` (Stripped) equipment event types beyond the core milestones. The API does **not** distinguish transshipment moves via an `isTransshipmentMove` field — transshipment must be inferred from the transport plan and `transportCall.UNLocationCode`.

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ✅ | `GET /` (TNT Events) | `transportEventTypeCode: DEPA` + `eventClassifierCode: PLN/EST/ACT` | `DEPA` + classifier | Full PLN→EST→ACT progression |
| 4.2 | Estimated Time of Arrival | ETA | ✅ | `GET /` (TNT Events) | `transportEventTypeCode: ARRI` + `eventClassifierCode: PLN/EST/ACT` | `ARRI` + classifier | Full PLN→EST→ACT progression |
| 4.3 | Vessel Arrival at Transshipment | — | ✅ | `GET /` (TNT Events) | `transportEventTypeCode: ARRI` at intermediate port | `ARRI` at intermediate | Identified by `transportCall.UNLocationCode` |
| 4.4 | Vessel Departure from Transshipment | — | ✅ | `GET /` (TNT Events) | `transportEventTypeCode: DEPA` at intermediate port | `DEPA` at intermediate | Identified by `transportCall.UNLocationCode` |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❌ | Not yet available. FAQ states: "Not yet, but please observe the release notes for changes" ([TNT API docs](https://api-portal.hlag.com)) |
| Event Polling with timestamp filter | ✅ | `eventCreatedDateTime` param with operators: `:gte`, `:gt`, `:lte`, `:lt`, `:eq` |
| Event Classifier Progression (PLN→EST→ACT) | ✅ | Both Transport and Equipment events support PLN, EST, ACT classifiers |
| Retracted Events | ❓ | Not documented in the public spec; DCSA standard supports `retractedEventID` but unclear if HL implements it |
| Change Remarks | ❓ | Not present in the analyzed OpenAPI spec; DCSA `changeRemark` field not found |
| Delay Reason Codes | ❓ | Not present in the analyzed OpenAPI spec; DCSA `delayReasonCode` field not found |

### Coverage Summary

| Category | Fields Available | Fields Unavailable | Fields Unknown | Coverage % |
|----------|-----------------|-------------------|----------------|-----------|
| API Domains (1.x) | 3/5 | 0/5 | 0/5 | 60% (2 partial) |
| Cutoffs (2.x) | 0/6 | 0/6 | 6/6 | 0% confirmed (likely available in Schedules API) |
| Container Milestones (3.x) | 8/9 | 0/9 | 0/9 | 89% (1 partial: inferred assignment) |
| Transport Events (4.x) | 4/4 | 0/4 | 0/4 | 100% |
| Change Detection (5.x) | 2/6 | 1/6 | 3/6 | 33% |
| **Total** | **17/30** | **1/30** | **9/30** | **57% confirmed, likely higher** |

> **Assessment**: The 57% confirmed coverage understates the likely real coverage. The 6 unknown cutoff fields are probably available via the Commercial Schedules API (which follows DCSA CS standard that includes cutoffs), and the 3 unknown change detection fields may be supported but not visible in the public spec. With authenticated access, coverage could realistically be 75-85%.

---

## Endpoint Reference

### Tracking / Events (Primary)

| Endpoint | Method | Lookup Params | Pagination | Response Format | Notes |
|----------|--------|--------------|------------|----------------|-------|
| `GET https://api.hlag.com/hlag/external/v2/events/` | GET | `equipmentReference`, `carrierBookingReference`, `transportDocumentReference` | `limit` param (default: 100, min: 1) + `sort` param | JSON | **Primary tracking endpoint.** At least one of the three lookup params required. Supports filtering by `eventType`, `equipmentEventTypeCode`, `transportEventTypeCode`, `shipmentEventTypeCode`, `documentTypeCode`, `exportVoyageNumber`, `UNLocationCode`, `eventCreatedDateTime` |

**Mock endpoint for testing:**
| Endpoint | Method | Notes |
|----------|--------|-------|
| `GET https://mock.api-portal.hlag.com/v2/events/` | GET | Sandbox/mock server for development. **⚠️ Returns v1.x-style event format** — see [Gotchas](#known-issues--gotchas) |

### Schedules

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| DCSA Commercial Schedules v1.0.1 | GET | Point-to-point routes, vessel schedules | Unknown | JSON | Listed in API catalog but paths not publicly exposed. Follows DCSA CS v1 standard |
| DCSA OVS v3.0.7 | GET | Vessel schedules (operational, liner-to-liner) | Unknown | JSON | Follows DCSA OVS v3 standard. Interface standard: [DCSA OVS spec](https://dcsa.org/wp-content/uploads/2020/07/DCSA-Interface-Standard-for-Operational-Vessel-Schedules-1.0-vF.pdf) |

### Pricing / Rates

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| Prices API v2.1.2 | GET/POST | Routing, equipment type, dates | Unknown | JSON | Real-time pricing and quotation API. Details require authenticated portal access |

### Other Endpoints

| Endpoint | Method | Purpose | Key Params | Notes |
|----------|--------|---------|-----------|-------|
| Authentication API v1.0.37 | POST | Token auth for legacy apps | Username/password | Only needed for legacy systems; modern apps use Client ID/Secret directly |
| Transportation Status v1.1.8 | POST | Inland carrier status reporting | Work order, container, arrival status | For inland carriers to report to HL, not for SSL tracking |
| Inland Delays v2.1.8 | POST | Inland delay announcements | Container, ETA, delay reason | For inland carriers, not for SSL tracking |
| Smart PTI v1.0.2 | GET | Reefer pre-trip inspection | Container reference | For depots/M&R suppliers |
| HL LIVE Subscription v3.0.7 | Various | Reefer cold chain monitoring | Subscription-based | Requires commercial contract; reefer-only |
| Live Position Subscription v1.0.6 | Various | Container GPS tracking | Smart containers only | Requires commercial contract |
| Live Position Events | Various | GPS event data | Smart containers only | Requires commercial contract |

### Lookup Methods Summary

| Identifier Type | Supported? | Which Endpoints? | Notes |
|----------------|-----------|-----------------|-------|
| **Bill of Lading (B/L) number** | ✅ | TNT Events via `transportDocumentReference` | B/L = Transport Document Reference in DCSA terminology |
| **Booking reference** | ✅ | TNT Events via `carrierBookingReference` | Returns events for all containers under booking |
| **Container number** | ✅ | TNT Events via `equipmentReference` | Follows BIC ISO 6346 format (e.g., `HLCU1234567`) |
| **Carrier booking number** | ✅ | Same as booking reference above | HL uses `carrierBookingReference` |
| **Vessel IMO / voyage** | ⚠️ | TNT Events — as filter only, not as primary lookup | `vesselIMONumber` is not a documented query param on the events endpoint; use `exportVoyageNumber` filter in combination with another primary identifier |

---

## Rate Limits & Quotas

| Detail | Value | Source |
|--------|-------|--------|
| **Global rate limit** | Tiered — see below | Official ([TNT API docs on api-portal.hlag.com](https://api-portal.hlag.com)) |
| **Tryout tier** | 100 calls/day, 10 calls/minute | Official |
| **Default tier** | 6,000 calls/day, 10 calls/minute | Official |
| **Premium tier** | 100,000 calls/day, 150 calls/minute | Official |
| **Per-endpoint limits** | Not documented separately; likely same tiers apply to all endpoints in a product | Official |
| **Rate limit response** | HTTP 429 (Too Many Requests) | Official (from OpenAPI spec `429` response definition) |
| **Rate limit by** | API key (Client ID) — assumed per-application | Estimated (unverified) |
| **Burst allowance** | Unknown | Unknown |
| **Tier upgrade process** | Unknown — likely through portal subscription upgrade or contacting HL | Estimated (unverified) |

---

## Webhook / Push Support

| Detail | Value |
|--------|-------|
| **Webhooks supported?** | No — not yet for Track & Trace |
| **Official statement** | FAQ: "Do you offer a notification service for the DCSA Track & Trace events that pushes data to my system?" → "Not yet, but please observe the release notes for changes." ([TNT API docs](https://api-portal.hlag.com)) |
| **HL LIVE push** | Yes — but only for reefer/cold chain monitoring, requires separate commercial contract |
| **Rate Sheet Notifications** | Yes — callback-based push for rate sheet changes. Uses `POST /notify` callback with `X-API-Key`, `X-Request-ID`, `X-Idempotency-Key` headers ([GitHub: customer-api-definitions](https://github.com/Hapag-Lloyd/customer-api-definitions)) |

> **Implication for SSL**: Polling-only strategy required for shipment tracking. Use `eventCreatedDateTime:gte` filter for efficient incremental polling. Webhook support may be added in future releases.

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | [https://www.hapag-lloyd.com/en/tracking.html](https://www.hapag-lloyd.com/en/tracking.html) |
| **Login required?** | No (basic tracking); Yes (full features) |
| **Data available on portal but NOT in API** | Per HL's own FAQ: "We're including additional data sources for the API to better reflect the changes and align with the website view. We encourage you to trust the website data until our next release." This implies the portal currently shows more complete data than the API |
| **Scraping feasibility** | Difficult — behind Cloudflare challenge (403 responses to curl, JS challenge required) |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Yes |
| **EDI message types** | Standard EDIFACT messages (IFTMIN, COPARN, BAPLIE, IFTSTA) — typical for major carriers |
| **EDI connection method** | Contact carrier for EDI setup |
| **EDI documentation** | Contact carrier: [https://www.hapag-lloyd.com/en/services-information/offices-localinfo.html](https://www.hapag-lloyd.com/en/services-information/offices-localinfo.html) |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Yes | Hapag-Lloyd is a major global carrier in project44's network |
| **FourKites** | Yes (estimated) | Major carrier — highly likely in FourKites network |
| **Vizion** | Yes (estimated) | Major carrier — highly likely in Vizion network |
| **INTTRA / E2open** | Yes | Hapag-Lloyd is connected to INTTRA platform |
| **CargoSmart** | Yes | CargoSmart website accessible and HL is a major carrier |

> **Aggregator note**: Given that the HL Track & Trace API is still in BETA with acknowledged data gaps vs. the web portal, aggregators like project44 may provide more complete tracking data in the near term, potentially sourced from EDI or direct partnerships rather than the public API.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown — not documented | Unknown |
| **API uptime/reliability** | Unknown — no published SLA; API is labeled BETA | Unknown |
| **Historical data depth** | Unknown — not documented | Unknown |
| **Timezone handling** | ISO 8601 with timezone offsets (`eventDateTime` is local date/time per spec) | Official (OpenAPI spec) |
| **Character encoding** | UTF-8 (JSON response) | Official |

### Known Issues & Gotchas

- **⚠️ BETA STATUS**: The Track & Trace API is explicitly labeled as a BETA version. From the API description: "Please note that the Track & Trace API is currently available only as a BETA version. The solution is still in development and will undergo changes and improvements." This means the API may change without notice.
- **⚠️ DATA DISCREPANCIES**: Hapag-Lloyd's own FAQ acknowledges that the API may show different data from the website: "We're including additional data sources for the API to better reflect the changes and align with the website view. We encourage you to trust the website data until our next release."
- **⚠️ LIMITED SHIPMENT EVENT CODES**: Only `ISSU` (Issued) and `CONF` (Confirmed) are supported for `shipmentEventTypeCode`. DCSA standard includes many more (RECE, DRFT, PENA, APPR, CANC, REJE, RELS, PENU). This limits booking lifecycle visibility.
- **⚠️ LIMITED DOCUMENT TYPE CODES**: Only `BKG` (Booking) and `TRD` (Transport Document) are supported for `documentTypeCode`. Missing `SHI` (Shipping Instructions).
- **NO WEBHOOK SUPPORT**: Push/event subscriptions are not available for Track & Trace. Polling only.
- **PAGINATION**: Uses `limit` parameter only (no offset/cursor documented). Default page size is 100. No `next` link or cursor mechanism visible in the spec — may return all matching events up to limit, requiring `eventCreatedDateTime` filtering for pagination.
- **SORT**: Supports field-based sorting with `:ASC`/`:DESC` suffix (e.g., `carrierBookingReference:DESC`).
- **NO `isTransshipmentMove` FIELD**: Unlike some DCSA implementations, transshipment moves are not explicitly flagged. Must be inferred from location matching against the transport plan.
- **IBM API CONNECT**: The API gateway is IBM API Connect (indicated by `X-IBM-Client-*` headers). This is relevant for error handling — IBM gateway errors may differ from application errors.
- **⚠️ MOCK SERVER DATA FORMAT MISMATCH**: The mock endpoint at `mock.api-portal.hlag.com` returns events in an older v1.x-style format that differs significantly from the v2.2.4 OpenAPI spec: uses flat `eventTypeCode` (e.g., `"eventTypeCode":"GTOT"`) instead of separate `equipmentEventTypeCode`/`transportEventTypeCode` fields; uses `shipmentINformationTypeCode` (note casing anomaly) instead of `shipmentEventTypeCode`; returns simple `transportCallID: 6` instead of embedded `transportCall` objects. Developers building against the mock will produce code that does not work with the real v2.2.4 API. Use the mock only for connectivity/auth testing, not for response-structure development.

### Recently Deprecated or Changed

- `transportCallID` field on Transport and Equipment events is deprecated: "not needed as the TransportCall object is included" — use embedded `transportCall` object instead.
- TNT API v2.2.2 was Pilot Test (May 2025); current version is v2.2.4.

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | Yes — comprehensive DCSA TNT v2 event data covering all core container milestones and transport events |
| **Implementation effort** | Medium (DCSA TNT v2 with minor deviations — limited ShipmentEvent codes, no isTransshipmentMove, beta caveats) |
| **DCSA base adapter usable?** | Yes with overrides — core event model follows DCSA TNT v2 closely, but ShipmentEvent deviations and missing fields need adapter-level handling |

### Recommended Approach

The Hapag-Lloyd adapter should extend the DCSA base adapter class since the TNT API closely follows DCSA Track & Trace v2.2. The primary tracking endpoint (`GET https://api.hlag.com/hlag/external/v2/events/`) returns standard DCSA event objects (EQUIPMENT, TRANSPORT, SHIPMENT) with standard codes and classifiers.

Key customizations needed:
1. **Authentication**: Implement IBM API Connect API Key auth (simple `X-IBM-Client-Id` + `X-IBM-Client-Secret` headers — no OAuth2 flow needed).
2. **ShipmentEvent mapping**: Handle the limited `shipmentEventTypeCode` values (only ISSU, CONF).
3. **Transshipment detection**: Implement logic to identify transshipment moves by comparing event locations against the transport plan, since `isTransshipmentMove` is not available.
4. **Cutoff data**: Integrate with the Commercial Schedules API for cutoff data, once authenticated access is available to verify endpoint paths.
5. **Beta handling**: Implement fallback/retry logic and expect occasional data inconsistencies per HL's own advisory.

### Recommended Lookup Method

**Carrier Booking Reference** (`carrierBookingReference`) is the recommended primary lookup method. It returns events for all containers under a booking, including transport and shipment events. For single-container tracking, use `equipmentReference`. For B/L tracking, use `transportDocumentReference`.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Every 2-4 hours for active shipments (limited by Tryout/Default tier rate limits) |
| **Incremental filter** | Use `eventCreatedDateTime:gte={lastPollTime}` for efficient incremental polling |
| **Batch tracking** | One API call per shipment identifier. No documented batch/multi-shipment endpoint |

**Rate limit math (Default tier)**:
- 6,000 calls/day = 250 calls/hour
- At 4 calls per shipment check (one per lookup + retries), can track ~62 shipments per hour
- With 2-hour polling: ~125 active shipments supported on Default tier
- Premium tier (100K/day): ~2,000+ active shipments with 2-hour polling

### Auth Implementation Notes

Authentication is straightforward — no OAuth2 token dance required. Simply include `X-IBM-Client-Id` and `X-IBM-Client-Secret` headers on every request. Credentials are obtained by registering at [api-portal.hlag.com](https://api-portal.hlag.com), creating an Application, and subscribing to the desired API product.

For the SDK adapter:
```typescript
// Simple header injection — no token refresh needed
const headers = {
  'X-IBM-Client-Id': credentials.clientId,
  'X-IBM-Client-Secret': credentials.clientSecret,
  'Accept': 'application/json',
};
```

### Edge Cases to Handle

- **Transshipment identification**: No `isTransshipmentMove` flag — must compare `transportCall.UNLocationCode` against the known route to determine if a LOAD/DISC event is at a transshipment port.
- **Data freshness mismatch**: API data may lag behind website data per HL's own advisory. Consider surfacing a "beta data" warning to consumers.
- **Limited ShipmentEvent types**: Only `ISSU` and `CONF`. Don't expect full booking lifecycle tracking (no RECE, DRFT, CANC, REJE events).
- **Multi-container bookings**: Querying by `carrierBookingReference` returns events for all containers — adapter should group events by `equipmentReference`.
- **Pagination edge case**: With only `limit` parameter and no cursor, large result sets may require filtering by `eventCreatedDateTime` ranges to avoid missing events beyond the limit.
- **BETA instability**: API may return unexpected data or change behavior between versions. Implement defensive parsing.

### Mapping Complexity

**Low-Medium**. The response format closely follows DCSA TNT v2 event model:
- Equipment events have standard `equipmentEventTypeCode` + `emptyIndicatorCode` + `transportCall` structure.
- Transport events have standard `transportEventTypeCode` + `eventClassifierCode` + `transportCall` structure.
- Location data uses standard `UNLocationCode` + nested `location` object.
- Vessel data includes `vesselIMONumber` + `vesselName`.

The main mapping challenges are:
1. Inferring transshipment status without `isTransshipmentMove`.
2. Handling the limited set of ShipmentEvent types.
3. Merging cutoff data from the Commercial Schedules API with tracking data from the TNT API (two different API products, potentially requiring two subscriptions).

---

## Open Questions

- [ ] **What tier does SSL get by default?** — Tryout (100/day) is very restrictive. Need to verify the process for upgrading to Default or Premium tier.
- [ ] **Commercial Schedules API endpoint paths?** — The public API listing didn't expose endpoint paths for the Schedules API. Need authenticated access to document the exact paths and confirm cutoff field availability.
- [ ] **When will TNT exit BETA?** — The API has been in beta/pilot since at least May 2025. The timeline for GA (general availability) would affect how much SSL should rely on it.
- [ ] **Historical data depth?** — How far back can events be queried? Critical for initial data backfill when onboarding existing shipments.
- [ ] **Does SSL have an existing Hapag-Lloyd business relationship?** — May simplify API access tier negotiation.
- [ ] **Is `vesselIMONumber` a supported query filter?** — The Ruby gem client lists it as a filter, but it's not in the primary Events endpoint query parameters in the OpenAPI spec from the portal.
- [ ] **`carrierServiceCode` filter?** — Referenced in the getting-started docs but not in the OpenAPI parameters section.
- [ ] **Are retracted events and delay reason codes supported?** — DCSA standard includes `retractedEventID`, `changeRemark`, and `delayReasonCode`, but these fields are absent from the public spec. May be implemented but not documented.
- [ ] **Webhook timeline?** — FAQ says "not yet" — is there a roadmap date?
- [ ] **Rate limit enforcement behavior?** — Does the 429 response include a `Retry-After` header? Per-key or per-IP?
- [ ] **Live testing with sandbox?** — The mock endpoint at `mock.api-portal.hlag.com` exists. What test data is available? Does it simulate realistic event sequences?

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | [https://www.hapag-lloyd.com](https://www.hapag-lloyd.com) |
| Developer Portal | [https://api-portal.hlag.com](https://api-portal.hlag.com) |
| API Catalog (public) | `https://api-portal.hlag.com/v1/apis` (returns JSON array of all API specs) |
| TNT API Base URL | `https://api.hlag.com/hlag/external/v2/events` |
| TNT Mock/Sandbox | `https://mock.api-portal.hlag.com/v2/events` |
| Portal Terms of Service | [https://api-portal.hlag.com/terms](https://api-portal.hlag.com/terms) |
| Portal Privacy Policy | [https://api-portal.hlag.com/privacy](https://api-portal.hlag.com/privacy) |
| Official GitHub (customer-api-definitions) | [https://github.com/Hapag-Lloyd/customer-api-definitions](https://github.com/Hapag-Lloyd/customer-api-definitions) |
| Rate Sheet Notification OpenAPI Spec | [https://github.com/Hapag-Lloyd/customer-api-definitions/blob/main/src/main/openapi/ratesheet/v1/subscription_callback.yaml](https://github.com/Hapag-Lloyd/customer-api-definitions/blob/main/src/main/openapi/ratesheet/v1/subscription_callback.yaml) |
| Community: Python SDK (PyPI) | [https://pypi.org/project/hapag-lloyd-sdk/](https://pypi.org/project/hapag-lloyd-sdk/) |
| Community: Python SDK (GitHub) | ~~[https://github.com/gedankenfabrik/hapag_lloyd_sdk](https://github.com/gedankenfabrik/hapag_lloyd_sdk)~~ — **⚠️ Returns 404** (deleted or private as of Feb 2026). PyPI package [`hapag-lloyd-sdk`](https://pypi.org/project/hapag-lloyd-sdk/) v0.2.1 still available. |
| Community: Ruby Client (GitHub) | [https://github.com/Cellpap/hapag-lloyd_client](https://github.com/Cellpap/hapag-lloyd_client) |
| DCSA About (confirms founding member) | [https://dcsa.org/about-us/](https://dcsa.org/about-us/) |
| DCSA TNT v2 Information Model | [https://dcsa.org/wp-content/uploads/2021/10/202108_DCSA_P1_Information-Model-v3.3_TNT22_Final.pdf](https://dcsa.org/wp-content/uploads/2021/10/202108_DCSA_P1_Information-Model-v3.3_TNT22_Final.pdf) |
| Web Portal Tracking | [https://www.hapag-lloyd.com/en/tracking.html](https://www.hapag-lloyd.com/en/tracking.html) |
| Sales Offices (for HL LIVE / EDI) | [https://www.hapag-lloyd.com/en/services-information/offices-localinfo.html](https://www.hapag-lloyd.com/en/services-information/offices-localinfo.html) |
