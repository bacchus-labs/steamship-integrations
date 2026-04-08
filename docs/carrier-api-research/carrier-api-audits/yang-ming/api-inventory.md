# Yang Ming Line -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing
> **Researched by**: Claude (automated research agent)
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | Yang Ming Marine Transport Corp. (Yang Ming Line / YML) |
| **SCAC Code** | YMLU |
| **Parent Company** | Yang Ming Marine Transport Corp. (independent, publicly traded on TWSE) |
| **Alliance** | THE Alliance (with Hapag-Lloyd, ONE, HMM) |
| **Primary Services** | Container shipping |
| **Market Position** | ~9th largest container shipping line globally; Taiwan's second-largest carrier (after Evergreen); fleet of ~100 vessels, ~724,000 TEU capacity |
| **Headquarters** | Keelung, Taiwan |
| **Website** | [https://www.yangming.com](https://www.yangming.com/en) |

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | No (landing page only) |
| **Developer portal URL** | [https://www.yangming.com/en/esolution/digital_solution/api_introduction](https://www.yangming.com/en/esolution/digital_solution/api_introduction) |
| **API documentation URL(s)** | N/A -- no public API documentation; technical details provided only after onboarding |
| **Documentation quality** | Poor -- the public-facing page describes APIs generically with no endpoints, schemas, or technical reference |
| **OpenAPI/Swagger spec available?** | No (not publicly available) |
| **Sandbox/test environment?** | Unknown |
| **Developer registration** | Requires partnership -- click "Apply API" button, Yang Ming contacts you; not self-service |
| **Developer support channels** | Not publicly documented; likely via regional sales/customer service contacts |
| **Community/third-party libraries** | None found |
| **API changelog / release notes** | Not published |

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | Yes -- founding member (April 2019) |
| **DCSA APIs implemented** | TNT (live) |
| **DCSA TNT version** | v2.2 (Official -- Yang Ming's API page references DCSA T&T v2.2, with upgrade path from v1.1) |
| **DCSA Booking version** | N/A -- no booking API announced |
| **DCSA Schedules version** | N/A -- no DCSA-compliant schedule API announced |
| **Known DCSA deviations** | Unknown -- no public documentation to assess deviations; specific implementation details only available after onboarding |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Yes | EDI listed as a digital solution on Yang Ming's e-solution portal |
| **INTTRA integration** | Yes (reported) | INTTRA/E2open platform supports DCSA-compliant carriers; Yang Ming is a DCSA founding member |
| **BIC (Bureau International des Containers)** | Unknown | |
| **UN/LOCODE** | Yes (estimated) | Expected given DCSA TNT v2.2 compliance, which uses UN/LOCODE for port references |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | Unknown -- not publicly documented |
| **Auth documentation** | N/A |
| **Registration process** | 1. Visit API introduction page. 2. Click "Apply API". 3. Yang Ming contacts you to discuss access. |
| **Registration URL** | [https://www.yangming.com/en/esolution/digital_solution/api_introduction](https://www.yangming.com/en/esolution/digital_solution/api_introduction) |
| **Partner program required?** | Yes -- for any access (application-based, not self-service) |
| **Partner program URL** | Same as registration URL |
| **Credential type** | Unknown |
| **Token refresh supported?** | Unknown |
| **Token lifetime** | Unknown |
| **Access tiers** | Unknown |
| **IP whitelisting required?** | Unknown |

### Access Requirements Summary for SSL

SSL would need to submit an API access request through Yang Ming's "Apply API" portal. This is not self-service -- Yang Ming's team will reach out to discuss integration requirements, likely involving a business relationship or partnership agreement. No public documentation describes the credentials, access tiers, or technical requirements. SSL should expect a multi-step onboarding process that may take weeks. Given that Yang Ming implements DCSA TNT v2.2, the authentication mechanism is likely OAuth2 or API key-based (common among DCSA adopters), but this cannot be confirmed without direct engagement with Yang Ming's technical team.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field must have a row.
> Available = Available | Unavailable = Not available | Partial = Partial / limited | Unknown = Unknown

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ⚠️ | Web portal only (no confirmed API) | Schedule data on portal | CS (if aligned) | Schedules available on web portal in HTML/TEXT/CSV/XML download; no programmatic API confirmed |
| 1.2 | Point-to-Point Route Options | ⚠️ | Web portal only | P2P search on portal | CS P2P | Point-to-Point search available at e-solution.yangming.com but no API endpoint confirmed |
| 1.3 | Booking Lifecycle | ❌ | N/A | N/A | N/A | E-booking available on web portal; no booking API announced |
| 1.4 | Shipping Instructions | ❌ | N/A | N/A | N/A | SI submission via web portal, FAX, or EDI; no API |
| 1.5 | Rates | ❌ | N/A | N/A | N/A | No rates API found |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❓ | Unknown | Unknown | `ECP` | DCSA TNT v2.2 spec supports cutoffs; Yang Ming implementation unknown without API access |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❓ | Unknown | Unknown | `EFC` | Same as above |
| 2.3 | Documentation Cutoff | DCO | ❓ | Unknown | Unknown | `DCO` | Same as above |
| 2.4 | VGM Cutoff | VCO | ❓ | Unknown | Unknown | `VCO` | VGM submission supported via mobile app and EDI; cutoff availability in API unknown |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ❓ | Unknown | Unknown | `FCO` | Same as above |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❓ | Unknown | Unknown | `LCO` | Same as above |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ⚠️ | DCSA TNT v2.2 API | Inferred from first equipment event | Inferred from first EquipmentEvent | DCSA TNT v2.2 supports this inference; confirmation requires API access |
| 3.2 | Empty Container Gate-Out (Pickup) | ✅ | DCSA TNT v2.2 API | Equipment event: gate-out + empty | `GTOT` + `EMPTY` | Standard DCSA TNT v2.2 equipment event |
| 3.3 | Full Container Gate-In | ✅ | DCSA TNT v2.2 API | Equipment event: gate-in + laden | `GTIN` + `LADEN` | Standard DCSA TNT v2.2 equipment event |
| 3.4 | Container Loaded on Vessel | ✅ | DCSA TNT v2.2 API | Equipment event: load + laden | `LOAD` + `LADEN` | Standard DCSA TNT v2.2 equipment event |
| 3.5 | Container Discharged at Transshipment | ✅ | DCSA TNT v2.2 API | Equipment event: discharge + laden + transshipment | `DISC` + `LADEN` + transshipment | Standard DCSA TNT v2.2 equipment event |
| 3.6 | Container Loaded at Transshipment | ✅ | DCSA TNT v2.2 API | Equipment event: load + laden + transshipment | `LOAD` + `LADEN` + transshipment | Standard DCSA TNT v2.2 equipment event |
| 3.7 | Container Discharged at Destination | ✅ | DCSA TNT v2.2 API | Equipment event: discharge + laden | `DISC` + `LADEN` | Standard DCSA TNT v2.2 equipment event |
| 3.8 | Full Container Gate-Out (Delivery) | ✅ | DCSA TNT v2.2 API | Equipment event: gate-out + laden | `GTOT` + `LADEN` | Standard DCSA TNT v2.2 equipment event |
| 3.9 | Empty Container Returned | ✅ | DCSA TNT v2.2 API | Equipment event: gate-in + empty | `GTIN` + `EMPTY` | Standard DCSA TNT v2.2 equipment event |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ✅ | DCSA TNT v2.2 API | Transport event: departure | `DEPA` + classifier | Standard DCSA TNT v2.2 transport event |
| 4.2 | Estimated Time of Arrival | ETA | ✅ | DCSA TNT v2.2 API | Transport event: arrival | `ARRI` + classifier | Standard DCSA TNT v2.2 transport event |
| 4.3 | Vessel Arrival at Transshipment | -- | ✅ | DCSA TNT v2.2 API | Transport event: arrival at intermediate | `ARRI` at intermediate | Standard DCSA TNT v2.2 transport event |
| 4.4 | Vessel Departure from Transshipment | -- | ✅ | DCSA TNT v2.2 API | Transport event: departure from intermediate | `DEPA` at intermediate | Standard DCSA TNT v2.2 transport event |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❓ | DCSA TNT v2.2 spec includes Subscription Callback API; Yang Ming implementation unknown |
| Event Polling with timestamp filter | ❓ | DCSA TNT v2.2 spec mandates event polling with `eventCreatedDateTime`; Yang Ming implementation unknown |
| Event Classifier Progression (PLN->EST->ACT) | ✅ | DCSA TNT v2.2 supports classifier progression on transport events |
| Retracted Events | ❓ | DCSA TNT v2.2 spec supports retracted events; Yang Ming implementation unknown |
| Change Remarks | ❓ | DCSA TNT v2.2 spec supports change remarks; Yang Ming implementation unknown |
| Delay Reason Codes | ❓ | DCSA TNT v2.2 spec supports delay reason codes; Yang Ming implementation unknown |

### Coverage Summary

| Category | Fields Available | Fields Partial | Fields Unavailable | Fields Unknown | Coverage % |
|----------|-----------------|---------------|-------------------|----------------|-----------|
| API Domains (1.x) | 0/5 | 2/5 | 3/5 | 0/5 | 0% |
| Cutoffs (2.x) | 0/6 | 0/6 | 0/6 | 6/6 | 0% |
| Container Milestones (3.x) | 8/9 | 1/9 | 0/9 | 0/9 | 89% |
| Transport Events (4.x) | 4/4 | 0/4 | 0/4 | 0/4 | 100% |
| Change Detection (5.x) | 1/6 | 0/6 | 0/6 | 5/6 | 17% |
| **Total** | **13/30** | **3/30** | **3/30** | **11/30** | **43%** |

> Note: Coverage % counts only fully Available fields. Container milestones and transport events are rated as Available based on Yang Ming's confirmed DCSA TNT v2.2 implementation, which by specification must support these event types. However, specific implementation completeness cannot be verified without live API access. Container Assigned (3.1) is Partial because it is inferred rather than explicitly reported. The 2 Partial API Domain fields (Schedules, P2P Routes) reflect web portal availability without a confirmed programmatic API. Cutoffs and most Change Detection mechanisms are Unknown because DCSA TNT v2.2 supports them in the standard, but Yang Ming's specific implementation has not been verified. Effective coverage could be significantly higher once onboarding and live testing confirm these fields.

---

## Endpoint Reference

### Tracking / Events

| Endpoint | Method | Lookup Params | Pagination | Response Format | Notes |
|----------|--------|--------------|------------|----------------|-------|
| DCSA TNT v2.2 (base path unknown) | GET | Likely: carrierBookingReference, equipmentReference, transportDocumentReference (B/L) | Unknown | JSON | Endpoint paths not publicly documented; DCSA v2.2 standard defines `/v2/events` |

### Schedules

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| Web portal only | N/A | Port, vessel, date range | N/A | HTML/TEXT/CSV/XML (download) | No programmatic schedule API confirmed |

### Booking

No booking API available.

### Other Endpoints

No other API endpoints documented.

### Lookup Methods Summary

| Identifier Type | Supported? | Which Endpoints? | Notes |
|----------------|-----------|-----------------|-------|
| **Bill of Lading (B/L) number** | ✅ (estimated) | DCSA TNT v2.2 | DCSA v2.2 supports B/L lookup via `transportDocumentReference`; web portal also supports B/L tracking |
| **Booking reference** | ✅ (estimated) | DCSA TNT v2.2 | DCSA v2.2 supports booking lookup via `carrierBookingReference`; web portal also supports booking tracking |
| **Container number** | ✅ (estimated) | DCSA TNT v2.2 | DCSA v2.2 supports container lookup via `equipmentReference`; web portal also supports container tracking |
| **Carrier booking number** | ✅ (estimated) | DCSA TNT v2.2 | Same as booking reference |
| **Vessel IMO / voyage** | ❓ | Unknown | No schedule API confirmed; vessel tracking available on web portal |

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
| **Webhooks supported?** | Unknown -- DCSA TNT v2.2 includes Subscription Callback API, but Yang Ming's implementation not confirmed |
| **Subscription endpoint** | Unknown |
| **Subscription management** | Unknown |
| **Subscribable event types** | Unknown |
| **Callback format** | If implemented, would follow DCSA v2.2 spec (event JSON POSTed to callbackUrl) |
| **Callback authentication** | Unknown |
| **Retry policy on failure** | Unknown |
| **Documented reliability** | Unknown |

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | [https://www.yangming.com/en/esolution/cargo_tracking](https://www.yangming.com/en/esolution/cargo_tracking) |
| **Login required?** | No (for basic tracking) |
| **Data available on portal but NOT in API** | Schedules (HTML/CSV/XML download), booking management, shipping instruction submission, document download, vessel tracking |
| **Scraping feasibility** | Not assessed -- portal appears to be a standard web application |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Yes |
| **EDI message types** | Not publicly documented in detail; standard EDIFACT expected (IFTMIN, COPARN, BAPLIE, IFTSTA) |
| **EDI connection method** | Not publicly documented |
| **EDI documentation** | Contact carrier -- [Digital Solutions overview](https://www.yangming.com/en/esolution/digital_solution_ov) |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Yes | [project44 Yang Ming Tracking](https://www.project44.com/tracking/container/yang-ming/) |
| **FourKites** | Yes (reported) | Major aggregator covering THE Alliance carriers |
| **Vizion** | Yes | Carrier code YMLU; B/L tracking supported, booking tracking "Coming Soon". [Supported carriers](https://docs.vizionapi.com/docs/supported-carriers) |
| **INTTRA / E2open** | Yes (reported) | INTTRA platform supports DCSA-compliant carriers; [DCSA compliance announcement](https://www.e2open.com/inttra-by-e2open-platform-compliant-with-shipping-industries-first-track-trace-standards/) |
| **CargoSmart** | Yes | Yang Ming is a GSBN founding member alongside CargoSmart. [Source](https://www.globenewswire.com/news-release/2018/11/06/1646014/0/en/Top-Ocean-Carriers-and-Terminal-Operators-Initiate-Blockchain-Consortium.html) |
| **Other**: Portcast | Yes | [Portcast Yang Ming Tracking](https://www.portcast.io/carrier-coverage/yang-ming-container-tracking) |
| **Other**: Terminal49 | Yes | [Terminal49 Yang Ming](https://terminal49.com/shipping-lines/ymlu-yangming-marine-transport-container-tracking) |
| **Other**: Dockflow | Yes | [Dockflow Yang Ming](https://dockflow.com/container-tracking/yang-ming/) |

> **Aggregator note**: Yang Ming is well-supported across all major aggregators. Given that Yang Ming's direct API requires a manual onboarding process with no public documentation, aggregators like Vizion or project44 may provide faster time-to-integration and broader data coverage. Vizion currently supports B/L tracking for Yang Ming, which may not require direct API onboarding. SSL should evaluate whether aggregator coverage meets field requirements before investing in direct API onboarding.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown | Unknown |
| **API uptime/reliability** | Unknown | Unknown |
| **Historical data depth** | Unknown | Unknown |
| **Timezone handling** | Unknown (likely UTC based on DCSA v2.2 alignment) | Estimated |
| **Character encoding** | Unknown | Unknown |

### Known Issues & Gotchas

- No public API documentation whatsoever -- all technical details are behind the onboarding gate.
- "Apply API" process is opaque -- no SLA on response time or approval criteria.
- SCAC code changed from YMLU to YMJA on October 1, 2023 per Vizion documentation, but YMLU is still widely used. The adapter should handle both.
- As a DCSA TNT v2.2 implementation, specific deviations from the standard are unknown and can only be discovered during integration testing.
- Web portal provides schedule data in downloadable formats (CSV, XML) which could serve as a fallback data source.

### Recently Deprecated or Changed

- Yang Ming previously offered DCSA T&T v1.1; the upgrade to v2.2 was announced. Existing v1.1 users were encouraged to contact their PIC to upgrade.

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | Yes -- for tracking (container milestones + transport events). Schedule and booking capabilities would require web portal scraping or aggregator. |
| **Implementation effort** | Medium (DCSA TNT v2.2 passthrough + onboarding effort + unknown deviations) |
| **DCSA base adapter usable?** | Yes -- Yang Ming implements DCSA TNT v2.2, so the DCSA base adapter should work with minimal overrides |

### Recommended Approach

The primary integration path is through Yang Ming's DCSA TNT v2.2 Track & Trace API for container milestones and transport events. Since Yang Ming implements the DCSA standard, the SDK adapter should extend the DCSA base adapter with Yang Ming-specific authentication configuration.

For schedule data, two options exist: (a) integrate through an aggregator that provides Yang Ming schedule data, or (b) implement a schedule scraper/downloader that pulls CSV/XML schedule files from Yang Ming's web portal. Neither is ideal, and SSL should assess whether aggregator schedule coverage is sufficient.

For booking and shipping instruction capabilities, there is no API path. These would need to be handled via EDI or web portal integration if required.

Given the opaque onboarding process, SSL should also maintain an aggregator-based fallback (Vizion or project44) that can provide tracking data without direct API access. This dual-path approach de-risks the integration timeline.

### Recommended Lookup Method

B/L number or container number (estimated, based on DCSA TNT v2.2 spec support). The web portal supports all three lookup types (container, B/L, booking), and the DCSA v2.2 standard supports querying by `transportDocumentReference` (B/L), `carrierBookingReference`, or `equipmentReference` (container). Actual support must be confirmed during onboarding.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Every 2-4 hours (conservative; adjust based on rate limits once known) |
| **Incremental filter** | DCSA TNT v2.2 mandates `eventCreatedDateTime` filter support -- use this for incremental polling if Yang Ming implements it |
| **Batch tracking** | DCSA v2.2 supports filtering by multiple identifiers in a single call; actual support unknown |

### Auth Implementation Notes

Authentication details are unknown. Based on other DCSA TNT v2.2 adopters (CMA CGM uses dual API Key + OAuth2, Hapag-Lloyd uses API Key, HMM uses API Key), Yang Ming likely uses either API Key or OAuth2. The adapter should be designed to support configurable auth mechanisms, defaulting to the most common DCSA pattern (API Key in header or OAuth2 client credentials).

### Edge Cases to Handle

- SCAC code duality: Yang Ming uses both YMLU and YMJA -- adapter must handle both codes in carrier identification
- Onboarding delay: adapter may need to fall back to aggregator data while direct API access is pending
- Unknown DCSA deviations: implement defensive parsing that gracefully handles missing or additional fields
- Schedule data gap: no schedule API means the adapter cannot provide programmatic schedule queries without an alternative data source
- Web portal data richness: portal exposes more data (schedules, booking management, documents) than the API

### Mapping Complexity

Low (for tracking). Yang Ming implements DCSA TNT v2.2, which means the standard DCSA event code mapping applies directly. Equipment events map to container milestones, transport events map to vessel schedule events, and the event classifier progression (PLN/EST/ACT) is standard. The main complexity is not in mapping but in the unknown areas: cutoff data availability, webhook support, and any Yang Ming-specific deviations from the DCSA spec.

---

## Open Questions

- [ ] What is the actual authentication mechanism (OAuth2, API Key, other)?
- [ ] What are the API base URL and endpoint paths?
- [ ] Does Yang Ming expose cutoff times in their TNT API response?
- [ ] Does Yang Ming implement the DCSA v2.2 Subscription Callback API (webhooks)?
- [ ] Does Yang Ming support `eventCreatedDateTime` filtering for incremental polling?
- [ ] What are the rate limits and quotas?
- [ ] Does SSL have an existing business relationship with Yang Ming that could expedite API access?
- [ ] Is a sandbox/test environment available?
- [ ] Does the TNT API support all three lookup methods (B/L, booking ref, container)?
- [ ] Are there any Yang Ming-specific deviations from the DCSA TNT v2.2 standard?
- [ ] What is the timeline for onboarding after submitting an "Apply API" request?

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | [https://www.yangming.com](https://www.yangming.com/en) |
| API Introduction | [https://www.yangming.com/en/esolution/digital_solution/api_introduction](https://www.yangming.com/en/esolution/digital_solution/api_introduction) |
| Digital Solutions Overview | [https://www.yangming.com/en/esolution/digital_solution_ov](https://www.yangming.com/en/esolution/digital_solution_ov) |
| DCSA TNT Announcement | [https://www.yangming.com/en/news/e_service_updates/14692](https://www.yangming.com/en/news/e_service_updates/14692) |
| Cargo Tracking Portal | [https://www.yangming.com/en/esolution/cargo_tracking](https://www.yangming.com/en/esolution/cargo_tracking) |
| Schedule Portal | [https://e-solution.yangming.com/e-service/schedule/schedule_ov.aspx](https://e-solution.yangming.com/e-service/schedule/schedule_ov.aspx) |
| Point-to-Point Schedule | [https://e-solution.yangming.com/e-service/schedule/PointToPoint.aspx](https://e-solution.yangming.com/e-service/schedule/PointToPoint.aspx) |
| Vessel Tracking Portal | [https://e-solution.yangming.com/e-service/vessel_tracking/SearchByVessel.aspx](https://e-solution.yangming.com/e-service/vessel_tracking/SearchByVessel.aspx) |
| DCSA Membership | [https://dcsa.org/about-us](https://dcsa.org/about-us) |
| GSBN Consortium | [https://www.globenewswire.com/news-release/2018/11/06/1646014/0/en/Top-Ocean-Carriers-and-Terminal-Operators-Initiate-Blockchain-Consortium.html](https://www.globenewswire.com/news-release/2018/11/06/1646014/0/en/Top-Ocean-Carriers-and-Terminal-Operators-Initiate-Blockchain-Consortium.html) |
| project44 Yang Ming Tracking | [https://www.project44.com/tracking/container/yang-ming/](https://www.project44.com/tracking/container/yang-ming/) |
| Vizion Supported Carriers | [https://docs.vizionapi.com/docs/supported-carriers](https://docs.vizionapi.com/docs/supported-carriers) |
| Terminal49 Yang Ming | [https://terminal49.com/shipping-lines/ymlu-yangming-marine-transport-container-tracking](https://terminal49.com/shipping-lines/ymlu-yangming-marine-transport-container-tracking) |
| Portcast Yang Ming Tracking | [https://www.portcast.io/carrier-coverage/yang-ming-container-tracking](https://www.portcast.io/carrier-coverage/yang-ming-container-tracking) |
| Dockflow Yang Ming | [https://dockflow.com/container-tracking/yang-ming/](https://dockflow.com/container-tracking/yang-ming/) |
| INTTRA DCSA Compliance | [https://www.e2open.com/inttra-by-e2open-platform-compliant-with-shipping-industries-first-track-trace-standards/](https://www.e2open.com/inttra-by-e2open-platform-compliant-with-shipping-industries-first-track-trace-standards/) |
| Mobile App (iOS) | [https://apps.apple.com/us/app/yang-ming/id573468171](https://apps.apple.com/us/app/yang-ming/id573468171) |
