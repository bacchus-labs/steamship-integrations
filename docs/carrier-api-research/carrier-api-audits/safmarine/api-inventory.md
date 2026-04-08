# Safmarine -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing. Safmarine was fully integrated into Maersk Line in 2020. All API access is through Maersk's developer portal and APIs. Research based on Maersk API documentation, maersk.com/safmarine integration page, third-party aggregator listings, DCSA membership records, and community resources.
> **Researched by**: Agent (carrier API audit workflow)
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | Safmarine (formerly South African Marine Corporation, Ltd.) |
| **SCAC Code** | SAFM |
| **Parent Company** | A.P. Moller-Maersk A/S (acquired 1999; brand retired and fully integrated into Maersk Line end of 2020) |
| **Alliance** | Maersk (subsidiary) -- currently operating under Gemini Cooperation (with Hapag-Lloyd); formerly 2M (with MSC, ended Jan 2025) |
| **Primary Services** | Container shipping (historically specialized in Africa, South America, and Indian Subcontinent trades) |
| **Market Position** | Retired brand -- all operations absorbed into Maersk Line. Safmarine's SCAC (SAFM) persists in legacy B/L numbers and industry systems but no longer represents independent operations |
| **Headquarters** | Antwerp, Belgium (historical); now Maersk HQ in Copenhagen, Denmark |
| **Website** | [https://www.maersk.com/safmarine](https://www.maersk.com/safmarine) (integration/transition page) |

### Brand Integration Status

Safmarine was acquired by A.P. Moller-Maersk in 1999 but operated as a distinct brand with its own booking, tracking, and customer portals until 2020. In September 2020, Maersk announced the retirement of the Safmarine brand (along with Damco), effective end of 2020:

- **October 31, 2020**: Spot quote and booking requests ended on safmarine.com
- **December 31, 2020**: All safmarine.com bookings ceased
- **Post-2020**: All shipment management migrated to maersk.com; Safmarine credentials work on maersk.com

Source: [maersk.com/safmarine](https://www.maersk.com/safmarine), [FreightWaves](https://www.freightwaves.com/news/why-maersk-axed-safmarine-and-damco-and-whats-next), [Seatrade Maritime](https://www.seatrade-maritime.com/containers/maersk-retiring-safmarine-and-damco-brands)

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | **No** (own portal). Uses Maersk's developer portal |
| **Developer portal URL** | [https://developer.maersk.com](https://developer.maersk.com) (Maersk shared portal) |
| **API documentation URL(s)** | [https://developer.maersk.com/api-catalogue](https://developer.maersk.com/api-catalogue) (Maersk API catalogue) |
| **Documentation quality** | Excellent (Maersk's documentation) -- no Safmarine-specific documentation exists |
| **OpenAPI/Swagger spec available?** | Yes -- via Maersk/DCSA standard specs at [github.com/dcsaorg/DCSA-OpenAPI](https://github.com/dcsaorg/DCSA-OpenAPI) and Maersk's portal |
| **Sandbox/test environment?** | Yes -- via Maersk's sandbox (requires developer.maersk.com registration) |
| **Developer registration** | Free self-service at [developer.maersk.com](https://developer.maersk.com) |
| **Developer support channels** | Maersk developer portal support, [status.maersk.com](https://status.maersk.com) |
| **Community/third-party libraries** | None specific to Safmarine. Maersk libraries are minimal (see Maersk inventory) |
| **API changelog / release notes** | Via Maersk developer portal (requires login) |

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | No (Safmarine is not independently a DCSA member). Maersk is a DCSA founding member; DCSA compliance is inherited through Maersk's infrastructure |
| **DCSA APIs implemented** | Via Maersk: TNT (Track & Trace), BKG (Booking), CS (Commercial Schedules) |
| **DCSA TNT version** | Via Maersk: v2 and v3 (both live -- `/synergy/tracking/v2/events` and `/track-and-trace/v3/events`) |
| **DCSA Booking version** | Via Maersk: v2.x |
| **DCSA Schedules version** | Via Maersk: v1.x |
| **Known DCSA deviations** | Same as Maersk -- see Maersk API inventory for details. Key: dual auth pattern (OAuth2 for some paths, API Key for others) |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Yes | Via Maersk EDI infrastructure. IFTMIN, IFTSTA, COPARN, BAPLIE supported |
| **INTTRA integration** | Yes | Via Maersk on INTTRA/E2open platform |
| **BIC (Bureau International des Containers)** | Yes | Standard container ID format used throughout Maersk APIs |
| **UN/LOCODE** | Yes | UNLocationCode used in all Maersk DCSA endpoints |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | Dual: OAuth2 Client Credentials (for `/synergy/` and `/v1/` paths) + API Key Consumer-Key header (for `/track-and-trace/` and `/schedules/` paths) -- same as Maersk |
| **Auth documentation** | [developer.maersk.com](https://developer.maersk.com) (authentication section, requires login) |
| **Registration process** | 1. Visit developer.maersk.com 2. Create free developer account 3. Register an application to obtain API key / client credentials |
| **Registration URL** | [https://developer.maersk.com](https://developer.maersk.com) |
| **Partner program required?** | No -- basic API access is self-service. Same as Maersk |
| **Partner program URL** | N/A for basic access |
| **Credential type** | Consumer-Key (API Key) for most endpoints; Client ID + Client Secret for OAuth2 endpoints |
| **Token refresh supported?** | Yes -- OAuth2 client_credentials flow; refresh by re-requesting |
| **Token lifetime** | Estimated ~1 hour (unverified -- same as Maersk estimate) |
| **Access tiers** | Same as Maersk: Basic (self-service, standard rate limits) and Partner/Enterprise (elevated limits) |
| **IP whitelisting required?** | No -- Maersk APIs have `access-control-allow-origin: *` |

### Access Requirements Summary for SSL

Safmarine shipments are accessed entirely through Maersk's API infrastructure. SSL needs the same credentials used for Maersk:

1. Register a free developer account at [developer.maersk.com](https://developer.maersk.com) (self-service, no business relationship needed)
2. Create an application to obtain a Consumer-Key and/or OAuth2 client credentials
3. Use the same API endpoints as for Maersk tracking -- Safmarine B/L numbers (SAFM prefix) and containers should be queryable through Maersk's tracking API

**Open question**: Whether the Maersk API accepts `safm` as a `brandScac` value, or whether Safmarine shipments are simply returned under the `maeu` brand code. This requires live testing.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field must have a row.
> Coverage below reflects Maersk API capabilities, since Safmarine shipments are served through Maersk's infrastructure.

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ✅ | `GET /schedules/v1/vessel-schedules`, `GET /schedules/v1/port-schedules` | VesselSchedule, PortSchedule | DCSA CS v1 | Via Maersk Schedules API |
| 1.2 | Point-to-Point Route Options | ✅ | `GET /schedules/v1/point-to-point-routes` | PointToPointRoute with legs[], transitTime, cutOffTimes[] | DCSA CS v1 | Via Maersk Schedules API |
| 1.3 | Booking Lifecycle | ✅ | `GET/POST /booking/v2/bookings` (Maersk path) | Booking with transportPlan[], shipmentCutOffTimes[] | DCSA BKG v2 | Via Maersk Booking API |
| 1.4 | Shipping Instructions | ⚠️ | Likely via Maersk eDocumentation endpoints | ShipmentEvent with documentTypeCode=SHI | DCSA EDoc | Available through Maersk but unconfirmed for Safmarine-branded shipments |
| 1.5 | Rates | ✅ | `GET /rates/` (Maersk path) | Proprietary | Not DCSA | Maersk Spot Rate API -- unclear if Safmarine-specific rates are available post-brand retirement |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ✅ | Booking confirmation / Schedules P2P response | cutOffDateTimeCode: "ECP" | `ECP` | Via Maersk -- in shipmentCutOffTimes[] |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ✅ | Booking confirmation / Schedules P2P response | cutOffDateTimeCode: "EFC" | `EFC` | Via Maersk |
| 2.3 | Documentation Cutoff | DCO | ✅ | Booking confirmation / Schedules P2P response | cutOffDateTimeCode: "DCO" | `DCO` | Via Maersk |
| 2.4 | VGM Cutoff | VCO | ✅ | Booking confirmation / Schedules P2P response | cutOffDateTimeCode: "VCO" | `VCO` | Via Maersk |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ✅ | Booking confirmation / Schedules P2P response | cutOffDateTimeCode: "FCO" | `FCO` | Via Maersk |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ⚠️ | Booking confirmation / Schedules P2P response | cutOffDateTimeCode: "LCO" | `LCO` | Via Maersk. Conditional: only present when receiptTypeAtOrigin = "CFS" |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ✅ | `GET /track-and-trace/v3/events` or `GET /synergy/tracking/v2/events` | Presence of first EquipmentEvent for booking ref | Inferred from first EquipmentEvent | Via Maersk TNT |
| 3.2 | Empty Container Gate-Out (Pickup) | ✅ | `GET /track-and-trace/v3/events` | GTOT + EMPTY | `GTOT` + `EMPTY` | Via Maersk TNT |
| 3.3 | Full Container Gate-In | ✅ | `GET /track-and-trace/v3/events` | GTIN + LADEN | `GTIN` + `LADEN` | Via Maersk TNT |
| 3.4 | Container Loaded on Vessel | ✅ | `GET /track-and-trace/v3/events` | LOAD + LADEN | `LOAD` + `LADEN` | Via Maersk TNT |
| 3.5 | Container Discharged at Transshipment | ✅ | `GET /track-and-trace/v3/events` | DISC + LADEN + isTransshipmentMove:true | `DISC` + `LADEN` + transshipment | Via Maersk TNT |
| 3.6 | Container Loaded at Transshipment | ✅ | `GET /track-and-trace/v3/events` | LOAD + LADEN + isTransshipmentMove:true | `LOAD` + `LADEN` + transshipment | Via Maersk TNT |
| 3.7 | Container Discharged at Destination | ✅ | `GET /track-and-trace/v3/events` | DISC + LADEN + isTransshipmentMove:false at destination | `DISC` + `LADEN` | Via Maersk TNT |
| 3.8 | Full Container Gate-Out (Delivery) | ✅ | `GET /track-and-trace/v3/events` | GTOT + LADEN | `GTOT` + `LADEN` | Via Maersk TNT |
| 3.9 | Empty Container Returned | ✅ | `GET /track-and-trace/v3/events` | GTIN + EMPTY | `GTIN` + `EMPTY` | Via Maersk TNT |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ✅ | `GET /track-and-trace/v3/events` | TransportEvent: DEPA + EST/PLN/ACT | `DEPA` + classifier | Via Maersk TNT |
| 4.2 | Estimated Time of Arrival | ETA | ✅ | `GET /track-and-trace/v3/events` | TransportEvent: ARRI + EST/PLN/ACT | `ARRI` + classifier | Via Maersk TNT |
| 4.3 | Vessel Arrival at Transshipment | -- | ✅ | `GET /track-and-trace/v3/events` | TransportEvent: ARRI at intermediate port | `ARRI` at intermediate | Via Maersk TNT |
| 4.4 | Vessel Departure from Transshipment | -- | ✅ | `GET /track-and-trace/v3/events` | TransportEvent: DEPA at intermediate port | `DEPA` at intermediate | Via Maersk TNT |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ✅ | Via Maersk: `POST /track-and-trace/v3/event-subscriptions` with callbackUrl |
| Event Polling with timestamp filter | ✅ | Via Maersk: `GET /track-and-trace/v3/events` with eventCreatedDateTime filter |
| Event Classifier Progression (PLN->EST->ACT) | ✅ | DCSA standard progression supported through Maersk |
| Retracted Events | ✅ | Via Maersk: metadata.retractedEventID field |
| Change Remarks | ✅ | Via Maersk: changeRemark field on TransportEvents |
| Delay Reason Codes | ✅ | Via Maersk: delayReasonCode on TransportEvents (DCSA codes) |

### Coverage Summary

| Category | Fields Available | Fields Partial | Fields Unavailable | Fields Unknown | Coverage % |
|----------|-----------------|---------------|-------------------|----------------|-----------|
| API Domains (1.x) | 4/5 | 1/5 | 0/5 | 0/5 | 80% |
| Cutoffs (2.x) | 5/6 | 1/6 | 0/6 | 0/6 | 83% |
| Container Milestones (3.x) | 9/9 | 0/9 | 0/9 | 0/9 | 100% |
| Transport Events (4.x) | 4/4 | 0/4 | 0/4 | 0/4 | 100% |
| Change Detection (5.x) | 6/6 | 0/6 | 0/6 | 0/6 | 100% |
| **Total** | **28/30** | **2/30** | **0/30** | **0/30** | **93%** |

> **Note**: The 2 partial fields (1.4 Shipping Instructions, 2.6 LCL Cutoff) are available through Maersk's infrastructure but marked as partial because Safmarine-specific behavior is unverified. Effective coverage through Maersk's APIs is likely 30/30 once live testing confirms Safmarine B/L compatibility.

---

## Endpoint Reference

Safmarine has no independent endpoints. All endpoints below are Maersk's APIs, which serve Safmarine shipment data.

### Tracking / Events

| Endpoint | Method | Lookup Params | Pagination | Response Format | Notes |
|----------|--------|--------------|------------|----------------|-------|
| `/track-and-trace/v3/events` | GET | B/L (documentReference), Booking (documentReference), Container (equipmentReference) | cursor | JSON (DCSA TNT v3) | Primary tracking endpoint. Auth: Consumer-Key header |
| `/synergy/tracking/v2/events` | GET | B/L, Booking, Container | cursor | JSON (DCSA TNT v2) | Legacy v2 endpoint. Auth: OAuth2 Bearer token |
| `/track-and-trace/v3/event-subscriptions` | POST | Subscription filters: eventType, documentReference, equipmentReference | N/A | JSON | Webhook subscription creation. Auth: Consumer-Key header |

### Schedules

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| `/schedules/v1/vessel-schedules` | GET | vesselIMONumber, vesselName, carrierVoyageNumber | cursor | JSON (DCSA CS v1) | Auth: Consumer-Key header |
| `/schedules/v1/port-schedules` | GET | UNLocationCode, facilityCode, dateRange | cursor | JSON (DCSA CS v1) | Auth: Consumer-Key header |
| `/schedules/v1/point-to-point-routes` | GET | originUNLocationCode, destinationUNLocationCode, departureDate | cursor | JSON (DCSA CS v1) | Returns routing options with cutoffs |

### Booking

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| `/booking/v2/bookings` | GET/POST | Booking reference | cursor | JSON (DCSA BKG v2) | Booking path confirmed on Maersk but exact prefix unverified |

### Other Endpoints

| Endpoint | Method | Purpose | Key Params | Notes |
|----------|--------|---------|-----------|-------|
| `/rates/` | GET | Spot rates | Origin, destination, container type | Proprietary (not DCSA). Auth: Consumer-Key |
| `/ecommerce/tracking/` | GET | Simplified tracking | Tracking number | Maersk e-commerce tracking endpoint |
| `/oauth2/access_token` | POST | OAuth2 token | client_id, client_secret, grant_type=client_credentials | Token endpoint for OAuth2-authenticated paths |

### Lookup Methods Summary

| Identifier Type | Supported? | Which Endpoints? | Notes |
|----------------|-----------|-----------------|-------|
| **Bill of Lading (B/L) number** | ✅ | Track & Trace v2/v3 | SAFM-prefixed B/L numbers expected to work through Maersk API (unverified) |
| **Booking reference** | ✅ | Track & Trace v2/v3, Booking API | Via documentReference parameter |
| **Container number** | ✅ | Track & Trace v2/v3 | Via equipmentReference parameter |
| **Carrier booking number** | ✅ | Track & Trace, Booking | Same as booking reference for Maersk |
| **Vessel IMO / voyage** | ✅ | Schedules API | vesselIMONumber + carrierVoyageNumber |

---

## Rate Limits & Quotas

| Detail | Value | Source |
|--------|-------|--------|
| **Global rate limit** | Unpublished -- same as Maersk | Unknown |
| **Per-endpoint limits** | Unpublished | Unknown |
| **Daily/monthly quota** | Unpublished | Unknown |
| **Rate limit response** | Likely 429 with Retry-After header (standard pattern) | Estimated |
| **Rate limit by** | API key / OAuth token (likely) | Estimated |
| **Burst allowance** | Unknown | Unknown |
| **Different tiers** | Basic (self-service) and Partner/Enterprise reported for Maersk | Reported |

---

## Webhook / Push Support

| Detail | Value |
|--------|-------|
| **Webhooks supported?** | Yes (via Maersk) |
| **Subscription endpoint** | `POST /track-and-trace/v3/event-subscriptions` |
| **Subscription management** | Create/list/delete via API |
| **Subscribable event types** | Equipment events, Transport events, Shipment events -- filterable by type, booking ref, equipment ref |
| **Callback format** | DCSA event JSON POSTed to callbackUrl |
| **Callback authentication** | Shared secret in header (details via Maersk portal) |
| **Retry policy on failure** | Unknown -- likely standard retry with backoff |
| **Documented reliability** | No published SLA specific to webhooks |

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | [https://www.maersk.com/tracking](https://www.maersk.com/tracking) (primary). Legacy safmarine.com redirects to maersk.com/safmarine |
| **Login required?** | No (basic tracking). Login required for full shipment details |
| **Data available on portal but NOT in API** | None known -- Maersk portal and API coverage align |
| **Scraping feasibility** | Not recommended -- Maersk portal is an SPA (JavaScript-rendered); API access is superior |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Yes -- via Maersk EDI infrastructure |
| **EDI message types** | IFTMIN, IFTSTA, COPARN, BAPLIE (and other EDIFACT types) |
| **EDI connection method** | Via Maersk EDI services |
| **EDI documentation** | [developer.maersk.com/support/getting-started-edi](https://developer.maersk.com/support/getting-started-edi) |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Yes (likely) | project44 covers 98%+ of global ocean freight. Safmarine not explicitly listed but Maersk is a major partner |
| **FourKites** | Yes (likely) | FourKites tracks all major carriers including Maersk. Safmarine data flows through Maersk |
| **Vizion** | Yes | [vizionapi.com/carrier-tracking/safmarine](https://www.vizionapi.com/carrier-tracking/safmarine) -- explicitly lists Safmarine |
| **INTTRA / E2open** | Yes | Maersk (including former Safmarine operations) available through INTTRA platform |
| **CargoSmart** | Unknown | No specific Safmarine listing found |
| **Terminal49** | Yes | [terminal49.com/shipping-lines/safm](https://terminal49.com/shipping-lines/safm-safmarine-container-line-container-tracking) -- B/L and booking tracking supported |
| **Portcast** | Yes | [portcast.io/carrier-coverage/safmarine](https://www.portcast.io/carrier-coverage/safmarine-container-line-tracking) |

> **Aggregator note**: Since Safmarine shipments flow through Maersk's infrastructure, aggregators that support Maersk effectively support Safmarine. Direct API integration via Maersk is the recommended approach rather than going through an aggregator.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Same as Maersk -- likely < 15 min for most events | Estimated (based on Maersk behavior) |
| **API uptime/reliability** | Maersk publishes API status at [developer.maersk.com/api-status](https://developer.maersk.com/api-status) and [status.maersk.com](https://status.maersk.com) | Official (Maersk) |
| **Historical data depth** | Unknown -- same as Maersk (likely 90+ days) | Unknown |
| **Timezone handling** | UTC (DCSA standard) | Official (DCSA spec) |
| **Character encoding** | UTF-8 | Official (DCSA spec) |

### Known Issues & Gotchas

- **Brand code uncertainty**: It is unverified whether the Maersk API accepts `safm` as a `brandScac` value. Legacy Safmarine B/L numbers should work as `documentReference` in tracking queries, but this needs live testing.
- **Retired brand confusion**: Some legacy systems and aggregators still reference Safmarine as a separate carrier. The SDK must handle SAFM SCAC code lookups by routing them through the Maersk adapter.
- **Dual auth pattern**: Same as Maersk -- different endpoints use different auth mechanisms (OAuth2 vs. API Key). See Maersk inventory for details.
- **Historical shipments**: Safmarine shipments booked before the 2020 brand retirement may have different data structures or limited availability depending on Maersk's data migration completeness.

### Recently Deprecated or Changed

- **Safmarine.com portal**: Deprecated end of 2020. Redirects to maersk.com/safmarine.
- **Safmarine booking system**: Ceased December 31, 2020. All bookings through maersk.com.
- **Safmarine Track & Trace**: Legacy tracking was maintained during transition but now redirects to Maersk tracking.

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | Yes -- by reusing the Maersk adapter entirely |
| **Implementation effort** | Very Low (alias/configuration on Maersk adapter) |
| **DCSA base adapter usable?** | Yes -- Maersk's DCSA implementation is the underlying infrastructure |

### Recommended Approach

The Safmarine SDK adapter should be a **thin alias/configuration layer on top of the Maersk adapter**. Since Safmarine's entire digital infrastructure has been absorbed into Maersk since 2020, there is no separate API to integrate with. The adapter should:

1. Register SAFM as a recognized SCAC code in the carrier registry
2. Route all API calls through the Maersk adapter (same endpoints, same auth, same response parsing)
3. If the Maersk API supports a `brandScac=safm` parameter, use it to filter results. If not, simply query using the Safmarine B/L number or container number directly.

This is functionally identical to how Hamburg Sud (SUDU) and Sealand (SEJJ) should be handled -- all are Maersk subsidiaries using the same API infrastructure.

### Recommended Lookup Method

**Bill of Lading number** is the recommended primary lookup. Safmarine B/L numbers use the SAFM prefix (e.g., SAFM12345678), which should be accepted by Maersk's tracking API as a `documentReference`. Container numbers are the secondary lookup method.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Every 2 hours (same as Maersk recommendation) |
| **Incremental filter** | Use `eventCreatedDateTime > lastPollTime` for incremental polling |
| **Batch tracking** | One call per shipment (DCSA pattern). Multiple shipments require multiple calls |

### Auth Implementation Notes

Identical to Maersk. The adapter should share the same credential store and token cache:

- **Consumer-Key header** for `/track-and-trace/` and `/schedules/` endpoints
- **OAuth2 Bearer token** (client_credentials flow via `POST /oauth2/access_token`) for `/synergy/` endpoints
- Token caching: reuse tokens until expiry (estimated ~1 hour)

### Edge Cases to Handle

- **SCAC routing**: When a tracking request comes in with SCAC=SAFM, the adapter must internally route to the Maersk adapter
- **Legacy B/L format**: Safmarine B/L numbers (SAFM prefix) should be passed directly as documentReference to the Maersk API
- **Brand code handling**: If Maersk API requires/supports brandScac, test whether `safm` is a valid value. Fall back to `maeu` if not
- **Historical data gap**: Very old Safmarine shipments (pre-2020 migration) may have incomplete data in Maersk's system

### Mapping Complexity

**Minimal to none.** Since the Safmarine adapter is a pure alias for the Maersk adapter, no mapping is required. The response format from Maersk's DCSA-compliant APIs is already the canonical model. The only "mapping" needed is at the carrier registry level: SAFM SCAC -> Maersk adapter.

---

## Open Questions

- [ ] Does the Maersk API accept `safm` as a valid `brandScac` value, or are Safmarine shipments simply returned under `maeu`?
- [ ] Can Safmarine-prefixed B/L numbers (e.g., SAFM12345678) be queried directly through Maersk's `/track-and-trace/v3/events` endpoint?
- [ ] Are there any legacy Safmarine shipments that are NOT accessible through Maersk's API (e.g., pre-migration historical data)?
- [ ] Does SSL have existing Maersk API credentials that can be reused for Safmarine tracking, or do they need separate registration?
- [ ] Are Safmarine-specific rates still available through Maersk's Spot Rate API, or are all rates now under the unified Maersk brand?

---

## Source Links

| Resource | URL |
|----------|-----|
| Maersk/Safmarine Integration Page | [https://www.maersk.com/safmarine](https://www.maersk.com/safmarine) |
| Maersk Developer Portal | [https://developer.maersk.com](https://developer.maersk.com) |
| Maersk API Catalogue | [https://developer.maersk.com/api-catalogue](https://developer.maersk.com/api-catalogue) |
| Maersk API Status | [https://developer.maersk.com/api-status](https://developer.maersk.com/api-status) |
| Maersk Tracking Portal | [https://www.maersk.com/tracking](https://www.maersk.com/tracking) |
| Maersk EDI Getting Started | [https://developer.maersk.com/support/getting-started-edi](https://developer.maersk.com/support/getting-started-edi) |
| DCSA OpenAPI Specs | [https://github.com/dcsaorg/DCSA-OpenAPI](https://github.com/dcsaorg/DCSA-OpenAPI) |
| FreightWaves -- Maersk Axed Safmarine | [https://www.freightwaves.com/news/why-maersk-axed-safmarine-and-damco-and-whats-next](https://www.freightwaves.com/news/why-maersk-axed-safmarine-and-damco-and-whats-next) |
| Seatrade -- Retiring Safmarine Brand | [https://www.seatrade-maritime.com/containers/maersk-retiring-safmarine-and-damco-brands](https://www.seatrade-maritime.com/containers/maersk-retiring-safmarine-and-damco-brands) |
| Vizion -- Safmarine Tracking | [https://www.vizionapi.com/carrier-tracking/safmarine](https://www.vizionapi.com/carrier-tracking/safmarine) |
| Terminal49 -- Safmarine SAFM | [https://terminal49.com/shipping-lines/safm-safmarine-container-line-container-tracking](https://terminal49.com/shipping-lines/safm-safmarine-container-line-container-tracking) |
| Portcast -- Safmarine Tracking | [https://www.portcast.io/carrier-coverage/safmarine-container-line-tracking](https://www.portcast.io/carrier-coverage/safmarine-container-line-tracking) |
| Wikipedia -- Safmarine | [https://en.wikipedia.org/wiki/Safmarine](https://en.wikipedia.org/wiki/Safmarine) |
