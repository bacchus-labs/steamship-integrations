# CSAV (Compania Sudamericana de Vapores) -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing. CSAV merged container operations into Hapag-Lloyd in 2014 and closed all directly operated services by July 2020. CSAV has no independent API infrastructure; all container shipping is handled by Hapag-Lloyd.
> **Researched by**: agent (audit/csav)
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | Compania Sudamericana de Vapores S.A. (CSAV) |
| **SCAC Code** | CHIW |
| **Parent Company** | CSAV S.A. (publicly traded, Santiago Stock Exchange: VAPORES) -- investment holding company with ~30% stake in Hapag-Lloyd AG |
| **Alliance** | N/A -- CSAV does not operate vessels; Hapag-Lloyd (in which CSAV holds equity) is in the Gemini Cooperation with Maersk |
| **Primary Services** | None (investment holding company). Container shipping historically; all operations merged into Hapag-Lloyd |
| **Market Position** | No longer an operating carrier. Largest shipping company in Latin America by history; today an equity investor in Hapag-Lloyd (5th largest global container line) |
| **Headquarters** | Santiago, Chile |
| **Website** | [https://www.csav.com](https://www.csav.com) |

> **Critical context**: CSAV merged its container shipping operations into Hapag-Lloyd in December 2014. CSAV closed its last directly operated services in July 2020. Today CSAV is purely an investment holding company. Its ~30% equity stake in Hapag-Lloyd represents over 85% of CSAV's consolidated assets. **CSAV has no shipping API, developer portal, or digital shipping infrastructure.** All container tracking, booking, scheduling, and event data for shipments historically associated with CSAV flow through Hapag-Lloyd's systems. See the [Hapag-Lloyd API inventory](../hapag-lloyd/api-inventory.md) for full details.

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | No |
| **Developer portal URL** | N/A -- use Hapag-Lloyd: [api-portal.hlag.com](https://api-portal.hlag.com) |
| **API documentation URL(s)** | N/A -- use Hapag-Lloyd API docs |
| **Documentation quality** | None -- CSAV has no API documentation |
| **OpenAPI/Swagger spec available?** | No |
| **Sandbox/test environment?** | N/A |
| **Developer registration** | N/A -- register at Hapag-Lloyd's portal for container tracking |
| **Developer support channels** | N/A |
| **Community/third-party libraries** | None for CSAV directly. See Hapag-Lloyd inventory for HL libraries |
| **API changelog / release notes** | N/A |

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | No -- CSAV is not a DCSA member. Hapag-Lloyd (which operates all former CSAV container services) is a DCSA founding member |
| **DCSA APIs implemented** | None directly. Via Hapag-Lloyd: TNT v2.2.4, CS v1.0.1, OVS v3.0.7 |
| **DCSA TNT version** | N/A (via Hapag-Lloyd: v2.2.4 BETA) |
| **DCSA Booking version** | N/A |
| **DCSA Schedules version** | N/A (via Hapag-Lloyd: CS v1.0.1, OVS v3.0.7) |
| **Known DCSA deviations** | N/A -- see Hapag-Lloyd inventory for HL's DCSA deviations |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | No (directly) | CSAV has no EDI infrastructure. Hapag-Lloyd supports EDI |
| **INTTRA integration** | No (directly) | Via Hapag-Lloyd's INTTRA connection |
| **BIC (Bureau International des Containers)** | N/A | Container prefixes CSVU and LNXU are tracked through Hapag-Lloyd |
| **UN/LOCODE** | N/A | Via Hapag-Lloyd APIs |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | N/A -- no CSAV API exists |
| **Auth documentation** | N/A |
| **Registration process** | N/A -- for container tracking, register at [api-portal.hlag.com](https://api-portal.hlag.com) |
| **Registration URL** | N/A |
| **Partner program required?** | N/A |
| **Partner program URL** | N/A |
| **Credential type** | N/A |
| **Token refresh supported?** | N/A |
| **Token lifetime** | N/A |
| **Access tiers** | N/A |
| **IP whitelisting required?** | N/A |

### Access Requirements Summary for SSL

CSAV has no API. SSL should use the Hapag-Lloyd adapter for any shipments historically associated with CSAV. In the carrier registry, CSAV's SCAC code (CHIW) should be mapped as an alias to Hapag-Lloyd (HLCU). No separate credentials, registration, or business relationship with CSAV is needed. See the [Hapag-Lloyd API inventory](../hapag-lloyd/api-inventory.md) for complete access requirements.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field must have a row.
> Coverage reflects what is available **via Hapag-Lloyd's APIs**, since CSAV has no independent API.
> ✅ = Available (via HL) | ❌ = Not available | ⚠️ = Partial / limited (via HL) | ❓ = Unknown

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ✅ | Hapag-Lloyd DCSA CS v1.0.1 + OVS v3.0.7 | Vessel schedules, port calls | DCSA CS v1 + OVS v3 | Via Hapag-Lloyd API |
| 1.2 | Point-to-Point Route Options | ✅ | Hapag-Lloyd DCSA CS v1.0.1 | P2P routing | DCSA CS v1 | Via Hapag-Lloyd API |
| 1.3 | Booking Lifecycle | ⚠️ | Hapag-Lloyd TNT v2.2.4 (ShipmentEvent) | ISSU, CONF only | DCSA TNT ShipmentEvent | Limited status codes via HL; no standalone Booking API |
| 1.4 | Shipping Instructions | ⚠️ | Hapag-Lloyd TNT v2.2.4 (ShipmentEvent) | ISSU, CONF for Transport Docs | DCSA TNT ShipmentEvent | Indirect only via HL; no eDocumentation API |
| 1.5 | Rates | ✅ | Hapag-Lloyd Prices API v2.1.2 | Quotations | Proprietary | Via Hapag-Lloyd API |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❓ | Not confirmed in HL TNT spec | -- | `ECP` | May be in HL Commercial Schedules response |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❓ | Not confirmed in HL TNT spec | -- | `EFC` | May be in HL Commercial Schedules response |
| 2.3 | Documentation Cutoff | DCO | ❓ | Not confirmed in HL TNT spec | -- | `DCO` | Likely in HL Commercial Schedules response |
| 2.4 | VGM Cutoff | VCO | ❓ | Not confirmed in HL TNT spec | -- | `VCO` | Likely in HL Commercial Schedules response |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ❓ | Not confirmed in HL TNT spec | -- | `FCO` | Likely in HL Commercial Schedules response |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❓ | Not confirmed in HL TNT spec | -- | `LCO` | Likely in HL Commercial Schedules response |

> **Note on Cutoffs**: Cutoff availability mirrors Hapag-Lloyd's status. The 6 cutoff fields are not confirmed in HL's public TNT spec but are likely available in the DCSA Commercial Schedules point-to-point response. Needs verification with authenticated access.

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ⚠️ | Hapag-Lloyd TNT Events | Inferred from first EquipmentEvent | Inferred from first EquipmentEvent | No explicit assignment event; inferred |
| 3.2 | Empty Container Gate-Out (Pickup) | ✅ | Hapag-Lloyd TNT Events | `GTOT` + `EMPTY` | `GTOT` + `EMPTY` | Via HL API |
| 3.3 | Full Container Gate-In | ✅ | Hapag-Lloyd TNT Events | `GTIN` + `LADEN` | `GTIN` + `LADEN` | Via HL API |
| 3.4 | Container Loaded on Vessel | ✅ | Hapag-Lloyd TNT Events | `LOAD` + `LADEN` | `LOAD` + `LADEN` | Via HL API |
| 3.5 | Container Discharged at Transshipment | ✅ | Hapag-Lloyd TNT Events | `DISC` + `LADEN` at T/S port | `DISC` + `LADEN` + transshipment | Via HL API; infer T/S from route |
| 3.6 | Container Loaded at Transshipment | ✅ | Hapag-Lloyd TNT Events | `LOAD` + `LADEN` at T/S port | `LOAD` + `LADEN` + transshipment | Via HL API |
| 3.7 | Container Discharged at Destination | ✅ | Hapag-Lloyd TNT Events | `DISC` + `LADEN` at destination | `DISC` + `LADEN` | Via HL API |
| 3.8 | Full Container Gate-Out (Delivery) | ✅ | Hapag-Lloyd TNT Events | `GTOT` + `LADEN` | `GTOT` + `LADEN` | Via HL API |
| 3.9 | Empty Container Returned | ✅ | Hapag-Lloyd TNT Events | `GTIN` + `EMPTY` | `GTIN` + `EMPTY` | Via HL API |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ✅ | Hapag-Lloyd TNT Events | `DEPA` + `PLN/EST/ACT` | `DEPA` + classifier | Via HL API |
| 4.2 | Estimated Time of Arrival | ETA | ✅ | Hapag-Lloyd TNT Events | `ARRI` + `PLN/EST/ACT` | `ARRI` + classifier | Via HL API |
| 4.3 | Vessel Arrival at Transshipment | -- | ✅ | Hapag-Lloyd TNT Events | `ARRI` at intermediate port | `ARRI` at intermediate | Via HL API |
| 4.4 | Vessel Departure from Transshipment | -- | ✅ | Hapag-Lloyd TNT Events | `DEPA` at intermediate port | `DEPA` at intermediate | Via HL API |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❌ | Not available (Hapag-Lloyd TNT does not yet support webhooks) |
| Event Polling with timestamp filter | ✅ | Via Hapag-Lloyd: `eventCreatedDateTime` with `:gte`, `:gt`, `:lte`, `:lt`, `:eq` operators |
| Event Classifier Progression (PLN->EST->ACT) | ✅ | Via Hapag-Lloyd: both Transport and Equipment events support PLN, EST, ACT classifiers |
| Retracted Events | ❓ | Not documented in Hapag-Lloyd's public spec |
| Change Remarks | ❓ | Not found in Hapag-Lloyd's analyzed OpenAPI spec |
| Delay Reason Codes | ❓ | Not found in Hapag-Lloyd's analyzed OpenAPI spec |

### Coverage Summary

| Category | Fields Available | Fields Unavailable | Fields Unknown | Coverage % |
|----------|-----------------|-------------------|----------------|-----------|
| API Domains (1.x) | 3/5 | 0/5 | 0/5 | 60% (2 partial) |
| Cutoffs (2.x) | 0/6 | 0/6 | 6/6 | 0% confirmed |
| Container Milestones (3.x) | 8/9 | 0/9 | 0/9 | 89% (1 partial) |
| Transport Events (4.x) | 4/4 | 0/4 | 0/4 | 100% |
| Change Detection (5.x) | 2/6 | 1/6 | 3/6 | 33% |
| **Total** | **17/30** | **1/30** | **9/30** | **57% confirmed** |

> **Note**: CSAV has no independent API. These coverage numbers are identical to Hapag-Lloyd's, since all CSAV container operations are handled by Hapag-Lloyd. The 57% confirmed coverage understates likely real coverage -- see Hapag-Lloyd inventory for detailed assessment. With authenticated Hapag-Lloyd API access, coverage is estimated at 75-85%.

---

## Endpoint Reference

CSAV has no API endpoints. All endpoints are provided by Hapag-Lloyd. See the [Hapag-Lloyd API inventory](../hapag-lloyd/api-inventory.md) for the complete endpoint reference, including:

- **Tracking/Events**: `GET https://api.hlag.com/hlag/external/v2/events/`
- **Schedules**: DCSA Commercial Schedules v1.0.1, OVS v3.0.7
- **Pricing**: Prices API v2.1.2
- **Mock/Sandbox**: `GET https://mock.api-portal.hlag.com/v2/events/`

### Lookup Methods Summary

| Identifier Type | Supported? | Which Endpoints? | Notes |
|----------------|-----------|-----------------|-------|
| **Bill of Lading (B/L) number** | ✅ | Hapag-Lloyd TNT via `transportDocumentReference` | Via HL API |
| **Booking reference** | ✅ | Hapag-Lloyd TNT via `carrierBookingReference` | Via HL API |
| **Container number** | ✅ | Hapag-Lloyd TNT via `equipmentReference` | CSAV prefixes CSVU, LNXU tracked via HL |
| **Carrier booking number** | ✅ | Same as booking reference | Via HL API |
| **Vessel IMO / voyage** | ⚠️ | Hapag-Lloyd TNT -- filter only, not primary lookup | Via HL API |

---

## Rate Limits & Quotas

N/A -- CSAV has no API. Rate limits for Hapag-Lloyd APIs:

| Detail | Value | Source |
|--------|-------|--------|
| **Tryout tier** | 100 calls/day, 10 calls/min | Official (Hapag-Lloyd TNT API docs) |
| **Default tier** | 6,000 calls/day, 10 calls/min | Official |
| **Premium tier** | 100,000 calls/day, 150 calls/min | Official |

See Hapag-Lloyd inventory for full rate limit details.

---

## Webhook / Push Support

N/A -- CSAV has no API. Hapag-Lloyd TNT does not yet support webhooks for shipment tracking. Polling-only strategy required. See Hapag-Lloyd inventory for details.

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | CSAV has no tracking portal. Use Hapag-Lloyd: [https://www.hapag-lloyd.com/en/tracking.html](https://www.hapag-lloyd.com/en/tracking.html) |
| **Login required?** | No (basic tracking on HL); Yes (full features) |
| **Data available on portal but NOT in API** | Per Hapag-Lloyd's FAQ, the website currently shows more complete data than the BETA API |
| **Scraping feasibility** | Difficult -- Hapag-Lloyd website is behind Cloudflare challenge |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | No (CSAV directly). Via Hapag-Lloyd: Yes |
| **EDI message types** | Via Hapag-Lloyd: IFTMIN, COPARN, BAPLIE, IFTSTA |
| **EDI connection method** | Via Hapag-Lloyd |
| **EDI documentation** | Contact Hapag-Lloyd |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Yes (via Hapag-Lloyd) | project44 supports Hapag-Lloyd; CSAV shipments tracked under HLCU |
| **FourKites** | Yes (via Hapag-Lloyd, estimated) | FourKites supports Hapag-Lloyd |
| **Vizion** | Yes | Vizion explicitly maps CSAV to carrier code HLCU ([source](https://docs.vizionapi.com/docs/supported-carriers)) |
| **INTTRA / E2open** | Yes (via Hapag-Lloyd) | Hapag-Lloyd is a founding member of INTTRA |
| **CargoSmart** | Yes (via Hapag-Lloyd) | CargoSmart supports Hapag-Lloyd |

> **Aggregator note**: All third-party aggregator access to CSAV shipment data flows through Hapag-Lloyd. Vizion explicitly lists CSAV with carrier code HLCU, confirming the full merger of digital infrastructure. There is no separate CSAV data channel.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown -- see Hapag-Lloyd inventory | Unknown |
| **API uptime/reliability** | Unknown -- Hapag-Lloyd TNT is labeled BETA | Unknown |
| **Historical data depth** | Unknown -- see Hapag-Lloyd inventory | Unknown |
| **Timezone handling** | ISO 8601 with timezone offsets (via Hapag-Lloyd) | Official (HL OpenAPI spec) |
| **Character encoding** | UTF-8 (via Hapag-Lloyd) | Official |

### Known Issues & Gotchas

- CSAV has no API -- all access is through Hapag-Lloyd. The primary "gotcha" is ensuring the carrier registry correctly maps CHIW to HLCU
- Container prefixes CSVU and LNXU must be recognized as Hapag-Lloyd containers in the SDK
- Legacy CSAV booking references may still be in circulation; these should resolve through Hapag-Lloyd's tracking system
- See Hapag-Lloyd inventory for HL-specific gotchas (mock server format mismatch, BETA data gaps vs. website, etc.)

### Recently Deprecated or Changed

- CSAV closed all directly operated container services in July 2020. The merger with Hapag-Lloyd was completed in December 2014. There is nothing to deprecate -- CSAV never had an API.

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | No standalone adapter needed -- use Hapag-Lloyd adapter with SCAC alias |
| **Implementation effort** | Minimal -- SCAC mapping only (CHIW -> HLCU) |
| **DCSA base adapter usable?** | N/A -- use Hapag-Lloyd adapter directly |

### Recommended Approach

Do not build a separate CSAV adapter. CSAV has no independent API infrastructure. Instead:

1. **Register CHIW as an alias for HLCU** in the carrier adapter registry. When the SDK receives a tracking request with SCAC code CHIW (CSAV), it should route to the Hapag-Lloyd adapter.
2. **Register container prefixes CSVU and LNXU** in the container-to-carrier mapping table, pointing to Hapag-Lloyd.
3. **No additional code is required** beyond the alias configuration.

This is the same pattern that should be used for other absorbed carriers (e.g., UASC -> Hapag-Lloyd, Nile Dutch -> Hapag-Lloyd).

### Recommended Lookup Method

Use the same lookup methods as Hapag-Lloyd: Bill of Lading (`transportDocumentReference`), Booking Reference (`carrierBookingReference`), or Container Number (`equipmentReference`). Container number is the most reliable for CSAV containers since CSVU/LNXU prefixes directly identify the equipment.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Same as Hapag-Lloyd: every 2-4 hours for active shipments |
| **Incremental filter** | `eventCreatedDateTime:gte` (Hapag-Lloyd TNT parameter) |
| **Batch tracking** | One call per container/booking/BL -- no batch endpoint via Hapag-Lloyd |

### Auth Implementation Notes

Use Hapag-Lloyd authentication: API Key via `X-IBM-Client-Id` and `X-IBM-Client-Secret` headers. No separate CSAV credentials exist or are needed.

### Edge Cases to Handle

- Legacy CSAV booking references: older systems may still reference CSAV bookings. These should be queryable through Hapag-Lloyd's `carrierBookingReference` parameter
- CSAV SCAC code confusion: some systems may use CHIW, others may already use HLCU for the same shipment. The SDK should normalize both to the Hapag-Lloyd adapter
- Container prefix lookup: CSVU and LNXU containers should be recognized as Hapag-Lloyd-operated

### Mapping Complexity

Zero additional mapping complexity beyond the Hapag-Lloyd adapter. The CSAV "adapter" is purely a routing alias. All event formats, field names, and response structures are identical to Hapag-Lloyd since the data comes from the same API.

---

## Open Questions

- [ ] Does SSL have any active shipments still referencing CSAV booking numbers? If so, do they resolve through Hapag-Lloyd's tracking?
- [ ] Are there any legacy EDI connections that still use CSAV (CHIW) as the carrier identifier?
- [ ] Should the SDK explicitly warn users when they query CSAV that results come from Hapag-Lloyd?

---

## Source Links

| Resource | URL |
|----------|-----|
| CSAV Website | [https://www.csav.com](https://www.csav.com) |
| CSAV Business Overview | [https://www.csav.com/our-business/](https://www.csav.com/our-business/) |
| Hapag-Lloyd Developer Portal | [https://api-portal.hlag.com](https://api-portal.hlag.com) |
| Hapag-Lloyd API Inventory | [../hapag-lloyd/api-inventory.md](../hapag-lloyd/api-inventory.md) |
| Hapag-Lloyd/CSAV Merger Press Release | [https://www.hapag-lloyd.com/en/press/releases/2014/12/hapag-lloyd-and-csav-complete-the-merger-and-become-the-fourth-l_37308.html](https://www.hapag-lloyd.com/en/press/releases/2014/12/hapag-lloyd-and-csav-complete-the-merger-and-become-the-fourth-l_37308.html) |
| Vizion Supported Carriers (CSAV -> HLCU) | [https://docs.vizionapi.com/docs/supported-carriers](https://docs.vizionapi.com/docs/supported-carriers) |
| CSAV Wikipedia | [https://en.wikipedia.org/wiki/CSAV](https://en.wikipedia.org/wiki/CSAV) |
| FreightWaves Merger Coverage | [https://www.freightwaves.com/news/hapag-lloyd-csav-complete-merger](https://www.freightwaves.com/news/hapag-lloyd-csav-complete-merger) |
