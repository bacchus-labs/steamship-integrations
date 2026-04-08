# Seaboard Marine -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing. Research based on Seaboard Marine's public website, MySeaboard portal documentation, EDI service pages, DCSA membership records, third-party aggregator listings, and community resource searches. No API credentials were obtained because Seaboard Marine does not offer a public API.
> **Researched by**: Agent (carrier API audit workflow)
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | Seaboard Marine Ltd. |
| **SCAC Code** | SMLU (note: listed as SEAL in steamship-lines.md but SEAL belongs to SeaLand/Maersk; multiple authoritative sources confirm SMLU) |
| **Parent Company** | Seaboard Corporation (wholly-owned subsidiary, established 1983) |
| **Alliance** | Independent |
| **Primary Services** | Container (dry, refrigerated, specialized, project cargo, LCL) |
| **Market Position** | Regional specialist, Caribbean Basin / Central America / South America. ~25 vessels, 60,000+ containers, serves 26+ countries and ~40 ports in the Western Hemisphere |
| **Headquarters** | Miami, Florida, USA |
| **Website** | [https://www.seaboardmarine.com](https://www.seaboardmarine.com) |

### Seaboard Marine Digital Ecosystem

| Entity | Role | URL |
|--------|------|-----|
| **Seaboard Marine Website** | Corporate site, public tracking, schedule search | [seaboardmarine.com](https://www.seaboardmarine.com) |
| **MySeaboard** | Customer portal for booking, tracking, schedules, documents, reports | [myseaboard.seaboardmarine.com](https://myseaboard.seaboardmarine.com) |
| **Seaboard Marine Mobile App** | iOS/Android app for tracking and services | [App Store](https://apps.apple.com/us/app/seaboard-marine/id982102311) |

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | **No** |
| **Developer portal URL** | N/A |
| **API documentation URL(s)** | N/A -- no public API documentation exists |
| **Documentation quality** | **None** -- no API documentation available. Web portal and EDI service pages exist but do not describe REST/SOAP APIs |
| **OpenAPI/Swagger spec available?** | No |
| **Sandbox/test environment?** | No |
| **Developer registration** | N/A -- no developer registration process exists |
| **Developer support channels** | General customer service only; EDI inquiries: EDIAdmin@seaboardmarine.com |
| **Community/third-party libraries** | None found -- no GitHub repos, npm packages, or PyPI packages for Seaboard Marine API integration |
| **API changelog / release notes** | Not published |

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | No |
| **DCSA APIs implemented** | None |
| **DCSA TNT version** | N/A |
| **DCSA Booking version** | N/A |
| **DCSA Schedules version** | N/A |
| **Known DCSA deviations** | N/A |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Yes | COARRI, CODECO, COPRAR, COREOR, CUSCAR, CUSRES, BAPLIE, VERMAS, APERAK |
| **ANSI X.12 (EDI)** | Yes | Messages 300, 301, 304, 309, 310, 315, 322, 323, 204, 214, 990, 997 |
| **INTTRA integration** | Unknown | "SM-line" logo appears on INTTRA carrier network page but may refer to SM Line (SMLM) rather than Seaboard Marine |
| **BIC (Bureau International des Containers)** | Yes | SMLU prefix on container IDs follows BIC/ISO 6346 standard |
| **UN/LOCODE** | Yes | Port codes used in schedules and EDI messaging |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | N/A (no API) |
| **Auth documentation** | N/A |
| **Registration process** | N/A for API. MySeaboard portal registration available for customers. EDI setup requires contacting EDIAdmin@seaboardmarine.com |
| **Registration URL** | [MySeaboard registration](https://myseaboard.seaboardmarine.com/) |
| **Partner program required?** | N/A for API. EDI requires business relationship |
| **Partner program URL** | N/A |
| **Credential type** | N/A |
| **Token refresh supported?** | N/A |
| **Token lifetime** | N/A |
| **Access tiers** | N/A |
| **IP whitelisting required?** | N/A |

### Access Requirements Summary for SSL

Seaboard Marine does not offer a public REST/SOAP API. There is no self-service developer registration or API key issuance. To obtain programmatic access to Seaboard Marine data, SSL has two options:

1. **EDI Integration**: Requires establishing a business relationship with Seaboard Marine and setting up EDI connectivity via AS2 (preferred), FTP, SFTP, or VAN. Contact EDIAdmin@seaboardmarine.com to initiate. EDI 315 (Shipment Status) and EDI 323 (Vessel Schedule) would provide the core tracking and schedule data SSL needs.

2. **Third-party aggregator**: Vizion API lists Seaboard Marine (SMLU) as "Coming Soon." Once available, this may provide API-based tracking without direct carrier integration. Other aggregators (project44, FourKites) have not confirmed Seaboard Marine support.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field must have a row.
> ✅ = Available | ❌ = Not available | ⚠️ = Partial / limited | ❓ = Unknown
>
> **Important context**: Seaboard Marine has no public REST/SOAP API. Field availability below is assessed across all access methods: EDI, web portal, and potential aggregator access. The "Carrier Endpoint" column references the access method rather than a REST endpoint.

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ⚠️ | EDI 323 / MySeaboard portal | EDI 323 "Vessel Schedule and Itinerary" | N/A (not DCSA) | Available via EDI 323 and web portal real-time schedule search. No REST API |
| 1.2 | Point-to-Point Route Options | ⚠️ | MySeaboard portal / seaboardmarine.com route search | Web-based route search tool | N/A | Available through web portal route search only. Not available via EDI or API |
| 1.3 | Booking Lifecycle | ⚠️ | EDI 300/301 / MySeaboard portal | EDI 300 (request), 301 (confirmation) | N/A | FCL and reefer bookings via portal; booking request/confirmation via EDI |
| 1.4 | Shipping Instructions | ⚠️ | EDI 304 / MySeaboard portal | EDI 304 "Ocean Shipping Instructions" | N/A | Shipping instructions via EDI 304. B/L preview available in portal |
| 1.5 | Rates | ⚠️ | MySeaboard portal / seaboardmarine.com | Rate request form, tariff search | N/A | Rate requests via web form. No programmatic rate API. EDI 310 provides B/L data with freight charges |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❓ | Unknown | Unknown | `ECP` | Not confirmed in any publicly documented EDI or portal output. May be in EDI 301 booking confirmation |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❓ | Unknown | Unknown | `EFC` | Not confirmed. May be in EDI 301 booking confirmation |
| 2.3 | Documentation Cutoff | DCO | ⚠️ | EDI 323 / MySeaboard portal | Likely in schedule/booking data | `DCO` | Cutoff times typically included in sailing schedule data. Confirmed available on portal schedule views but specific field mapping unverified |
| 2.4 | VGM Cutoff | VCO | ⚠️ | MySeaboard portal / VERMAS | VGM submission via portal and EDIFACT VERMAS | `VCO` | Portal supports VGM submission, implying cutoff date is communicated. Specific EDI field unverified |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ⚠️ | EDI 323 / MySeaboard portal | Likely in schedule data | `FCO` | Standard cutoff typically in sailing schedule data. Specific field mapping unverified |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❓ | Unknown | Unknown | `LCO` | Seaboard Marine handles LCL cargo but specific LCL cutoff data availability unverified |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ❓ | Unknown | Unknown | Inferred from first EquipmentEvent | Not confirmed in EDI or portal data. May be implied by EDI 301 booking confirmation |
| 3.2 | Empty Container Gate-Out (Pickup) | ⚠️ | EDI 315 / EDI 322 / MySeaboard portal | EDI 315 status event; EDI 322 terminal outgate | `GTOT` + `EMPTY` | EDI 322 provides terminal gate-out events. Portal shows equipment tracking |
| 3.3 | Full Container Gate-In | ⚠️ | EDI 315 / EDI 322 / MySeaboard portal | EDI 315 status event; EDI 322 terminal ingate | `GTIN` + `LADEN` | EDI 322 provides terminal gate-in events |
| 3.4 | Container Loaded on Vessel | ⚠️ | EDI 315 / MySeaboard portal | EDI 315 "loaded on vessel" status | `LOAD` + `LADEN` | EDI 315 reports cargo loading events |
| 3.5 | Container Discharged at Transshipment | ⚠️ | EDI 315 / MySeaboard portal | EDI 315 discharge event at intermediate port | `DISC` + `LADEN` + transshipment | EDI 315 reports discharge events; transshipment distinction depends on EDI detail level |
| 3.6 | Container Loaded at Transshipment | ⚠️ | EDI 315 / MySeaboard portal | EDI 315 load event at intermediate port | `LOAD` + `LADEN` + transshipment | Same as above for loading at transshipment port |
| 3.7 | Container Discharged at Destination | ⚠️ | EDI 315 / MySeaboard portal | EDI 315 discharge event at destination | `DISC` + `LADEN` | EDI 315 reports cargo arrival/discharge events |
| 3.8 | Full Container Gate-Out (Delivery) | ⚠️ | EDI 315 / EDI 322 / MySeaboard portal | EDI 315/322 terminal outgate (laden) | `GTOT` + `LADEN` | EDI 322 provides terminal gate-out events |
| 3.9 | Empty Container Returned | ⚠️ | EDI 315 / EDI 322 / MySeaboard portal | EDI 315/322 terminal ingate (empty) | `GTIN` + `EMPTY` | EDI 322 reports empty returns at terminal |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ⚠️ | EDI 323 / EDI 315 / MySeaboard portal | EDI 323 schedule; EDI 315 vessel departure status | `DEPA` + classifier | EDI 323 provides vessel schedules with ETD. Portal shows real-time schedule data |
| 4.2 | Estimated Time of Arrival | ETA | ⚠️ | EDI 323 / EDI 315 / MySeaboard portal | EDI 323 schedule; EDI 315 vessel arrival status | `ARRI` + classifier | EDI 323 provides vessel schedules with ETA. Portal shows real-time schedule data |
| 4.3 | Vessel Arrival at Transshipment | -- | ⚠️ | EDI 315 / MySeaboard portal | EDI 315 vessel arrival at intermediate port | `ARRI` at intermediate | Depends on EDI 315 detail level for transshipment events |
| 4.4 | Vessel Departure from Transshipment | -- | ⚠️ | EDI 315 / MySeaboard portal | EDI 315 vessel departure from intermediate port | `DEPA` at intermediate | Depends on EDI 315 detail level for transshipment events |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❌ | No webhook/push capability. No API exists to support subscriptions |
| Event Polling with timestamp filter | ❌ | No API endpoint to poll. EDI 315 messages are pushed by Seaboard Marine per EDI schedule |
| Event Classifier Progression (PLN→EST→ACT) | ❓ | EDI 315 may include event status qualifiers, but DCSA-style PLN/EST/ACT progression is not documented |
| Retracted Events | ❓ | Not documented for EDI 315 |
| Change Remarks | ❓ | EDI 315 may include free-text remarks but not documented |
| Delay Reason Codes | ❓ | Not documented for EDI 315 |

### Coverage Summary

> Coverage is assessed for **REST/SOAP API availability** (the primary integration method for the SDK). Fields marked ⚠️ (available via EDI/portal only, not via API) are counted separately below.

| Category | API Available | EDI/Portal Only (⚠️) | Unavailable (❌) | Unknown (❓) | API Coverage % |
|----------|--------------|----------------------|-----------------|-------------|---------------|
| API Domains (1.x) | 0/5 | 5/5 | 0/5 | 0/5 | 0% |
| Cutoffs (2.x) | 0/6 | 3/6 | 0/6 | 3/6 | 0% |
| Container Milestones (3.x) | 0/9 | 8/9 | 0/9 | 1/9 | 0% |
| Transport Events (4.x) | 0/4 | 4/4 | 0/4 | 0/4 | 0% |
| Change Detection (5.x) | 0/6 | 0/6 | 2/6 | 4/6 | 0% |
| **Total** | **0/30** | **20/30** | **2/30** | **8/30** | **0%** |

> **Coverage note**: The 0% coverage reflects that **no data is available via a REST/SOAP API**. However, if EDI integration is established, effective coverage would be significantly higher:
>
> | Category | EDI Coverage | EDI Fields Available | Notes |
> |----------|-------------|---------------------|-------|
> | API Domains (1.x) | ~80% | 4/5 | Schedules (323), Booking (300/301), SI (304), B/L (310). No rate API |
> | Cutoffs (2.x) | ~50% (estimated) | ~3/6 | DCO, VCO, FCO likely in schedule/booking data. ERD, EFC, LCO uncertain |
> | Container Milestones (3.x) | ~89% | 8/9 | EDI 315 + 322 cover most milestones. Container assignment (3.1) uncertain |
> | Transport Events (4.x) | ~100% | 4/4 | EDI 323 (schedules) + EDI 315 (vessel movement status) |
> | Change Detection (5.x) | ~17% | 1/6 | EDI 315 pushes are event-driven (no polling needed), but no webhooks, retraction, or classifier progression |
> | **EDI Total (estimated)** | **~67%** | **~20/30** | **Estimated based on EDI message type capabilities** |

---

## Endpoint Reference

Seaboard Marine does not expose REST/SOAP API endpoints. This section is replaced by the EDI message reference below.

### EDI Message Reference

#### ANSI X.12 Transaction Sets

| Message | Name | Purpose | SSL Relevance |
|---------|------|---------|---------------|
| 300 | Booking Request | Reserve cargo space | Booking lifecycle (1.3) |
| 301 | Booking Confirmation | Confirm booking | Booking lifecycle (1.3), may contain cutoff times |
| 304 | Ocean Shipping Instructions | Shipper's letter of instruction | Shipping instructions (1.4) |
| 309 | AMS Manifest | US Customs automated manifest | Regulatory compliance |
| 310 | Bill of Lading / Ocean Invoice | B/L data with freight charges | Documentation, rates (partial) |
| 315 | Shipment Status | Cargo receipt, departure, arrival events | Core tracking: milestones (3.x), transport events (4.x) |
| 322 | Terminal Operations / Ramp Activity | Gate in/out events | Gate milestones (3.2, 3.3, 3.8, 3.9) |
| 323 | Vessel Schedule and Itinerary | Sailing schedules | Schedules (1.1), ETD/ETA (4.1, 4.2), cutoffs (2.x) |
| 204 | Motor Carrier Load Tender | Inland transport offer | Out of scope for ocean tracking |
| 214 | Transportation Carrier Shipment Status | Inland status updates | Out of scope for ocean tracking |
| 990 | Load Tender Response | Response to 204 | Out of scope for ocean tracking |
| 997 | Functional Acknowledgement | EDI validation/error reporting | EDI infrastructure |

#### UN/EDIFACT Message Types

| Message | Name | Purpose | SSL Relevance |
|---------|------|---------|---------------|
| COARRI | Container Discharge/Loading Report | Reports on containers discharged/loaded | Load/discharge events (3.4-3.7) |
| CODECO | Container Gate In/Out Report | Container gate movements | Gate events (3.2, 3.3, 3.8, 3.9) |
| COPRAR | Container Discharge/Loading Order | Orders for container handling | Operational |
| COREOR | Container Release Order | Container release instructions | Delivery (3.8) |
| CUSCAR | Customs Cargo Report | Customs declaration data | Regulatory |
| CUSRES | Customs Response | Customs clearance status | Regulatory |
| BAPLIE | Bayplan/Stowage Plan | Vessel stowage information | Vessel operations |
| VERMAS | Verified Gross Mass | VGM declarations | VGM compliance (2.4) |
| APERAK | Application Error/Acknowledgment | Error reporting | EDI infrastructure |

### Lookup Methods Summary

| Identifier Type | Supported? | Which Methods? | Notes |
|----------------|-----------|---------------|-------|
| **Bill of Lading (B/L) number** | ⚠️ | MySeaboard portal, EDI 315 | Portal tracking confirmed. EDI 315 references B/L |
| **Booking reference** | ⚠️ | MySeaboard portal, EDI 300/301 | Portal tracking confirmed |
| **Container number** | ⚠️ | MySeaboard portal, EDI 315/322 | Portal equipment tracking confirmed |
| **Carrier booking number** | ⚠️ | MySeaboard portal | Same as booking reference for Seaboard Marine |
| **Vessel IMO / voyage** | ⚠️ | MySeaboard portal, EDI 323 | Portal vessel/voyage tracking confirmed |

> All lookup methods require either EDI connectivity or web portal access. No REST/SOAP API lookup is available.

---

## Rate Limits & Quotas

| Detail | Value | Source |
|--------|-------|--------|
| **Global rate limit** | N/A (no API) | Official |
| **Per-endpoint limits** | N/A | Official |
| **Daily/monthly quota** | N/A | Official |
| **Rate limit response** | N/A | Official |
| **Rate limit by** | N/A | Official |
| **Burst allowance** | N/A | Official |
| **Different tiers** | N/A | Official |

---

## Webhook / Push Support

| Detail | Value |
|--------|-------|
| **Webhooks supported?** | No |
| **Subscription endpoint** | N/A |
| **Subscription management** | N/A |
| **Subscribable event types** | N/A |
| **Callback format** | N/A |
| **Callback authentication** | N/A |
| **Retry policy on failure** | N/A |
| **Documented reliability** | N/A |

> **EDI push note**: While there are no webhooks, EDI 315 messages are inherently push-based -- Seaboard Marine sends status updates to the trading partner's EDI system as events occur. This provides a form of event-driven notification, though it requires EDI infrastructure rather than HTTP callbacks.

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | [https://www.seaboardmarine.com/tracking/](https://www.seaboardmarine.com/tracking/) (public), [https://myseaboard.seaboardmarine.com/](https://myseaboard.seaboardmarine.com/) (full portal) |
| **Login required?** | Yes for full features; limited public tracking available |
| **Data available on portal but NOT in API** | All portal data -- there is no API. Portal provides: booking status, B/L preview, equipment tracking, vessel/voyage tracking, sailing schedules, customizable reports |
| **Scraping feasibility** | Not assessed. MySeaboard requires login. Public tracking page structure not evaluated for scraping. Terms of service not reviewed |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Yes -- extensive support |
| **EDI message types** | ANSI X.12: 300, 301, 304, 309, 310, 315, 322, 323, 204, 214, 990, 997. EDIFACT: COARRI, CODECO, COPRAR, COREOR, CUSCAR, CUSRES, BAPLIE, VERMAS, APERAK |
| **EDI connection method** | AS2 (preferred), FTP, SFTP, VAN |
| **EDI documentation** | [https://www.seaboardmarine.com/electronic-data-interchange/](https://www.seaboardmarine.com/electronic-data-interchange/) |
| **EDI contact** | EDIAdmin@seaboardmarine.com |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Unknown | Not confirmed in public carrier lists. Seaboard Marine's regional focus may limit inclusion |
| **FourKites** | Unknown | Not confirmed in public carrier lists |
| **Vizion** | Coming Soon | Listed as SMLU with "Coming Soon" status on Vizion supported carriers page |
| **INTTRA / E2open** | Unknown | "SM-line" logo on INTTRA carrier network page, but this may be SM Line (SMLM) not Seaboard Marine. INTTRA's network of 60+ carriers could include Seaboard Marine given their EDI capabilities |
| **CargoSmart** | Unknown | No specific confirmation found |
| **Terminal49** | No | SMLU not listed in Terminal49's shipping lines |
| **OpenTrack** | Yes (limited) | Supports tracking after CSM activation. MBL-only not supported; requires POL/POD UN/LOCODEs in API requests |

> **Aggregator note**: Given Seaboard Marine's lack of a REST API, aggregator integration would be the most practical path for SSL's SDK. Vizion's "Coming Soon" status is the most promising lead. OpenTrack already supports Seaboard Marine with caveats.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown | Unknown |
| **API uptime/reliability** | N/A (no API) | Official |
| **Historical data depth** | Unknown for EDI. Portal likely shows active shipments only | Estimated |
| **Timezone handling** | Unknown | Unknown |
| **Character encoding** | Unknown for EDI; web portal likely UTF-8 | Estimated |

### Known Issues & Gotchas

- **No API**: The most significant limitation. All programmatic access requires EDI infrastructure or web scraping
- **SCAC discrepancy**: The carrier's SCAC is SMLU, not SEAL (which belongs to SeaLand/Maersk). This must be corrected in `docs/steamship-lines.md`
- **Regional carrier**: Seaboard Marine operates exclusively in the Western Hemisphere (Caribbean, Central/South America). Trade lane coverage is limited compared to global carriers
- **EDI setup overhead**: EDI integration requires business relationship establishment, connectivity setup (AS2/SFTP), and message mapping -- significantly more effort than REST API integration
- **Portal age**: MySeaboard portal page metadata shows last update May 2020, suggesting limited ongoing digital investment

### Recently Deprecated or Changed

- No deprecation notices found. The carrier's digital services appear stable but static.

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | Partial -- No REST/SOAP API exists. An adapter could be built using (a) a third-party aggregator when available (Vizion "Coming Soon"), (b) EDI integration if SSL establishes B2B connectivity, or (c) web scraping (not recommended) |
| **Implementation effort** | Very High (no API). EDI adapter: High. Aggregator adapter: Medium (once Vizion adds SMLU support) |
| **DCSA base adapter usable?** | No -- fully custom. Seaboard Marine is not DCSA-compliant and has no REST API |

### Recommended Approach

The recommended approach for Seaboard Marine is a **multi-tiered strategy**:

1. **Near-term (aggregator)**: Wait for Vizion to activate SMLU support (currently "Coming Soon"). Once available, build a Vizion-backed adapter that translates Vizion's standardized container events to SSL's canonical model. This avoids the overhead of direct EDI integration while providing tracking data. Also evaluate OpenTrack as an interim option (already supports Seaboard Marine with POL/POD requirements).

2. **Medium-term (EDI)**: If SSL's business needs require deeper integration (booking, shipping instructions, schedules, cutoffs), establish EDI connectivity with Seaboard Marine via AS2. Build an EDI adapter that processes X.12 315 (status), 322 (terminal ops), and 323 (schedules) messages. This provides the richest data but requires significant infrastructure investment.

3. **Not recommended**: Web portal scraping. The MySeaboard portal requires authentication, and scraping is fragile, potentially violates ToS, and difficult to maintain.

### Recommended Lookup Method

Container number is the most universally supported identifier across Seaboard Marine's tracking options (portal, EDI 315, EDI 322, and third-party aggregators like OpenTrack). Bill of Lading number is also widely supported. Booking reference works well in the portal and EDI 300/301 flows.

For aggregator-based tracking (Vizion, OpenTrack), container number is the primary lookup method. OpenTrack additionally requires POL/POD UN/LOCODEs.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | N/A for direct integration (no API to poll). For aggregator: follow aggregator's recommended interval (typically every 2-4 hours) |
| **Incremental filter** | EDI 315 is push-based (event-driven). For aggregator: use aggregator's event timestamp filtering |
| **Batch tracking** | EDI: one message per shipment event. Aggregator: depends on provider (Vizion supports individual container tracking) |

### Auth Implementation Notes

No API authentication to implement. For EDI, connectivity is established at the transport layer (AS2 certificates, SFTP credentials) rather than application-layer auth. For aggregator access, implement the aggregator's authentication (e.g., Vizion API key).

### Edge Cases to Handle

- **SCAC code confusion**: Ensure the adapter uses SMLU (not SEAL) when communicating with aggregators or matching carrier data
- **Regional trade lanes**: Seaboard Marine serves only Western Hemisphere routes. Lookups for containers on other trade lanes will return no results
- **EDI message timing**: EDI 315 messages may not be real-time; they depend on Seaboard Marine's processing schedule and EDI infrastructure latency
- **Transshipment granularity**: EDI 315 may not clearly distinguish transshipment events from origin/destination events, requiring inference from port codes

### Mapping Complexity

Without a REST API, there is no direct JSON/XML response to map. If using an aggregator (Vizion, OpenTrack), mapping complexity depends on the aggregator's event model -- typically medium complexity as aggregators provide pre-normalized data. For EDI, mapping complexity is high: X.12 315 uses positional segments and element codes that must be parsed and translated to DCSA-equivalent events. The carrier's proprietary event codes in EDI 315 would need to be mapped to DCSA equipment/transport event type codes.

---

## Open Questions

- [ ] Does SSL have an existing business relationship with Seaboard Marine?
- [ ] Is SSL already set up for EDI with any carriers? (Would reduce incremental effort for Seaboard Marine EDI)
- [ ] When will Vizion activate SMLU support? (Currently "Coming Soon")
- [ ] Is the SCAC code in steamship-lines.md (SEAL) a data entry error? Multiple sources confirm SMLU. SEAL is SeaLand/Maersk
- [ ] Does Seaboard Marine's EDI 315 include event qualifier codes that could map to PLN/EST/ACT progression?
- [ ] Does INTTRA/E2open include Seaboard Marine in their carrier network? (The "SM-line" logo is ambiguous)
- [ ] What is the actual data freshness for Seaboard Marine's EDI 315 messages?

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | [https://www.seaboardmarine.com](https://www.seaboardmarine.com) |
| About Page | [https://www.seaboardmarine.com/about/](https://www.seaboardmarine.com/about/) |
| MySeaboard Portal | [https://myseaboard.seaboardmarine.com](https://myseaboard.seaboardmarine.com) |
| Public Tracking | [https://www.seaboardmarine.com/tracking/](https://www.seaboardmarine.com/tracking/) |
| EDI Documentation | [https://www.seaboardmarine.com/electronic-data-interchange/](https://www.seaboardmarine.com/electronic-data-interchange/) |
| EDI Services Page | [https://www.seaboardmarine.com/services/electronic-data-interchange/](https://www.seaboardmarine.com/services/electronic-data-interchange/) |
| MySeaboard Features | [https://www.seaboardmarine.com/new-to-myseaboard/](https://www.seaboardmarine.com/new-to-myseaboard/) |
| Mobile App (iOS) | [https://apps.apple.com/us/app/seaboard-marine/id982102311](https://apps.apple.com/us/app/seaboard-marine/id982102311) |
| Seaboard Corporation (Parent) | [https://www.seaboardcorp.com/our-companies/seaboard-marine/](https://www.seaboardcorp.com/our-companies/seaboard-marine/) |
| DCSA Members | [https://dcsa.org](https://dcsa.org) |
| Vizion Supported Carriers | [https://docs.vizionapi.com/docs/supported-carriers](https://docs.vizionapi.com/docs/supported-carriers) |
| INTTRA Carrier Network | [https://www.inttra.com/ocean-carrier-network/](https://www.inttra.com/ocean-carrier-network/) |
| OpenTrack - Seaboard Marine | [https://support.opentrack.co/en/articles/9454527-tracking-seaboard-marine](https://support.opentrack.co/en/articles/9454527-tracking-seaboard-marine) |
| Terminal49 - Seaboard Marine Terminal | [https://terminal49.com/terminals/m988-seaboard-marine](https://terminal49.com/terminals/m988-seaboard-marine) |
