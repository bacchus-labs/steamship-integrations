# SeaLand (A Maersk Company) -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing. SeaLand is a retired Maersk brand; all API access is through Maersk's developer portal. This inventory references the Maersk API inventory as the canonical source and documents SeaLand-specific considerations.
> **Researched by**: Agent (carrier-api-inventory workflow)
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | SeaLand -- A Maersk Company (brand retired December 2023) |
| **SCAC Code** | SEJJ (Europe), SEAU (Americas), MCPU (Asia) |
| **Parent Company** | A.P. Moller-Maersk A/S |
| **Alliance** | Gemini Cooperation (with Hapag-Lloyd; via Maersk parent) |
| **Primary Services** | Intra-regional container shipping (Americas, Europe-Mediterranean, Asia intra-regional). Brand retired; services now operate under Maersk brand |
| **Market Position** | Former intra-regional specialist under Maersk. Focused on intra-Americas, intra-Europe, and intra-Asia trades. All operations now under Maersk |
| **Headquarters** | Miramar, Florida, USA (Americas operations); now consolidated under Maersk, Copenhagen, Denmark |
| **Website** | https://www.maersk.com/sealand (redirect/migration page; original sealandmaersk.com retired) |

### Brand History and Current Status

SeaLand was revived in 2015 by Maersk as a specialized intra-regional container shipping brand, serving intra-Americas, intra-Europe (via Seago Line), and intra-Asia (via MCC Transport) trades. In January 2023, Maersk announced the retirement of SeaLand along with Hamburg Sud and other acquired brands as part of a unified Maersk brand strategy. By December 2023, the SeaLand brand ceased to exist. All bookings, tracking, and operations are now handled through Maersk.com and Maersk's API infrastructure.

