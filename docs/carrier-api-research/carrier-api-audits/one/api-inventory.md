# Ocean Network Express (ONE) — API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only — not verified with live API testing. Research based on public web presence, DCSA membership records, developer portal discovery (SPA-rendered; full content not accessible without registration), EDI portal documentation, eCommerce platform analysis, third-party aggregator coverage, and industry press. No API credentials were obtained or used.
> **Researched by**: Agent (carrier API audit workflow)
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | Ocean Network Express Pte. Ltd. (ONE) |
| **SCAC Code** | ONEY |
| **Parent Company** | Joint venture of NYK Line, Mitsui O.S.K. Lines (MOL), and K Line (Kawasaki Kisen Kaisha) |
| **Alliance** | THE Alliance (with Hapag-Lloyd, HMM, Yang Ming) |
| **Primary Services** | Container shipping (fully containerized) |
| **Market Position** | 6th largest container carrier globally. Fleet capacity exceeding 1.4 million TEUs across ~240 vessels. THE Alliance connects 81 ports on 34 service loops |
| **Headquarters** | Singapore (7 Straits View, #16-01 Marina One East Tower, Singapore 018936) |
| **Website** | [https://www.one-line.com](https://www.one-line.com) |

### Background

Ocean Network Express was established on July 7, 2017, and commenced commercial operations on April 1, 2018, through the merger of the container shipping businesses of three major Japanese carriers: Nippon Yusen Kaisha (NYK), Mitsui O.S.K. Lines (MOL), and Kawasaki Kisen Kaisha (K Line). Despite being the newest of the major carriers, ONE rapidly established itself as a top-6 carrier by TEU capacity.

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | **Yes** |
| **Developer portal URL** | [https://developers.one-line.com](https://developers.one-line.com/get-started) |
| **API documentation URL(s)** | Portal is SPA-rendered; API product listings and documentation require registration. Not publicly browsable |
| **Documentation quality** | **Unknown** — portal exists and appears professional, but content could not be reviewed without registration due to SPA rendering. No publicly accessible Swagger/OpenAPI specs were found |
| **OpenAPI/Swagger spec available?** | Unknown — likely available within the developer portal after registration, but not confirmed |
| **Sandbox/test environment?** | Unknown |
| **Developer registration** | Requires creating an account. Whether approval or business relationship is additionally required is unknown |
| **Developer support channels** | Unknown — likely documented within the portal |
| **Community/third-party libraries** | **None found** — no GitHub repos, npm packages, or PyPI packages for ONE API integration |
| **API changelog / release notes** | Not published publicly |

### eCommerce Platform

ONE operates a separate eCommerce platform at [https://ecomm.one-line.com](https://ecomm.one-line.com) providing web-based services including Cargo Tracking, Mail Tracking, Rail Tracking Report (North America), booking management, and schedule search. This platform is customer-facing and distinct from the developer API portal.

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | **Yes — founding member** (one of 9 carriers that established DCSA in April 2019) ([Source](https://dcsa.org/about-us/members)) |
| **DCSA APIs implemented** | **Track & Trace (TNT)** — confirmed as implemented. Booking, Commercial Schedules, and eDocumentation are unknown. ONE was reported as "one of the first to offer a Track & Trace API based on DCSA standards" ([Source](https://splash247.com/top-carriers-adopting-dcsa-track-and-trace-standards/)) |
| **DCSA TNT version** | Unknown — likely v2.2 based on timing of other DCSA member implementations, but could not be confirmed from public sources |
| **DCSA Booking version** | Unknown — not confirmed from public sources |
| **DCSA Schedules version** | Unknown — not confirmed from public sources |
| **Known DCSA deviations** | Unknown — no deviation information available without API access |

> **Note on DCSA eBL**: ONE is adopting DCSA eBL standards through a partnership with GSBN (Global Shipping Business Network), announced in February 2025. ONE is the second DCSA member (after Hapag-Lloyd) to partner with GSBN for eBL. All DCSA members have committed to 100% eBL adoption by 2030. ([Source](https://smartmaritimenetwork.com/2025/02/25/ocean-network-express-adopts-dcsa-ebl-standards-using-gsbn-blockchain/))

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | **Yes** | Comprehensive support: IFTMBF, IFTMBC, IFTMIN, IFTMCS, IFTSTA, IFTSAI, VERMAS, CONTRL, APERAK |
| **ANSI X12 (EDI)** | **Yes** | Transaction sets: 300, 301, 304, 310, 315, 323, 997, 824 |
| **INTTRA integration** | **Yes** | ONE listed on INTTRA/E2open ocean carrier network |
| **BIC (Bureau International des Containers)** | Yes | Container IDs follow BIC ISO 6346 format (ONE prefixes: ONEU, etc.) |
| **UN/LOCODE** | Yes | Standard port codes used throughout tracking and schedule data |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | Unknown — developer portal has a dedicated "API Auth" page at https://developers.one-line.com/api-auth but content was not accessible via web fetch (SPA-rendered) |
| **Auth documentation** | https://developers.one-line.com/api-auth (requires registration/portal access) |
| **Registration process** | Create an account on the developer portal. Further steps unknown |
| **Registration URL** | [https://developers.one-line.com/get-started](https://developers.one-line.com/get-started) |
| **Partner program required?** | Unknown — portal language says "Start by creating an account, seeing our full API" which suggests some level of self-service, but whether a business relationship is required for production access is not confirmed |
| **Partner program URL** | N/A |
| **Credential type** | Unknown |
| **Token refresh supported?** | Unknown |
| **Token lifetime** | Unknown |
| **Access tiers** | Unknown |
| **IP whitelisting required?** | Unknown |

### Access Requirements Summary for SSL

ONE has a developer portal at developers.one-line.com, which is a positive sign for API accessibility. However, the portal is SPA-rendered and the specific registration process, authentication mechanism, and access requirements could not be determined without creating an account. SSL should register on the developer portal to assess the full API product catalog, authentication requirements, and any business relationship prerequisites. Given that ONE is a DCSA founding member and publicly advertises API access, the barrier to entry may be lower than carriers like MSC that require formal partner onboarding. However, this is speculative until portal registration is completed.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field must have a row.
> Availability assessed from: DCSA membership (TNT confirmed), eCommerce platform capabilities, EDI support, and third-party integrator data. Many fields are marked Unknown because specific API documentation could not be reviewed.

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ⚠️ | Unknown | Unknown | DCSA CS (if implemented) | Schedules available on eCommerce portal; EDI IFTSAI/323 supported. API endpoint unknown |
| 1.2 | Point-to-Point Route Options | ⚠️ | Unknown | Unknown | DCSA CS (if implemented) | "Dynamic point-to-point schedules and routing options" mentioned on eCommerce platform |
| 1.3 | Booking Lifecycle | ⚠️ | Unknown | Unknown | DCSA BKG (if implemented) | Booking management available via eCommerce platform and EDI (IFTMBF/300, IFTMBC/301). API availability unknown |
| 1.4 | Shipping Instructions | ⚠️ | Unknown | Unknown | DCSA eDoc (if implemented) | EDI IFTMIN/304 supported. API availability unknown |
| 1.5 | Rates | ❓ | Unknown | Unknown | N/A (not DCSA) | No evidence of a rates API. Rates may be available via eCommerce portal or through sales channels |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❓ | Unknown | Unknown | `ECP` | eCommerce platform mentions "cargo cut-off date at origin" which may include ERD. Specific field availability unknown |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❓ | Unknown | Unknown | `EFC` | Unknown |
| 2.3 | Documentation Cutoff | DCO | ⚠️ | Unknown | Unknown | `DCO` | eCommerce platform shows "upcoming deadlines" for logged-in users, likely including DCO |
| 2.4 | VGM Cutoff | VCO | ⚠️ | Unknown | Unknown | `VCO` | EDI VERMAS supported, suggesting VGM workflow is digitized. VCO likely available |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ⚠️ | Unknown | Unknown | `FCO` | "Cargo cut-off date at origin" mentioned on eCommerce platform |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❓ | Unknown | Unknown | `LCO` | Unknown |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ❓ | Unknown | Unknown | Inferred from first EquipmentEvent | Unknown |
| 3.2 | Empty Container Gate-Out (Pickup) | ⚠️ | Unknown | Unknown | `GTOT` + `EMPTY` | DCSA TNT implemented; EDI IFTSTA/315 provides container movements. Likely available but unverified |
| 3.3 | Full Container Gate-In | ⚠️ | Unknown | Unknown | `GTIN` + `LADEN` | Third-party trackers report "Gate in Full" as a tracked milestone |
| 3.4 | Container Loaded on Vessel | ⚠️ | Unknown | Unknown | `LOAD` + `LADEN` | Third-party trackers report "Loaded at POL" milestone |
| 3.5 | Container Discharged at Transshipment | ⚠️ | Unknown | Unknown | `DISC` + `LADEN` + transshipment | Likely available via DCSA TNT but unverified |
| 3.6 | Container Loaded at Transshipment | ⚠️ | Unknown | Unknown | `LOAD` + `LADEN` + transshipment | Likely available via DCSA TNT but unverified |
| 3.7 | Container Discharged at Destination | ⚠️ | Unknown | Unknown | `DISC` + `LADEN` | Third-party trackers report "Discharged at POD" milestone |
| 3.8 | Full Container Gate-Out (Delivery) | ⚠️ | Unknown | Unknown | `GTOT` + `LADEN` | Third-party trackers report "Gate out Full" milestone |
| 3.9 | Empty Container Returned | ❓ | Unknown | Unknown | `GTIN` + `EMPTY` | Unknown — not reported by third-party trackers |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ⚠️ | Unknown | Unknown | `DEPA` + classifier | Third-party trackers report "Departure from POL". Estimated dates available on eCommerce platform |
| 4.2 | Estimated Time of Arrival | ETA | ⚠️ | Unknown | Unknown | `ARRI` + classifier | ETA available on eCommerce platform and through third-party trackers |
| 4.3 | Vessel Arrival at Transshipment | -- | ⚠️ | Unknown | Unknown | `ARRI` at intermediate | Likely available via DCSA TNT but unverified |
| 4.4 | Vessel Departure from Transshipment | -- | ⚠️ | Unknown | Unknown | `DEPA` at intermediate | Likely available via DCSA TNT but unverified |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❓ Unknown | If DCSA TNT v2.2+ is implemented, webhooks should be available per DCSA spec. Unverified |
| Event Polling with timestamp filter | ⚠️ Likely | DCSA TNT mandates event polling. ONE implements DCSA TNT. Unverified but expected |
| Event Classifier Progression (PLN->EST->ACT) | ⚠️ Likely | Standard DCSA classifier progression. Expected if TNT is implemented |
| Retracted Events | ❓ Unknown | DCSA feature; availability depends on implementation completeness |
| Change Remarks | ❓ Unknown | DCSA feature; availability depends on implementation completeness |
| Delay Reason Codes | ❓ Unknown | DCSA feature; availability depends on implementation completeness |

### Coverage Summary

| Category | Fields Available | Fields Unavailable | Fields Unknown | Coverage % |
|----------|-----------------|-------------------|----------------|-----------|
| API Domains (1.x) | 0/5 | 0/5 | 1/5 | 0% (4 partial via EDI/portal; API unverified) |
| Cutoffs (2.x) | 0/6 | 0/6 | 3/6 | 0% (3 partial: DCO, VCO, FCO likely from portal "deadlines" feature) |
| Container Milestones (3.x) | 0/9 | 0/9 | 2/9 | 0% (7 partial: core milestones confirmed by third-party trackers) |
| Transport Events (4.x) | 0/4 | 0/4 | 0/4 | 0% (4 partial: ETD/ETA confirmed on eCommerce platform) |
| Change Detection (5.x) | 0/6 | 0/6 | 4/6 | 0% (2 partial: polling and classifier progression expected per DCSA) |
| **Total** | **0/30** | **0/30** | **10/30** | **0% confirmed, 67% likely, 33% unknown** |

> **Important caveat**: No fields could be marked as fully confirmed (green checkmark) because ONE's developer portal is SPA-rendered and API documentation could not be reviewed without registration. The 20 "caveat" fields (67%) reflect capabilities that are expected to exist based on strong indirect evidence: DCSA founding membership with confirmed TNT implementation, comprehensive EDI support covering the same functional areas, eCommerce platform features showing the data, and third-party tracker milestone coverage. The 10 "unknown" fields (33%) lack even indirect evidence. Zero fields were assessed as unavailable, which is consistent with ONE's position as a major DCSA carrier. To convert caveats to confirmed availability, registration on the developer portal is required.

---

## Endpoint Reference

> **Note**: Specific API endpoints could not be documented because the developer portal at developers.one-line.com is SPA-rendered and requires registration to view API documentation. The endpoint sections below reflect what is known or expected.

### Tracking / Events

| Endpoint | Method | Lookup Params | Pagination | Response Format | Notes |
|----------|--------|--------------|------------|----------------|-------|
| Unknown (DCSA TNT expected) | GET | B/L, Booking, Container (confirmed from eCommerce platform) | Unknown | JSON (expected) | ONE implements DCSA TNT; specific endpoint path unknown |

### Schedules

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| Unknown | GET | Unknown | Unknown | JSON (expected) | Schedules available on eCommerce platform; API endpoint unknown |

### Booking

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| Unknown | Unknown | Unknown | Unknown | Unknown | Booking available via eCommerce platform and EDI; API endpoint unknown |

### Lookup Methods Summary

| Identifier Type | Supported? | Which Endpoints? | Notes |
|----------------|-----------|-----------------|-------|
| **Bill of Lading (B/L) number** | Yes | Tracking (confirmed from eCommerce platform) | |
| **Booking reference** | Yes | Tracking (confirmed from eCommerce platform) | |
| **Container number** | Yes | Tracking (confirmed from eCommerce platform) | |
| **Carrier booking number** | Unknown | Unknown | |
| **Vessel IMO / voyage** | Unknown | Unknown | Vessel schedules available on eCommerce platform |

---

## Rate Limits & Quotas

| Detail | Value | Source |
|--------|-------|--------|
| **Global rate limit** | Unpublished | Unknown |
| **Per-endpoint limits** | Unpublished | Unknown |
| **Daily/monthly quota** | Unpublished | Unknown |
| **Rate limit response** | Unknown | Unknown |
| **Rate limit by** | Unknown | Unknown |
| **Burst allowance** | Unknown | Unknown |
| **Different tiers** | Unknown | Unknown |

---

## Webhook / Push Support

| Detail | Value |
|--------|-------|
| **Webhooks supported?** | Unknown — expected if DCSA TNT v2.2+ is implemented (v2.2 introduced the Subscription Callback API) |
| **Subscription endpoint** | Unknown |
| **Subscription management** | Unknown |
| **Subscribable event types** | Unknown |
| **Callback format** | Unknown (expected DCSA event JSON if implemented) |
| **Callback authentication** | Unknown |
| **Retry policy on failure** | Unknown |
| **Documented reliability** | Unknown |

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | [https://ecomm.one-line.com/one-ecom/manage-shipment/cargo-tracking](https://ecomm.one-line.com/one-ecom/manage-shipment/cargo-tracking) |
| **Login required?** | No for basic tracking; Yes for full features (upcoming deadlines, alerts) |
| **Data available on portal but NOT in API** | Unknown — cannot compare until API documentation is reviewed |
| **Scraping feasibility** | Not assessed |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | **Yes — comprehensive** |
| **EDI message types (EDIFACT)** | IFTMBF (Booking Request), IFTMBC (Booking Confirmation), IFTMIN (Shipping Instructions), IFTMCS (Bill of Lading), IFTSTA (Container Movements), IFTSAI (Schedules), VERMAS (VGM), CONTRL (Functional Ack), APERAK (Application Ack) |
| **EDI message types (ANSI X12)** | 300, 301, 304, 310, 315, 323, 997, 824 |
| **Additional formats** | XML, CSV, Flat Files |
| **EDI connection method** | AS2, FTP, SMTP email |
| **EDI documentation** | [https://www.one-line.com/en/standard-page/edi-portal](https://www.one-line.com/en/standard-page/edi-portal) |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | **Yes** | ONE container tracking available. [Source](https://www.project44.com/tracking/container/one/) |
| **FourKites** | Estimated yes | FourKites covers 85+ carriers; ONE is 6th largest globally. Not explicitly confirmed but highly probable |
| **Vizion** | **Yes** | ONE explicitly listed. Supports Container ID, Booking number, BL number lookup. [Source](https://www.vizionapi.com/carrier-tracking/ocean-network-express-one) |
| **INTTRA / E2open** | **Yes** | ONE listed on INTTRA ocean carrier network. Electronic booking, shipping instructions, BL, and tracking. [Source](https://www.inttra.com/ocean-carrier-network/) |
| **CargoSmart** | Unknown | Not explicitly confirmed from research |
| **Other**: Portcast | Yes | Real-time and predictive visibility. [Source](https://www.portcast.io/carrier-coverage/ocean-network-express-one-container-tracking) |
| **Other**: Dockflow | Yes | Satellite, carrier, and AIS data. [Source](https://dockflow.com/container-tracking/one/) |

> **Aggregator note**: Given the number of unknowns in ONE's direct API, aggregators like project44, Vizion, and INTTRA may serve as a practical fallback integration path. These aggregators already have established connections to ONE and can provide tracking data without needing to navigate ONE's developer portal registration process.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown | Unknown |
| **API uptime/reliability** | Unknown | Unknown |
| **Historical data depth** | Unknown | Unknown |
| **Timezone handling** | Unknown (UTC expected if DCSA-compliant) | Unknown |
| **Character encoding** | Unknown | Unknown |

### Known Issues & Gotchas

- Developer portal at developers.one-line.com is SPA-rendered (JavaScript-heavy single-page application), making it impossible to review API documentation without registration and browser access
- ONE was formed from three Japanese carriers (NYK, MOL, K Line) — legacy system integration may affect data consistency for older shipments or during transition periods
- THE Alliance services (shared vessel slots with Hapag-Lloyd, HMM, Yang Ming) may complicate tracking when ONE containers are on alliance partner vessels

### Recently Deprecated or Changed

- No deprecation notices identified from public sources

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | **Yes (likely)** — ONE is a DCSA founding member with a confirmed TNT implementation and a developer portal. However, feasibility cannot be fully confirmed until the developer portal is accessed |
| **Implementation effort** | Low to Medium (estimated) — if ONE implements standard DCSA APIs, a DCSA base adapter with thin configuration layer should work. Cannot confirm until API docs are reviewed |
| **DCSA base adapter usable?** | Yes (expected) — ONE's DCSA TNT implementation should be compatible with a shared DCSA adapter. Deviations unknown |

### Recommended Approach

ONE should be approachable as a DCSA-compliant carrier, similar to the approach used for Maersk, Hapag-Lloyd, and Evergreen. The first step is to register on the developer portal at developers.one-line.com and review the full API catalog to determine exactly which DCSA APIs are implemented and at what versions.

If ONE implements DCSA TNT v2.2 (as is likely based on the timeline of other carrier implementations), the SDK adapter can extend the shared DCSA base adapter class with ONE-specific configuration (base URL, authentication, any DCSA deviations). If they have upgraded to TNT v3, even better — fewer deviations from the latest standard are expected.

As a fallback or complement, integration through aggregators (project44, Vizion, or INTTRA) should be evaluated. These aggregators already provide ONE tracking data and may offer a faster path to integration if the direct API proves difficult to access or has limitations.

### Recommended Lookup Method

Bill of Lading (B/L) number or Container number — both confirmed as supported through the eCommerce platform. B/L number provides shipment-level context (all containers on a shipment), while container number provides granular per-container tracking. The DCSA TNT standard supports both.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Every 2-4 hours (estimated — cannot determine optimal interval without knowing rate limits and data freshness) |
| **Incremental filter** | Use `eventCreatedDateTime > lastPollTime` if DCSA TNT is implemented (mandatory per DCSA spec) |
| **Batch tracking** | Unknown — DCSA TNT typically supports one shipment per query. Batch capability unknown |

### Auth Implementation Notes

Authentication mechanism is unknown. The developer portal has a dedicated API Auth page, suggesting non-trivial auth (likely OAuth2 or JWT based on industry patterns). SSL will need to register on the portal to determine the exact flow. Given that other DCSA carriers use OAuth2 (Maersk, CMA CGM) or JWT (Evergreen), one of these is the most likely mechanism.

### Edge Cases to Handle

- THE Alliance vessel sharing: ONE containers may be on Hapag-Lloyd, HMM, or Yang Ming vessels. Tracking events should still flow through ONE's API for ONE bookings, but vessel details may reference partner vessels
- Legacy carrier transition: ONE was formed from NYK, MOL, and K Line in 2018. Very old bookings or references from pre-2018 may use legacy SCAC codes
- Multi-carrier transshipment: Transshipment events at alliance hub ports may involve containers being handled across multiple alliance partners

### Mapping Complexity

If ONE implements standard DCSA TNT, mapping complexity should be **low** — the DCSA event model maps directly to the canonical data model defined in `docs/required-data-fields.md`. The primary mapping concern would be identifying which DCSA version is in use (v2.2 vs v3) as there are structural differences between versions (single `/events` endpoint in v2.2 vs separate event type endpoints in v3, presence/absence of `isTransshipmentMove` field, etc.).

---

## Open Questions

- [ ] What specific API products are listed on the developer portal? (requires registration at developers.one-line.com)
- [ ] What DCSA TNT version does ONE implement? (v2.2 or v3)
- [ ] Does ONE implement DCSA Booking, Commercial Schedules, or eDocumentation APIs?
- [ ] What is the authentication mechanism? (OAuth2, JWT, API Key?)
- [ ] What are the rate limits and quotas?
- [ ] Is there a sandbox/test environment?
- [ ] Does ONE support webhooks/event subscriptions (DCSA Subscription Callback API)?
- [ ] What is the event data freshness (latency from physical event to API availability)?
- [ ] Does SSL have an existing business relationship with ONE?
- [ ] Is portal registration self-service or does it require carrier approval?

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | [https://www.one-line.com](https://www.one-line.com) |
| Developer Portal | [https://developers.one-line.com](https://developers.one-line.com/get-started) |
| Developer Portal - API Auth | [https://developers.one-line.com/api-auth](https://developers.one-line.com/api-auth) |
| eCommerce Platform | [https://ecomm.one-line.com](https://ecomm.one-line.com) |
| Cargo Tracking (Web) | [https://ecomm.one-line.com/one-ecom/manage-shipment/cargo-tracking](https://ecomm.one-line.com/one-ecom/manage-shipment/cargo-tracking) |
| EDI Portal | [https://www.one-line.com/en/standard-page/edi-portal](https://www.one-line.com/en/standard-page/edi-portal) |
| DCSA Members Page | [https://dcsa.org/about-us/members](https://dcsa.org/about-us/members) |
| DCSA TNT Adoption Article | [https://splash247.com/top-carriers-adopting-dcsa-track-and-trace-standards/](https://splash247.com/top-carriers-adopting-dcsa-track-and-trace-standards/) |
| DCSA eBL/GSBN Announcement | [https://smartmaritimenetwork.com/2025/02/25/ocean-network-express-adopts-dcsa-ebl-standards-using-gsbn-blockchain/](https://smartmaritimenetwork.com/2025/02/25/ocean-network-express-adopts-dcsa-ebl-standards-using-gsbn-blockchain/) |
| project44 ONE Tracking | [https://www.project44.com/tracking/container/one/](https://www.project44.com/tracking/container/one/) |
| Vizion ONE Tracking | [https://www.vizionapi.com/carrier-tracking/ocean-network-express-one](https://www.vizionapi.com/carrier-tracking/ocean-network-express-one) |
| INTTRA Carrier Network | [https://www.inttra.com/ocean-carrier-network/](https://www.inttra.com/ocean-carrier-network/) |
| Stedi EDI Network | [https://www.stedi.com/edi/network/ocean-network-express](https://www.stedi.com/edi/network/ocean-network-express) |
| Google Cloud Case Study | [https://cloud.google.com/customers/one](https://cloud.google.com/customers/one) |
