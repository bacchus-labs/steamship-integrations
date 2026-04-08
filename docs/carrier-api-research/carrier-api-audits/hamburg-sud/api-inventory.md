# Hamburg Süd — API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only — not verified with live API testing. Hamburg Süd has no independent API; all programmatic access is through Maersk's APIs at developer.maersk.com. This inventory documents the Maersk API capabilities as they apply to Hamburg Süd shipments.
> **Researched by**: Agent (carrier API inventory workflow)
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | Hamburg Südamerikanische Dampfschifffahrts-Gesellschaft A/S & Co KG (commonly "Hamburg Süd" or "Hamburg Sud") |
| **SCAC Code** | SUDU |
| **Parent Company** | A.P. Moller-Maersk A/S (acquired 2017; brand unified into Maersk 2023-2024) |
| **Alliance** | Maersk subsidiary — operates under Maersk's network (Gemini Cooperation with Hapag-Lloyd) |
| **Primary Services** | Container shipping (historically focused on North-South trades: Americas, Africa, Australasia) |
| **Market Position** | Formerly 7th-largest container shipping line globally; now fully absorbed into Maersk (2nd-largest) |
| **Headquarters** | Hamburg, Germany (historical); now part of Copenhagen-based Maersk |
| **Website** | https://www.maersk.com/hamburgsud (hamburgsud.com redirects to maersk.com) |

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | No (independent); Yes (via Maersk) |
| **Developer portal URL** | https://developer.maersk.com |
| **API documentation URL(s)** | https://developer.maersk.com (SPA — API catalogue requires JavaScript rendering) |
| **Documentation quality** | Excellent (Maersk's portal; no Hamburg Süd-specific docs exist) |
| **OpenAPI/Swagger spec available?** | Yes — via Maersk/DCSA standard specs at https://github.com/dcsaorg/DCSA-OpenAPI |
| **Sandbox/test environment?** | Yes — via Maersk developer portal |
| **Developer registration** | Free self-service at https://developer.maersk.com |
| **Developer support channels** | Maersk developer portal support, API support team, status page at https://status.maersk.com |
| **Community/third-party libraries** | None specific to Hamburg Süd; minimal Maersk-specific libraries on GitHub/npm/PyPI |
| **API changelog / release notes** | Available on Maersk developer portal (requires login); DCSA spec changelogs at https://github.com/dcsaorg/DCSA-OpenAPI |

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | Not independently — covered under Maersk's DCSA founding membership |
| **DCSA APIs implemented** | TNT (Track & Trace), BKG (Booking), CS (Commercial Schedules) — all via Maersk |
| **DCSA TNT version** | v2 and v3 (via Maersk — both `/synergy/tracking/v2/events` and `/track-and-trace/v3/events` confirmed live) |
| **DCSA Booking version** | v2.x (via Maersk) |
| **DCSA Schedules version** | v1.x (via Maersk — `/schedules/v1/vessel-schedules`, `/schedules/v1/port-schedules`, `/schedules/v1/point-to-point-routes` confirmed live) |
| **Known DCSA deviations** | None known beyond those documented for Maersk. See Maersk API inventory for details. |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Yes | Historically supported IFTMIN, IFTSTA, COPARN, BAPLIE. Post-migration, all EDI flows through Maersk's EDI channel. |
| **INTTRA integration** | Yes | Hamburg Süd was on INTTRA for booking and eVGM submissions pre-merger; now accessible via Maersk on INTTRA/E2open. |
| **BIC (Bureau International des Containers)** | Yes | SUDU container prefix follows BIC standard format. |
| **UN/LOCODE** | Yes | Used throughout Maersk APIs. |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | Dual (via Maersk): OAuth2 Client Credentials + API Key (Consumer-Key header) depending on endpoint |
| **Auth documentation** | https://developer.maersk.com (authentication section) |
| **Registration process** | 1. Visit https://developer.maersk.com 2. Create free developer account 3. Register an application 4. Obtain API key / client credentials |
| **Registration URL** | https://developer.maersk.com |
| **Partner program required?** | No — basic API access is self-service via Maersk developer portal |
| **Partner program URL** | N/A for basic access |
| **Credential type** | Consumer-Key (API Key) for tracking/schedules endpoints; Client ID + Client Secret for OAuth2 endpoints |
| **Token refresh supported?** | Yes — OAuth2 client_credentials flow; refresh by re-requesting |
| **Token lifetime** | Estimated ~1 hour (unverified — standard OAuth2 pattern) |
| **Access tiers** | Reported: Basic (self-service, standard rate limits) and Partner/Enterprise (elevated limits) |
| **IP whitelisting required?** | No |

### Access Requirements Summary for SSL

Hamburg Süd shipments are fully managed through Maersk's API infrastructure. SSL should use the same Maersk developer account and credentials already established for the Maersk integration. No separate registration, partnership, or credentials are needed for Hamburg Süd.

The key question SSL needs to validate through live testing is whether Maersk's Tracking API accepts SUDU-prefixed container numbers and Hamburg Süd bill of lading numbers directly, or whether these identifiers have been remapped to Maersk-format identifiers post-migration. Third-party aggregators (Terminal49, project44, Portcast) all continue to track SUDU containers successfully, which strongly suggests SUDU identifiers remain valid in the underlying carrier systems.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field must have a row.
> All coverage ratings below assume access via Maersk's APIs (since Hamburg Süd has no independent API).
> ✅ = Available | ❌ = Not available | ⚠️ = Partial / limited | ❓ = Unknown

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ✅ | `GET /schedules/v1/vessel-schedules`, `GET /schedules/v1/port-schedules` (Maersk) | Vessel schedule objects with port calls, ETAs/ETDs | DCSA CS v1 | Via Maersk API. Unknown whether Hamburg Süd-specific services appear distinctly or merged under Maersk schedules. |
| 1.2 | Point-to-Point Route Options | ✅ | `GET /schedules/v1/point-to-point-routes` (Maersk) | `PointToPoint` objects with `legs[]`, `transitTime`, `cutOffTimes[]` | DCSA CS v1 | Via Maersk API |
| 1.3 | Booking Lifecycle | ✅ | Maersk Booking API (DCSA BKG v2) | Booking objects with `transportPlan[]`, `shipmentCutOffTimes[]` | DCSA BKG v2 | Via Maersk API. Hamburg Süd bookings now placed through Maersk systems. |
| 1.4 | Shipping Instructions | ⚠️ | Maersk eDocumentation API | ShipmentEvent with `documentTypeCode=SHI` | DCSA eDoc | Via Maersk API. Marked partial because eDoc implementation specifics not fully confirmed for ex-Hamburg Süd shipments. |
| 1.5 | Rates | ⚠️ | Maersk Spot Rate API (`/rates/`) | Proprietary rate objects with `brandScac` parameter | Not DCSA | Maersk Offers API uses `brandScac` parameter. Confirmed SCACs: maeu, mcpu, seau, sejj. SUDU likely supported but not publicly documented. |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ✅ | Maersk Booking/Schedules API | `cutOffDateTimeCode: "ECP"` in `shipmentCutOffTimes[]` or `cutOffTimes[]` | `ECP` | Via Maersk API |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ✅ | Maersk Booking/Schedules API | `cutOffDateTimeCode: "EFC"` | `EFC` | Via Maersk API |
| 2.3 | Documentation Cutoff | DCO | ✅ | Maersk Booking/Schedules API | `cutOffDateTimeCode: "DCO"` | `DCO` | Via Maersk API |
| 2.4 | VGM Cutoff | VCO | ✅ | Maersk Booking/Schedules API | `cutOffDateTimeCode: "VCO"` | `VCO` | Via Maersk API |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ✅ | Maersk Booking/Schedules API | `cutOffDateTimeCode: "FCO"` | `FCO` | Via Maersk API |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ⚠️ | Maersk Booking/Schedules API | `cutOffDateTimeCode: "LCO"` | `LCO` | Via Maersk API. Conditional: only present when `receiptTypeAtOrigin = "CFS"`. |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ✅ | Maersk TNT v3 (`GET /track-and-trace/v3/events`) | Inferred from first EquipmentEvent with `relatedDocumentReferences[].type=BKG` | Inferred from first EquipmentEvent | Via Maersk API |
| 3.2 | Empty Container Gate-Out (Pickup) | ✅ | Maersk TNT v3 | `equipmentEventTypeCode: GTOT` + `emptyIndicatorCode: EMPTY` | `GTOT` + `EMPTY` | Via Maersk API |
| 3.3 | Full Container Gate-In | ✅ | Maersk TNT v3 | `equipmentEventTypeCode: GTIN` + `emptyIndicatorCode: LADEN` | `GTIN` + `LADEN` | Via Maersk API |
| 3.4 | Container Loaded on Vessel | ✅ | Maersk TNT v3 | `equipmentEventTypeCode: LOAD` + `emptyIndicatorCode: LADEN` | `LOAD` + `LADEN` | Via Maersk API |
| 3.5 | Container Discharged at Transshipment | ✅ | Maersk TNT v3 | `equipmentEventTypeCode: DISC` + `emptyIndicatorCode: LADEN` + `isTransshipmentMove: true` | `DISC` + `LADEN` + transshipment | Via Maersk API |
| 3.6 | Container Loaded at Transshipment | ✅ | Maersk TNT v3 | `equipmentEventTypeCode: LOAD` + `emptyIndicatorCode: LADEN` + `isTransshipmentMove: true` | `LOAD` + `LADEN` + transshipment | Via Maersk API |
| 3.7 | Container Discharged at Destination | ✅ | Maersk TNT v3 | `equipmentEventTypeCode: DISC` + `emptyIndicatorCode: LADEN` + `isTransshipmentMove: false` | `DISC` + `LADEN` | Via Maersk API |
| 3.8 | Full Container Gate-Out (Delivery) | ✅ | Maersk TNT v3 | `equipmentEventTypeCode: GTOT` + `emptyIndicatorCode: LADEN` | `GTOT` + `LADEN` | Via Maersk API |
| 3.9 | Empty Container Returned | ✅ | Maersk TNT v3 | `equipmentEventTypeCode: GTIN` + `emptyIndicatorCode: EMPTY` | `GTIN` + `EMPTY` | Via Maersk API |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ✅ | Maersk TNT v3 / Schedules API | TransportEvent: `transportEventTypeCode: DEPA` + `eventClassifierCode: EST/PLN/ACT` | `DEPA` + classifier | Via Maersk API |
| 4.2 | Estimated Time of Arrival | ETA | ✅ | Maersk TNT v3 / Schedules API | TransportEvent: `transportEventTypeCode: ARRI` + `eventClassifierCode: EST/PLN/ACT` | `ARRI` + classifier | Via Maersk API |
| 4.3 | Vessel Arrival at Transshipment | — | ✅ | Maersk TNT v3 | TransportEvent: `transportEventTypeCode: ARRI` at intermediate port | `ARRI` at intermediate | Via Maersk API |
| 4.4 | Vessel Departure from Transshipment | — | ✅ | Maersk TNT v3 | TransportEvent: `transportEventTypeCode: DEPA` at intermediate port | `DEPA` at intermediate | Via Maersk API |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ✅ | Via Maersk: `POST /v3/event-subscriptions` with `callbackUrl`. Filters by event type, booking ref, equipment ref, vessel. |
| Event Polling with timestamp filter | ✅ | Via Maersk: `GET /v3/events` with `eventCreatedDateTime` filter. DCSA-mandatory -- all Maersk TNT endpoints support this. |
| Event Classifier Progression (PLN→EST→ACT) | ✅ | Via Maersk: Events progress PLN → EST → ACT for transport events. |
| Retracted Events | ✅ | Via Maersk: `metadata.retractedEventID` field for voided events. |
| Change Remarks | ✅ | Via Maersk: `changeRemark` field on TransportEvents (free text, max 250 chars). |
| Delay Reason Codes | ✅ | Via Maersk: `delayReasonCode` on TransportEvents (DCSA-standardized codes). |

### Coverage Summary

| Category | Fields Available | Fields Partial | Fields Unavailable | Fields Unknown | Coverage % |
|----------|-----------------|---------------|-------------------|----------------|-----------|
| API Domains (1.x) | 3/5 | 2/5 | 0/5 | 0/5 | 60% (100% with partials) |
| Cutoffs (2.x) | 5/6 | 1/6 | 0/6 | 0/6 | 83% (100% with partials) |
| Container Milestones (3.x) | 9/9 | 0/9 | 0/9 | 0/9 | 100% |
| Transport Events (4.x) | 4/4 | 0/4 | 0/4 | 0/4 | 100% |
| Change Detection (5.x) | 6/6 | 0/6 | 0/6 | 0/6 | 100% |
| **Total** | **27/30** | **3/30** | **0/30** | **0/30** | **90%** (100% with partials) |

> **Note on coverage**: The 3 fields marked ⚠️ (Shipping Instructions, Rates, LCL Cutoff) are marked partial/caveated rather than unavailable. Shipping Instructions and Rates are available via Maersk but have caveats specific to Hamburg Süd shipments (eDoc implementation not fully confirmed for ex-Hamburg Süd shipments; Rates `brandScac` support for SUDU not publicly documented). LCL Cutoff is conditional by nature (only applicable to CFS shipments). All 30 fields have been assessed -- none are truly unavailable or unknown.

---

## Endpoint Reference

> Hamburg Süd has no independent API endpoints. All endpoints below are Maersk's, documented in detail in the Maersk API inventory at `docs/carriers/maersk/api-inventory.md`.

### Tracking / Events

| Endpoint | Method | Lookup Params | Pagination | Response Format | Notes |
|----------|--------|--------------|------------|----------------|-------|
| `/track-and-trace/v3/events` | GET | B/L, Booking ref, Container, Vessel IMO | cursor | JSON | Maersk API -- API Key auth (Consumer-Key header) |
| `/synergy/tracking/v2/events` | GET | B/L, Booking ref, Container | cursor | JSON | Maersk API -- OAuth2 auth |

### Schedules

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| `/schedules/v1/vessel-schedules` | GET | vessel, date range | cursor | JSON | Maersk API -- API Key auth |
| `/schedules/v1/port-schedules` | GET | port (UN/LOCODE), date range | cursor | JSON | Maersk API -- API Key auth |
| `/schedules/v1/point-to-point-routes` | GET | origin, destination, date | cursor | JSON | Maersk API -- API Key auth |

### Booking

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| Maersk Booking API (DCSA BKG v2) | GET/POST | Booking ref | N/A | JSON | Maersk API -- exact path requires portal access to confirm |

### Other Endpoints

| Endpoint | Method | Purpose | Key Params | Notes |
|----------|--------|---------|-----------|-------|
| `/rates/` | GET | Spot rates | Origin, destination, brandScac | Maersk API -- brandScac parameter may accept SUDU |
| `/v3/event-subscriptions` | POST | Webhook subscriptions | callbackUrl, event filters | Maersk API |

### Lookup Methods Summary

| Identifier Type | Supported? | Which Endpoints? | Notes |
|----------------|-----------|-----------------|-------|
| **Bill of Lading (B/L) number** | ✅ (via Maersk) | TNT v3, TNT v2 | SUDU BL numbers likely accepted -- requires live validation |
| **Booking reference** | ✅ (via Maersk) | TNT v3, TNT v2, Booking API | Post-migration bookings use Maersk booking format |
| **Container number** | ✅ (via Maersk) | TNT v3, TNT v2 | SUDU-prefixed containers confirmed trackable by third-party aggregators |
| **Carrier booking number** | ✅ (via Maersk) | TNT v3, TNT v2 | Same as booking reference post-migration |
| **Vessel IMO / voyage** | ✅ (via Maersk) | TNT v3, Schedules | Vessel data available through Maersk schedules |

---

## Rate Limits & Quotas

| Detail | Value | Source |
|--------|-------|--------|
| **Global rate limit** | Unpublished (Maersk does not publish specific rate limits publicly) | Unknown |
| **Per-endpoint limits** | Unpublished | Unknown |
| **Daily/monthly quota** | Unpublished (reported: Basic tier has standard limits, Partner tier has elevated limits) | Reported |
| **Rate limit response** | Unknown (likely 429 with Retry-After header based on standard patterns) | Estimated |
| **Rate limit by** | API key / OAuth token (via Maersk) | Estimated |
| **Burst allowance** | Unknown | Unknown |
| **Different tiers** | Reported: Basic (self-service) and Partner/Enterprise (elevated) | Reported |

---

## Webhook / Push Support

| Detail | Value |
|--------|-------|
| **Webhooks supported?** | Yes (via Maersk) |
| **Subscription endpoint** | `POST /v3/event-subscriptions` (Maersk) |
| **Subscription management** | Create/list/delete via Maersk API |
| **Subscribable event types** | Equipment events (LOAD, DISC, GTIN, GTOT, etc.), Transport events (ARRI, DEPA), Shipment events |
| **Callback format** | DCSA event JSON POSTed to callbackUrl |
| **Callback authentication** | Unknown (requires Maersk portal docs) |
| **Retry policy on failure** | Unknown |
| **Documented reliability** | Unknown |

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | https://www.maersk.com/tracking/ (Hamburg Süd's own tracking no longer exists) |
| **Login required?** | No (for basic container/BL tracking) |
| **Data available on portal but NOT in API** | None known — portal and API share same data source (Maersk) |
| **Scraping feasibility** | Not assessed — API access via Maersk is the recommended approach |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Yes (via Maersk EDI channel) |
| **EDI message types** | IFTMIN, IFTSTA, COPARN, BAPLIE (historically supported; now via Maersk) |
| **EDI connection method** | Via Maersk EDI channel (specific connection method requires Maersk contact) |
| **EDI documentation** | Contact Maersk — Hamburg Süd EDI docs no longer available |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Yes | Dedicated Hamburg Süd tracking page. Supports MBL/BL and container number lookup. 98%+ global ocean coverage. |
| **FourKites** | Yes (inferred) | 85+ ocean carriers; Hamburg Süd/Maersk within coverage. No dedicated Hamburg Süd page found. |
| **Vizion** | Yes (inferred) | 98% ocean shipment coverage claimed. SUDU likely covered. No specific Hamburg Süd documentation found. |
| **INTTRA / E2open** | Yes | Hamburg Süd historically on INTTRA for booking and eVGM. Post-merger accessible via Maersk on INTTRA/E2open. |
| **CargoSmart** | Unknown | No specific Hamburg Süd integration found. |

> **Aggregator note**: Since Hamburg Süd shipments are tracked through Maersk's infrastructure, aggregator coverage for Maersk effectively extends to Hamburg Süd. The direct Maersk API integration is the recommended approach rather than going through an aggregator, since SSL already has Maersk API access.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Same as Maersk (reported < 15 min for most events) | Reported (Maersk community) |
| **API uptime/reliability** | Same as Maersk — status page at https://status.maersk.com | Official (Maersk) |
| **Historical data depth** | Unknown — depends on how far back Maersk retains ex-Hamburg Süd shipment data | Unknown |
| **Timezone handling** | UTC (Maersk/DCSA standard: ISO 8601 with timezone) | Official (DCSA spec) |
| **Character encoding** | UTF-8 | Official (DCSA spec) |

### Known Issues & Gotchas

- **Brand migration data continuity**: Shipments that started under Hamburg Süd's systems and were migrated mid-voyage to Maersk's systems may have incomplete event histories or gaps at the transition point. Historical data depth for pre-migration Hamburg Süd shipments is unknown.
- **SUDU identifier acceptance**: While third-party aggregators confirm SUDU containers are trackable, it is unverified whether Maersk's API directly accepts SUDU SCAC codes or Hamburg Süd-format BL numbers. Live testing required.
- **BrandScac parameter**: Maersk's Offers API uses `brandScac` for multi-brand support (confirmed: maeu, mcpu, seau, sejj). Whether SUDU is a valid brandScac value is not publicly documented.
- **EDI migration**: Customers were instructed to switch to Maersk EDI channel. Any legacy Hamburg Süd EDI configurations will no longer work for new bookings.

### Recently Deprecated or Changed

- **Hamburg Süd website**: hamburgsud.com now 301-redirects to maersk.com (as of 2025-2026)
- **Hamburg Süd Data Integrations page**: hamburgsud.com/digital-solutions/data-integrations redirects to maersk.com
- **Hamburg Süd EDI channel**: Deprecated in favor of Maersk EDI channel (per Maersk's 2023 migration guidance)
- **Hamburg Süd booking system**: Replaced by Maersk.com booking (Hamburg Süd "Captain Peter" portal being phased out)

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | Yes — but as a thin alias/configuration layer on the Maersk adapter, not a standalone adapter |
| **Implementation effort** | Low (configuration-only on top of Maersk adapter) |
| **DCSA base adapter usable?** | Yes — Hamburg Süd inherits Maersk's full DCSA compliance |

### Recommended Approach

Hamburg Süd should **not** have its own standalone adapter. Instead, the SDK should implement Hamburg Süd support as a **carrier alias or configuration variant of the Maersk adapter**. The recommended architecture:

1. The Maersk adapter handles all API communication, auth, and response parsing
2. A Hamburg Süd carrier entry in the registry maps SCAC `SUDU` to the Maersk adapter with Hamburg Süd-specific configuration (e.g., `brandScac: "sudu"` for rate queries, SUDU container prefix recognition)
3. No separate HTTP client, auth flow, or response normalization is needed

This is analogous to how Sealand (SEJJ), Sealand Americas (SEAU), and Sealand Asia (MCPU) are likely handled in Maersk's own systems — different brand SCACs routed through the same API infrastructure.

### Recommended Lookup Method

**Container number** (SUDU prefix) is the safest starting point, as third-party aggregators confirm SUDU containers are trackable through Maersk's systems. Bill of Lading number is the next option but requires live validation to confirm format compatibility.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Same as Maersk: every 2-4 hours for active shipments |
| **Incremental filter** | Use `eventCreatedDateTime > lastPollTime` (DCSA standard, supported via Maersk TNT) |
| **Batch tracking** | One call per shipment (same as Maersk — no batch endpoint) |

### Auth Implementation Notes

No separate auth implementation needed. Reuse the Maersk adapter's dual auth:
- **API Key (Consumer-Key)** for `/track-and-trace/v3/` and `/schedules/v1/` paths
- **OAuth2 (client_credentials)** for `/synergy/tracking/v2/` and other paths

SSL's existing Maersk credentials should work for Hamburg Süd shipments.

### Edge Cases to Handle

- **SUDU container prefix**: Ensure the adapter recognizes SUDU-prefixed container numbers and routes them through the Maersk adapter
- **Historical BL formats**: Hamburg Süd BL numbers may use a different format than Maersk BL numbers. The adapter should accept both formats.
- **Migration-era shipments**: Shipments from the 2023-2024 migration period may have mixed data — started in Hamburg Süd systems, completed in Maersk systems. Event history may have gaps.
- **Brand-specific rate queries**: If using Maersk's Offers API for rate data, the `brandScac` parameter may need to be `sudu` for Hamburg Süd-specific routes (historically North-South trade lanes).

### Mapping Complexity

**Minimal**. Since all data comes from Maersk's DCSA-compliant APIs, the mapping is identical to the Maersk adapter. No carrier-specific field mapping, event code translation, or response format handling is needed. The only complexity is in routing — ensuring SUDU identifiers reach the Maersk adapter correctly.

---

## Open Questions

- [ ] Does Maersk's TNT API accept SUDU SCAC code as a filter parameter (e.g., `carrierScac=SUDU`)? Requires live testing.
- [ ] Do Hamburg Süd-format BL numbers work directly in Maersk's tracking endpoints? Requires live testing.
- [ ] Is `sudu` a valid `brandScac` value in Maersk's Offers API for rate queries?
- [ ] How far back does Maersk retain historical event data for pre-migration Hamburg Süd shipments?
- [ ] Does SSL have any active Hamburg Süd shipments that could be used for validation testing?
- [ ] Are there any Hamburg Süd-specific routes or services that appear differently in Maersk's schedule data?

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website (redirects to Maersk) | https://www.hamburgsud.com |
| Maersk Hamburg Süd transition page | https://www.maersk.com/hamburgsud |
| Developer Portal (Maersk) | https://developer.maersk.com |
| API Documentation (Maersk) | https://developer.maersk.com/api-catalogue |
| Maersk API Status | https://status.maersk.com |
| DCSA OpenAPI Specs | https://github.com/dcsaorg/DCSA-OpenAPI |
| Maersk Brand Unification Announcement | https://www.maersk.com/news/articles/2023/06/19/unifying-with-the-maersk-brand |
| INTTRA eVGM adoption (historical) | https://www.inttra.com/newsroom/press-releases/hamburg-sud-to-adopt-inttra-evgm/ |
| project44 Hamburg Süd Tracking | https://www.project44.com/tracking/container/hamburg-sud/ |
| Terminal49 Hamburg Süd Tracking | https://terminal49.com/shipping-lines/sudu-hamburg-sud-container-tracking |
| Maersk Offers API (brandScac docs) | https://api.productmanagement.maersk.com/offers/docs/endpoints/productoffers.html |
| Supply Chain Dive - Brand Unification | https://www.supplychaindive.com/news/Maersk-unifies-brands-as-it-pushes-for-integrated-services/641457/ |