**For SDK purposes, SeaLand is not a separate carrier -- it is Maersk.** The SeaLand adapter should be a thin alias/wrapper around the Maersk adapter.

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | No (uses Maersk's portal) |
| **Developer portal URL** | https://developer.maersk.com (Maersk unified portal) |
| **API documentation URL(s)** | https://developer.maersk.com (SPA; same documentation as Maersk) |
| **Documentation quality** | Excellent (inherits Maersk's comprehensive DCSA-aligned documentation) |
| **OpenAPI/Swagger spec available?** | Yes -- via DCSA standard specs at https://github.com/dcsaorg/DCSA-OpenAPI and Maersk's interactive docs |
| **Sandbox/test environment?** | Yes -- via Maersk developer portal sandbox |
| **Developer registration** | Free self-service at https://developer.maersk.com. Note: EDI docs mention that users registered with "any Sealand -- A Maersk Company region" need separate Developer Portal credentials |
| **Developer support channels** | Maersk developer portal support, API support team, status page at https://status.maersk.com |
| **Community/third-party libraries** | None SeaLand-specific. Minimal Maersk-specific libraries (see Maersk inventory) |
| **API changelog / release notes** | Available on Maersk developer portal; DCSA spec changelogs at https://github.com/dcsaorg/DCSA-OpenAPI |

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | Not separately -- Maersk is a DCSA founding member; SeaLand inherits compliance |
| **DCSA APIs implemented** | TNT (Track & Trace), BKG (Booking), CS (Commercial Schedules) -- all via Maersk |
| **DCSA TNT version** | v2 and v3 (via Maersk: `/synergy/tracking/v2/events` and `/track-and-trace/v3/events`) |
| **DCSA Booking version** | v2 (via Maersk) |
| **DCSA Schedules version** | v1 (via Maersk: `/schedules/v1/vessel-schedules`, `/schedules/v1/port-schedules`, `/schedules/v1/point-to-point-routes`) |
| **Known DCSA deviations** | Same as Maersk -- none documented publicly |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Yes | Via Maersk EDI infrastructure. IFTMIN, IFTSTA, COPARN, BAPLIE supported |
| **INTTRA integration** | Yes | Maersk/SeaLand available on INTTRA (E2open) platform |
| **BIC (Bureau International des Containers)** | Yes | Standard container ID format used throughout Maersk APIs |
| **UN/LOCODE** | Yes | UNLocationCode used consistently across all Maersk endpoints |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | Dual: OAuth2 Client Credentials + API Key (Consumer-Key header) -- same as Maersk |
| **Auth documentation** | https://developer.maersk.com (authentication section) |
| **Registration process** | 1. Visit https://developer.maersk.com 2. Create free developer account 3. Register application 4. Obtain API key / client credentials |
| **Registration URL** | https://developer.maersk.com |
| **Partner program required?** | No -- basic API access is self-service (same as Maersk) |
| **Partner program URL** | N/A for basic access |
| **Credential type** | Consumer-Key (API Key) for most endpoints; Client ID + Client Secret for OAuth2 endpoints |
| **Token refresh supported?** | Yes -- OAuth2 client_credentials flow; refresh by re-requesting |
| **Token lifetime** | Unknown -- estimated ~1 hour based on standard OAuth2 patterns (same as Maersk) |
| **Access tiers** | Reported: Basic (self-service, standard rate limits) and Partner/Enterprise (elevated limits) |
| **IP whitelisting required?** | No |

### Access Requirements Summary for SSL

SeaLand API access is identical to Maersk API access. SSL should:

1. Register a free developer account at https://developer.maersk.com (if not already done for Maersk)
2. Use the same Maersk credentials to track SeaLand shipments
3. Legacy SeaLand B/L numbers (prefixed with SEAU, SEJJ, or MCPU) should be trackable through Maersk's tracking API. Live testing is needed to confirm whether a specific `brandScac` parameter is required or whether Maersk's API resolves these automatically.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field has a row.
> All fields are accessed via Maersk's API infrastructure. Coverage is identical to Maersk.
> ✅ = Available | ❌ = Not available | ⚠️ = Partial / limited | ❓ = Unknown

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ✅ | `GET /schedules/v1/vessel-schedules`, `GET /schedules/v1/port-schedules` (Maersk API) | Vessel rotation objects with port calls, ETAs/ETDs | DCSA CS v1 `vessel-schedules`, `port-schedules` | Via Maersk API. SeaLand intra-regional routes included in Maersk schedule data |
| 1.2 | Point-to-Point Route Options | ✅ | `GET /schedules/v1/point-to-point-routes` (Maersk API) | `PointToPoint` objects with `legs[]`, `transitTime`, `cutOffTimes[]` | DCSA CS v1 `point-to-point-routes` | Via Maersk API |
| 1.3 | Booking Lifecycle | ✅ | Maersk Booking API (exact path prefix requires portal access) | Booking status, `transportPlan[]`, `shipmentCutOffTimes[]` | DCSA BKG v2 `/v2/bookings` | Via Maersk API. New bookings made under Maersk brand |
| 1.4 | Shipping Instructions | ⚠️ | Via ShipmentEvents in Maersk TNT API | ShipmentEvent with `documentTypeCode=SHI` | DCSA EBL API | Likely available via Maersk but dedicated EBL endpoint not confirmed |
| 1.5 | Rates | ✅ | `GET /rates/spot` (Maersk API) | Proprietary spot rate response | Not DCSA -- proprietary Maersk API | Via Maersk API. SeaLand routes may use `brandScac` parameter |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ✅ | CS point-to-point response (Maersk API) | `cutOffDateTimeCode: "ECP"` in `cutOffTimes[]` | `ECP` | Via Maersk API |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ✅ | Booking confirmation + CS point-to-point (Maersk API) | `cutOffDateTimeCode: "EFC"` | `EFC` | Via Maersk API |
| 2.3 | Documentation Cutoff | DCO | ✅ | Booking confirmation (Maersk API) | `cutOffDateTimeCode: "DCO"` in `shipmentCutOffTimes[]` | `DCO` | Via Maersk API |
| 2.4 | VGM Cutoff | VCO | ✅ | Booking confirmation (Maersk API) | `cutOffDateTimeCode: "VCO"` in `shipmentCutOffTimes[]` | `VCO` | Via Maersk API |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ✅ | Booking confirmation (Maersk API) | `cutOffDateTimeCode: "FCO"` in `shipmentCutOffTimes[]` | `FCO` | Via Maersk API |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ⚠️ | Booking confirmation (Maersk API) | `cutOffDateTimeCode: "LCO"` in `shipmentCutOffTimes[]` | `LCO` | Conditional -- only present when `receiptTypeAtOrigin = "CFS"` |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ✅ | `GET /track-and-trace/v3/events?eventTypes=EQUIPMENT` (Maersk API) | Inferred from first EquipmentEvent with `relatedDocumentReferences[].type=BKG` | Inferred from first EquipmentEvent | Via Maersk API |
| 3.2 | Empty Container Gate-Out (Pickup) | ✅ | `GET /track-and-trace/v3/events` (Maersk API) | `equipmentEventTypeCode: GTOT` + `emptyIndicatorCode: EMPTY` | `GTOT` + `EMPTY` | Via Maersk API |
| 3.3 | Full Container Gate-In | ✅ | `GET /track-and-trace/v3/events` (Maersk API) | `equipmentEventTypeCode: GTIN` + `emptyIndicatorCode: LADEN` | `GTIN` + `LADEN` | Via Maersk API |
| 3.4 | Container Loaded on Vessel | ✅ | `GET /track-and-trace/v3/events` (Maersk API) | `equipmentEventTypeCode: LOAD` + `emptyIndicatorCode: LADEN` + `isTransshipmentMove: false` | `LOAD` + `LADEN` | Via Maersk API |
| 3.5 | Container Discharged at Transshipment | ✅ | `GET /track-and-trace/v3/events` (Maersk API) | `equipmentEventTypeCode: DISC` + `emptyIndicatorCode: LADEN` + `isTransshipmentMove: true` | `DISC` + `LADEN` + transshipment | Via Maersk API |
| 3.6 | Container Loaded at Transshipment | ✅ | `GET /track-and-trace/v3/events` (Maersk API) | `equipmentEventTypeCode: LOAD` + `emptyIndicatorCode: LADEN` + `isTransshipmentMove: true` | `LOAD` + `LADEN` + transshipment | Via Maersk API |
| 3.7 | Container Discharged at Destination | ✅ | `GET /track-and-trace/v3/events` (Maersk API) | `equipmentEventTypeCode: DISC` + `emptyIndicatorCode: LADEN` + `isTransshipmentMove: false` | `DISC` + `LADEN` | Via Maersk API |
| 3.8 | Full Container Gate-Out (Delivery) | ✅ | `GET /track-and-trace/v3/events` (Maersk API) | `equipmentEventTypeCode: GTOT` + `emptyIndicatorCode: LADEN` | `GTOT` + `LADEN` | Via Maersk API |
| 3.9 | Empty Container Returned | ✅ | `GET /track-and-trace/v3/events` (Maersk API) | `equipmentEventTypeCode: GTIN` + `emptyIndicatorCode: EMPTY` | `GTIN` + `EMPTY` | Via Maersk API |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ✅ | `GET /track-and-trace/v3/events?eventTypes=TRANSPORT` + Schedules API (Maersk) | `transportEventTypeCode: DEPA` + `eventClassifierCode: PLN/EST/ACT` | `DEPA` + classifier | Via Maersk API |
| 4.2 | Estimated Time of Arrival | ETA | ✅ | `GET /track-and-trace/v3/events?eventTypes=TRANSPORT` + Schedules API (Maersk) | `transportEventTypeCode: ARRI` + `eventClassifierCode: PLN/EST/ACT` | `ARRI` + classifier | Via Maersk API |
| 4.3 | Vessel Arrival at Transshipment | -- | ✅ | `GET /track-and-trace/v3/events?eventTypes=TRANSPORT` (Maersk API) | `transportEventTypeCode: ARRI` at intermediate port | `ARRI` at intermediate | Via Maersk API |
| 4.4 | Vessel Departure from Transshipment | -- | ✅ | `GET /track-and-trace/v3/events?eventTypes=TRANSPORT` (Maersk API) | `transportEventTypeCode: DEPA` on connecting vessel | `DEPA` at intermediate | Via Maersk API |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ✅ | Via Maersk: `POST /track-and-trace/v3/event-subscriptions` with `callbackUrl`. Full CRUD subscription management |
| Event Polling with timestamp filter | ✅ | Via Maersk: `GET /track-and-trace/v3/events?eventCreatedDateTime:gte={timestamp}`. Mandatory per DCSA spec |
| Event Classifier Progression (PLN->EST->ACT) | ✅ | Standard DCSA classifier codes via Maersk API |
| Retracted Events | ✅ | `metadata.retractedEventID` field via Maersk API |
| Change Remarks | ✅ | `changeRemark` field on TransportEvents via Maersk API |
| Delay Reason Codes | ✅ | `delayReasonCode` on TransportEvents via Maersk API |

### Coverage Summary

| Category | Fields Available | Fields Unavailable | Fields Unknown | Coverage % |
|----------|-----------------|-------------------|----------------|-----------|
| API Domains (1.x) | 4/5 | 0/5 | 1/5 | 80% |
| Cutoffs (2.x) | 5/6 | 0/6 | 1/6 | 83% |
| Container Milestones (3.x) | 9/9 | 0/9 | 0/9 | 100% |
| Transport Events (4.x) | 4/4 | 0/4 | 0/4 | 100% |
| Change Detection (5.x) | 6/6 | 0/6 | 0/6 | 100% |
| **Total** | **28/30** | **0/30** | **2/30** | **93%** |

> **Notes on Coverage:**
> - Coverage is identical to Maersk because SeaLand shipments use Maersk's API infrastructure
> - Shipping Instructions (1.4) marked as partial: likely available via ShipmentEvents but dedicated EBL endpoint not confirmed
> - LCL Cutoff (2.6) marked as partial: conditionally available only for CFS shipments (standard DCSA behavior)
> - All container milestones and transport events are fully covered through DCSA TNT v3
> - All change detection mechanisms supported via Maersk

---

## Endpoint Reference

SeaLand does not have its own API endpoints. All endpoints are Maersk endpoints documented in the Maersk API inventory (`docs/carriers/maersk/api-inventory.md`). Key endpoints summarized below for reference.

### Tracking / Events

| Endpoint | Method | Lookup Params | Pagination | Response Format | Notes |
|----------|--------|--------------|------------|----------------|-------|
| `/track-and-trace/v3/events` | GET | `documentTypeCodes`, `documentReference`, `equipmentReference`, `vesselIMONumber`, `eventTypes`, `eventCreatedDateTime` | Header-based (`limit` + page headers) | JSON (DCSA event array) | Primary tracking endpoint. API Key auth |
| `/track-and-trace/v3/events/{eventID}` | GET | `eventID` path param | N/A | JSON (DCSA event) | Single event retrieval |
| `/synergy/tracking/v2/events` | GET | Same as v3 with v2 schema | Page-based headers | JSON (DCSA event array) | Legacy v2 endpoint. OAuth2 auth |

### Schedules

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| `/schedules/v1/vessel-schedules` | GET | `vesselIMONumber`, `carrierServiceCode`, `UNLocationCode` | Cursor-based | JSON (DCSA vessel schedule array) | API Key auth |
| `/schedules/v1/port-schedules` | GET | `UNLocationCode` (required), date range | Cursor-based | JSON (DCSA port schedule array) | API Key auth |
| `/schedules/v1/point-to-point-routes` | GET | `placeOfReceipt`, `placeOfDelivery`, date range | Cursor-based | JSON (PointToPoint array) | API Key auth |

### Booking

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| DCSA BKG v2: `/v2/bookings` | GET/POST/PUT/DELETE | `carrierBookingReference` | Cursor-based | JSON | Exact Maersk path prefix requires portal access |

### Lookup Methods Summary

| Identifier Type | Supported? | Which Endpoints? | Notes |
|----------------|-----------|-----------------|-------|
| **Bill of Lading (B/L) number** | ✅ | TNT events (`documentTypeCodes=TRD&documentReference={blNumber}`) | Legacy SeaLand B/L numbers (SEAU/SEJJ/MCPU prefix) expected to resolve via Maersk API |
| **Booking reference** | ✅ | TNT events (`documentTypeCodes=BKG&documentReference={bookingRef}`) | New bookings are under Maersk brand |
| **Container number** | ✅ | TNT events (`equipmentReference={containerNumber}`) | Per-container tracking |
| **Carrier booking number** | ✅ | Same as booking reference | `carrierBookingReference` in DCSA |
| **Vessel IMO / voyage** | ✅ | TNT events, Schedules API | Filter by vessel |

---

## Rate Limits & Quotas

| Detail | Value | Source |
|--------|-------|--------|
| **Global rate limit** | Unpublished (same as Maersk) | Unknown |
| **Per-endpoint limits** | Unpublished (same as Maersk) | Unknown |
| **Daily/monthly quota** | Unpublished | Unknown |
| **Rate limit response** | Expected: 429 with Retry-After header | Estimated (unverified) |
| **Rate limit by** | Consumer-Key / OAuth token | Estimated (unverified) |
| **Burst allowance** | Unknown | Unknown |
| **Different tiers** | Reported: free/self-service tier has lower limits; partner tier has higher limits | Reported |

---

## Webhook / Push Support

| Detail | Value |
|--------|-------|
| **Webhooks supported?** | Yes -- via Maersk's DCSA TNT v3 subscription model |
| **Subscription endpoint** | `POST /track-and-trace/v3/event-subscriptions` (Maersk API) |
| **Subscription management** | Full CRUD via Maersk API |
| **Subscribable event types** | All DCSA event types: SHIPMENT, TRANSPORT, EQUIPMENT (via Maersk) |
| **Callback format** | DCSA event JSON POSTed to `callbackUrl` |
| **Callback authentication** | Shared secret (set during subscription creation, rotatable) |
| **Retry policy on failure** | Unknown (carrier-specific) |
| **Documented reliability** | Unknown -- no published SLA |

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | https://www.maersk.com/tracking (SeaLand tracking redirects here) |
| **Login required?** | No for basic container/B/L tracking |
| **Data available on portal but NOT in API** | Unlikely -- Maersk's API surface is comprehensive |
| **Scraping feasibility** | Not needed -- API coverage is excellent |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Yes (via Maersk) |
| **EDI message types** | IFTMIN, IFTSTA, COPARN, BAPLIE |
| **EDI connection method** | AS2, SFTP via Maersk EDI team |
| **EDI documentation** | https://developer.maersk.com/support/getting-started-edi |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Yes | Via Maersk integration |
| **FourKites** | Yes | Via Maersk integration |
| **Vizion** | Yes | Explicitly lists SeaLand with SCAC SEAU |
| **INTTRA / E2open** | Yes | Maersk/SeaLand available; supports booking and tracking |
| **CargoSmart** | Yes | Via Maersk integration |
| **Terminal49** | Yes | Lists "Sealand Americas (SEAU)" as supported carrier |
| **ShipsGo** | Yes | Provides SEALAND tracking API using carrier data |
| **Portcast** | Yes | Supports "Sealand Maersk" container tracking with predictive ETA |

> **Aggregator note:** Multiple third-party aggregators explicitly support SeaLand under SCAC code SEAU, even after brand retirement. This suggests the SEAU carrier code remains active in aggregator systems. For SSL's direct integration, using Maersk's API directly provides the richest data.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Reported as ~5-15 minutes (same as Maersk) | Reported |
| **API uptime/reliability** | Maersk status page at https://status.maersk.com | Official (status page) |
| **Historical data depth** | Estimated ~90-180 days (same as Maersk) | Estimated (unverified) |
| **Timezone handling** | ISO 8601 with timezone offset per DCSA spec | Official (DCSA spec) |
| **Character encoding** | UTF-8 per DCSA spec | Official (DCSA spec) |

### Known Issues & Gotchas

- **Legacy SCAC code resolution**: SeaLand has three regional SCAC codes (SEJJ, SEAU, MCPU). It is unconfirmed whether Maersk's tracking API automatically resolves legacy SeaLand B/L numbers or requires a specific `brandScac` parameter. Live testing required.

- **Brand retirement transition period**: Some aggregators and industry systems still reference "SeaLand" as a separate carrier. The SDK should map all three SeaLand SCAC codes (SEJJ, SEAU, MCPU) to the Maersk adapter.

- **Dual auth mechanism**: Same as Maersk -- some endpoints use OAuth2, others use API Key (Consumer-Key header). See Maersk inventory for details.

- **Historical shipments**: SeaLand shipments booked before December 2023 may have SeaLand-branded B/L numbers. These should be trackable via Maersk's API but may require the legacy SCAC code as a lookup parameter.

- **Maersk-inherited gotchas**: All Maersk API gotchas apply (path prefix variations, multiple tracking endpoint versions, booking endpoint path unknown, Akamai bot protection). See Maersk inventory for full list.

### Recently Deprecated or Changed

- **SeaLand brand retired December 2023**: All services consolidated under Maersk brand. sealandmaersk.com gradually being shut down; redirects to maersk.com/sealand.
- **SeaLand mobile app closed October 15, 2023**
- **All new bookings under Maersk brand since October 1, 2023**

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | Yes -- via Maersk API (identical coverage). SeaLand adapter = Maersk adapter alias |
| **Implementation effort** | Minimal -- SeaLand adapter is a configuration alias for the Maersk adapter with SCAC code mapping |
| **DCSA base adapter usable?** | Yes -- Maersk is a DCSA founding member with comprehensive compliance |

### Recommended Approach

The SeaLand adapter should **not** be a separate implementation. Instead:

1. **Maersk adapter**: Build the full Maersk adapter as documented in the Maersk API inventory (DCSA base adapter + Maersk config layer).

2. **SeaLand alias**: Create a `SeaLandAdapter` that extends or wraps `MaerskAdapter` with zero additional logic. The only differences:
   - SCAC code mapping: `SEJJ` / `SEAU` / `MCPU` -> Maersk adapter
   - Carrier name in metadata: "SeaLand (A Maersk Company)"
   - Any `brandScac` parameter injection if Maersk API requires it for legacy lookups

3. **SCAC routing**: The carrier adapter registry should route all three SeaLand SCAC codes to the Maersk adapter (or SeaLand alias).

This approach avoids code duplication and ensures SeaLand tracking stays in sync with Maersk API changes.

### Recommended Lookup Method

Same as Maersk: **Bill of Lading (B/L) number** as primary, **booking reference** as secondary, **container number** as supplementary.

For legacy SeaLand shipments, the B/L number will carry a SeaLand prefix (e.g., `SEAU...`). These should be passed directly to Maersk's API -- verify during live testing that resolution is automatic.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Every 2-4 hours for active shipments (same as Maersk) |
| **Incremental filter** | `eventCreatedDateTime:gte={lastPollTimestamp}` via Maersk API |
| **Batch tracking** | One API call per shipment (same as Maersk) |

### Auth Implementation Notes

Identical to Maersk. See Maersk API inventory for OAuth2 and API Key flow details.

```
OAuth2 Flow (for /synergy/ and /v1/ endpoints):
  POST https://api.maersk.com/oauth2/access_token
  Body: grant_type=client_credentials&client_id={id}&client_secret={secret}

API Key Flow (for /track-and-trace/ and /schedules/ endpoints):
  Header: Consumer-Key: {api_key}
```

### Edge Cases to Handle

- **SCAC code aliasing**: SDK must recognize SEJJ, SEAU, and MCPU as SeaLand codes and route to Maersk adapter
- **Legacy B/L prefix resolution**: Test whether `SEAU`-prefixed B/L numbers resolve automatically in Maersk API
- **Brand metadata**: When returning carrier info for a SeaLand shipment, should the SDK report "SeaLand" or "Maersk"? Recommend reporting "Maersk (formerly SeaLand)" for legacy shipments
- **All Maersk edge cases apply**: Transshipment event ordering, rolled containers, vessel changes, alliance transitions. See Maersk inventory

### Mapping Complexity

**Minimal.** The SeaLand adapter adds zero mapping complexity beyond Maersk. It is purely a SCAC code alias. All event parsing, normalization, pagination, and auth logic is handled by the Maersk adapter.

---

## Open Questions

- [ ] **Do legacy SeaLand B/L numbers (SEAU/SEJJ/MCPU prefix) resolve automatically in Maersk's tracking API?** Or is a `brandScac` parameter required?
- [ ] **Are all three SeaLand SCAC codes (SEJJ, SEAU, MCPU) still active in Maersk's system?** Or have they been consolidated to a single code?
- [ ] **Does Maersk's Offers/Rates API still accept SeaLand brandScac values?** The Maersk Offers API documentation references `brandScac` as a parameter
- [ ] **How long will legacy SeaLand booking/tracking data remain accessible in Maersk's system?** Retention policy for pre-merger data
- [ ] **Does SSL have existing Maersk developer credentials?** Same credentials cover SeaLand

---

## Source Links

| Resource | URL |
|----------|-----|
| SeaLand Migration Page | https://www.maersk.com/sealand |
| Maersk Brand Unification Announcement | https://www.maersk.com/news/articles/2023/01/27/a-unified-maersk-brand |
| Maersk Brand Transition Update | https://www.maersk.com/news/articles/2023/07/06/unifying-as-the-maersk-brand |
| Maersk Developer Portal | https://developer.maersk.com |
| Maersk Tracking Portal | https://www.maersk.com/tracking |
| Maersk API Status | https://developer.maersk.com/api-status |
| Maersk System Status | https://status.maersk.com |
| Maersk EDI Getting Started | https://developer.maersk.com/support/getting-started-edi |
| Maersk Offers API (brandScac reference) | https://api.productmanagement.maersk.com/offers/docs/endpoints/productoffers.html |
| Vizion SeaLand Tracking | https://www.vizionapi.com/carrier-tracking/sealand |
| Terminal49 SeaLand Americas | https://terminal49.com/shipping-lines/seau-sealand-americas-container-tracking/ |
| Portcast SeaLand Tracking | https://www.portcast.io/carrier-coverage/sealand-maersk-container-tracking |
| ShipsGo SeaLand Tracking | https://shipsgo.com/ocean/carriers/sealand/container-tracking |
| DCSA OpenAPI Specs (GitHub) | https://github.com/dcsaorg/DCSA-OpenAPI |
| SeaLand Wikipedia | https://en.wikipedia.org/wiki/SeaLand |
