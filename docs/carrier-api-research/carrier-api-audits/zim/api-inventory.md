# ZIM Integrated Shipping Services -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing
> **Researched by**: Agent
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | ZIM Integrated Shipping Services Ltd. (commonly "ZIM") |
| **SCAC Code** | ZIMU |
| **Parent Company** | ZIM (publicly traded, Israel). Hapag-Lloyd acquisition agreement signed 2026-02-17 (~$4.2B); regulatory approvals expected late 2026. Until closing, ZIM operates independently |
| **Alliance** | Independent (no alliance membership). Operates vessel sharing agreements (VSAs) and slot charter arrangements with multiple carriers |
| **Primary Services** | Container shipping on all major global trade routes. Modern fleet with focus on trans-Pacific, Asia-Mediterranean, Atlantic, Intra-Asia trades |
| **Market Position** | 10th-largest container shipping line globally |
| **Headquarters** | Haifa, Israel |
| **Website** | https://www.zim.com |

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | Yes |
| **Developer portal URL** | https://api.zim.com/ |
| **API documentation URL(s)** | https://api.zim.com/ (Azure API Management portal; requires login to view API specs). Secondary site: https://docs.zimconnections.com/ (Redoc-based; content not publicly accessible during research) |
| **Documentation quality** | Poor (from external perspective) -- API portal exists but all documentation is behind authentication. No public Swagger/OpenAPI specs, no publicly visible endpoint descriptions, no developer guides accessible without login |
| **OpenAPI/Swagger spec available?** | Unknown -- likely available within the authenticated portal (Azure API Management and Redoc both typically serve OpenAPI specs). Not accessible publicly |
| **Sandbox/test environment?** | Unknown -- no public mention of sandbox or test environment |
| **Developer registration** | Requires approval -- organizations must apply for and obtain a security token ("API Token") through the registration process at api.zim.com |
| **Developer support channels** | API support page: https://www.zim.com/contact-us/zim-api-support |
| **Community/third-party libraries** | None found -- no ZIM-specific shipping API wrapper libraries on GitHub, npm, or PyPI |
| **API changelog / release notes** | Not published publicly |

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | Yes -- founding member (April 2019) alongside MSC, Maersk, CMA CGM, Hapag-Lloyd, ONE, Evergreen, Yang Ming, HMM |
| **DCSA APIs implemented** | TNT (Track & Trace) -- adopted per DCSA announcement (April 2021). Specific implementation details not publicly confirmed |
| **DCSA TNT version** | Unknown -- likely v2.2 based on DCSA membership timeline and standard adoption announcements, but version not publicly confirmed for ZIM specifically |
| **DCSA Booking version** | N/A -- no public evidence of DCSA Booking API implementation |
| **DCSA Schedules version** | N/A -- no public evidence of DCSA Commercial Schedules API implementation |
| **Known DCSA deviations** | None documented publicly |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Yes | Bilateral EDI supported. Specific message types not publicly listed but INTTRA eVGM (VERMAS) confirmed. Likely IFTMIN, COPARN, IFTSTA, BAPLIE based on carrier size |
| **INTTRA integration** | Yes | ZIM is an INTTRA carrier partner. Booking, tracking, and eVGM via INTTRA platform. Source: https://www.zim.com/tools/ecommerce-partners |
| **BIC (Bureau International des Containers)** | Yes | Standard container ID format used (B/L prefix: ZIMU) |
| **UN/LOCODE** | Yes (assumed) | Expected for any DCSA-adopting carrier |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | API Token (subscription key via Azure API Management). Specific mechanism (API Key header, Bearer token, or OAuth2) not confirmed from public sources |
| **Auth documentation** | Behind login at https://api.zim.com/ |
| **Registration process** | 1. Visit https://api.zim.com/ 2. Sign up for an account 3. Apply for API Token 4. Organization reviewed and approved 5. Token issued with rate limits defined |
| **Registration URL** | https://api.zim.com/profile |
| **Partner program required?** | Unknown -- registration appears to require organizational approval, suggesting a business relationship may be needed |
| **Partner program URL** | N/A |
| **Credential type** | API Token (specific format unknown -- Azure API Management typically uses subscription keys passed as headers) |
| **Token refresh supported?** | Unknown |
| **Token lifetime** | Unknown |
| **Access tiers** | Rate limits (calls per minute/day) defined during registration per API Terms. Specific tiers not publicly documented |
| **IP whitelisting required?** | Unknown |

### Access Requirements Summary for SSL

ZIM's API access requires organizational registration and approval through the Azure API Management portal at api.zim.com. The process is not self-service in the way that some portals are -- organizations must apply and be approved before receiving API tokens. The API Terms and Conditions state that tokens cannot be shared with third parties unless pre-approved, and usage is metered by calls per minute/day.

SSL will need to register an organizational account, go through whatever approval process ZIM requires (likely verification of shipping industry relationship), and then obtain API tokens. The exact timeline for approval is not publicly documented. Given ZIM's pending acquisition by Hapag-Lloyd (expected to close late 2026), SSL should consider whether to invest in a direct ZIM integration or plan for eventual migration to Hapag-Lloyd's API platform.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field has a row.
> Since ZIM's API documentation is entirely behind authentication, most assessments below are based on: (1) ZIM's DCSA membership and T&T adoption announcement, (2) web portal capabilities, (3) myZIM platform features, and (4) industry-standard expectations for a top-10 carrier. Confidence is lower than for carriers with publicly documented APIs.

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ⚠️ | Unknown API endpoint. Web portal: https://www.zim.com/schedules (search by point-to-point, port, vessel, line) | Unknown | DCSA CS v1 (if implemented) | Schedule data available on web portal; likely exposed via API but not confirmed. No DCSA CS implementation confirmed |
| 1.2 | Point-to-Point Route Options | ⚠️ | Unknown API endpoint. Web portal supports point-to-point schedule search | Unknown | DCSA CS v1 (if implemented) | Available on web portal; API exposure unconfirmed |
| 1.3 | Booking Lifecycle | ⚠️ | Unknown API endpoint. myZIM platform supports booking creation/management | Unknown | N/A | myZIM provides booking functionality. eZIM (legacy) closed Dec 2025, migrated to myZIM. API booking endpoints likely exist given api.zim.com portal but unconfirmed |
| 1.4 | Shipping Instructions | ⚠️ | Unknown API endpoint. myZIM supports SI submission for confirmed bookings | Unknown | N/A | myZIM provides SI submission. API endpoint existence unconfirmed |
| 1.5 | Rates | ❓ | Unknown | Unknown | N/A (not DCSA) | No evidence of rates API |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❓ | Unknown | Unknown | `ECP` | If ZIM implements DCSA TNT with booking/schedule data, cutoffs may be included. Unconfirmed |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❓ | Unknown | Unknown | `EFC` | Same as 2.1 |
| 2.3 | Documentation Cutoff | DCO | ❓ | Unknown | Unknown | `DCO` | Same as 2.1 |
| 2.4 | VGM Cutoff | VCO | ❓ | Unknown | Unknown | `VCO` | ZIM supports eVGM via INTTRA, so VGM cutoff data likely exists in their systems |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ❓ | Unknown | Unknown | `FCO` | Same as 2.1 |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❓ | Unknown | Unknown | `LCO` | Same as 2.1 |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ❓ | Unknown | Unknown | Inferred from first EquipmentEvent | If DCSA TNT implemented, inferred from first equipment event |
| 3.2 | Empty Container Gate-Out (Pickup) | ⚠️ | Track & Trace API (assumed DCSA TNT) | Expected: `GTOT` + `EMPTY` | `GTOT` + `EMPTY` | Web portal tracking shows container movement events. DCSA adoption implies these milestones are available via API |
| 3.3 | Full Container Gate-In | ⚠️ | Track & Trace API (assumed DCSA TNT) | Expected: `GTIN` + `LADEN` | `GTIN` + `LADEN` | Same rationale as 3.2 |
| 3.4 | Container Loaded on Vessel | ⚠️ | Track & Trace API (assumed DCSA TNT) | Expected: `LOAD` + `LADEN` | `LOAD` + `LADEN` | Same rationale as 3.2 |
| 3.5 | Container Discharged at Transshipment | ⚠️ | Track & Trace API (assumed DCSA TNT) | Expected: `DISC` + `LADEN` + transshipment | `DISC` + `LADEN` + transshipment | Same rationale as 3.2 |
| 3.6 | Container Loaded at Transshipment | ⚠️ | Track & Trace API (assumed DCSA TNT) | Expected: `LOAD` + `LADEN` + transshipment | `LOAD` + `LADEN` + transshipment | Same rationale as 3.2 |
| 3.7 | Container Discharged at Destination | ⚠️ | Track & Trace API (assumed DCSA TNT) | Expected: `DISC` + `LADEN` | `DISC` + `LADEN` | Same rationale as 3.2 |
| 3.8 | Full Container Gate-Out (Delivery) | ⚠️ | Track & Trace API (assumed DCSA TNT) | Expected: `GTOT` + `LADEN` | `GTOT` + `LADEN` | Same rationale as 3.2 |
| 3.9 | Empty Container Returned | ⚠️ | Track & Trace API (assumed DCSA TNT) | Expected: `GTIN` + `EMPTY` | `GTIN` + `EMPTY` | Same rationale as 3.2 |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ⚠️ | Track & Trace API (assumed DCSA TNT); Schedules web portal | Expected: `DEPA` + classifier (PLN/EST/ACT) | `DEPA` + classifier | Web portal shows schedule data with ETD. DCSA TNT adoption implies transport events available via API |
| 4.2 | Estimated Time of Arrival | ETA | ⚠️ | Track & Trace API (assumed DCSA TNT); Schedules web portal | Expected: `ARRI` + classifier (PLN/EST/ACT) | `ARRI` + classifier | Same rationale as 4.1 |
| 4.3 | Vessel Arrival at Transshipment | -- | ⚠️ | Track & Trace API (assumed DCSA TNT) | Expected: `ARRI` at intermediate port | `ARRI` at intermediate | Same rationale as 4.1 |
| 4.4 | Vessel Departure from Transshipment | -- | ⚠️ | Track & Trace API (assumed DCSA TNT) | Expected: `DEPA` at intermediate port | `DEPA` at intermediate | Same rationale as 4.1 |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❓ | Unknown -- DCSA TNT v2.2 includes optional subscription endpoints but ZIM's implementation status is unconfirmed. No public documentation of webhook capabilities |
| Event Polling with timestamp filter | ⚠️ | Expected if DCSA TNT implemented -- `GET /events` with `eventCreatedDateTime` filter is mandatory per DCSA TNT spec. Unconfirmed for ZIM specifically |
| Event Classifier Progression (PLN->EST->ACT) | ⚠️ | Expected if DCSA TNT implemented -- standard classifier progression. Unconfirmed for ZIM specifically |
| Retracted Events | ❓ | Unknown -- supported in DCSA TNT spec but carrier implementation varies |
| Change Remarks | ❓ | Unknown -- supported in DCSA TNT spec but carrier implementation varies |
| Delay Reason Codes | ❓ | Unknown -- supported in DCSA TNT spec but carrier implementation varies |

### Coverage Summary

| Category | Fields Available | Fields Partial/Caveat | Fields Unavailable | Fields Unknown | Coverage % |
|----------|-----------------|----------------------|-------------------|----------------|-----------|
| API Domains (1.x) | 0/5 | 4/5 | 0/5 | 1/5 | 0% confirmed (80% with caveats) |
| Cutoffs (2.x) | 0/6 | 0/6 | 0/6 | 6/6 | 0% confirmed |
| Container Milestones (3.x) | 0/9 | 8/9 | 0/9 | 1/9 | 0% confirmed (89% with caveats) |
| Transport Events (4.x) | 0/4 | 4/4 | 0/4 | 0/4 | 0% confirmed (100% with caveats) |
| Change Detection (5.x) | 0/6 | 2/6 | 0/6 | 4/6 | 0% confirmed (33% with caveats) |
| **Total** | **0/30** | **18/30** | **0/30** | **12/30** | **0% confirmed (60% with caveats)** |

> **Notes on Coverage:**
> - ZIM's API documentation is entirely behind authentication, making confirmed coverage impossible from desk research alone.
> - The "with caveats" percentages reflect ZIM's DCSA founding membership and T&T standard adoption announcement, which strongly implies DCSA TNT event support. However, the specific DCSA TNT version, implementation completeness, and any deviations are unknown.
> - All container milestones and transport events are marked as "Available with caveats" because ZIM's web portal tracking shows these events, and their DCSA adoption announcement covers T&T. The caveat is that API-level access has not been confirmed.
> - Cutoffs are entirely unknown because cutoff data typically comes from booking/schedule APIs, and ZIM's implementation of these is unconfirmed.
> - Schedules, booking, and shipping instructions are available on the web portal (myZIM) but API exposure for these domains is unconfirmed.
> - No fields are marked as unavailable because ZIM's full API capability is hidden behind authentication. A carrier of this size is likely to have more than what's publicly visible.

---

## Endpoint Reference

> ZIM's API endpoint paths, methods, parameters, and response formats are not publicly documented. The following is based on the known existence of the api.zim.com portal and the docs.zimconnections.com documentation site.

### Tracking / Events

| Endpoint | Method | Lookup Params | Pagination | Response Format | Notes |
|----------|--------|--------------|------------|----------------|-------|
| Unknown (DCSA TNT expected) | GET | Expected: B/L, Booking ref, Container number (per DCSA TNT standard and web portal tracking) | Unknown (DCSA cursor-based expected) | JSON (expected) | ZIM adopted DCSA T&T standards. Endpoint paths require portal access to confirm |

### Schedules

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| Unknown | GET | Expected: port, vessel, date range, point-to-point (per web portal capabilities) | Unknown | JSON (expected) | Web portal at https://www.zim.com/schedules supports port, vessel, line, and P2P search |

### Lookup Methods Summary

| Identifier Type | Supported? | Which Endpoints? | Notes |
|----------------|-----------|-----------------|-------|
| **Bill of Lading (B/L) number** | ⚠️ (web portal confirmed) | Web portal tracking; likely API tracking endpoint | B/L format: ZIMU + 8-12 alphanumeric characters. Vizion also supports ZIM B/L tracking |
| **Booking reference** | ⚠️ (web portal confirmed) | Web portal tracking; likely API tracking endpoint | Supported on web tracking portal and Vizion |
| **Container number** | ⚠️ (web portal confirmed) | Web portal tracking; likely API tracking endpoint | Supported on web tracking portal and Vizion |
| **Carrier booking number** | ❓ | Unknown | May be same as booking reference |
| **Vessel IMO / voyage** | ⚠️ (web portal confirmed) | Web portal schedules | Schedules searchable by vessel on web portal |

---

## Rate Limits & Quotas

| Detail | Value | Source |
|--------|-------|--------|
| **Global rate limit** | Yes -- defined during registration (calls per minute/day). Specific numbers unpublished | Official (API Terms) |
| **Per-endpoint limits** | Unpublished | Unknown |
| **Daily/monthly quota** | Unpublished | Unknown |
| **Rate limit response** | Unknown | Unknown |
| **Rate limit by** | Per-API Token (per organization) | Estimated (based on Azure API Management typical behavior) |
| **Burst allowance** | Unknown | Unknown |
| **Different tiers** | Unknown -- rate limits set during registration may vary by organization | Estimated |

---

## Webhook / Push Support

| Detail | Value |
|--------|-------|
| **Webhooks supported?** | Unknown -- no public documentation found. DCSA TNT v2.2 includes optional subscription endpoints but ZIM's implementation is unconfirmed |
| **Subscription endpoint** | Unknown |
| **Subscription management** | Unknown |
| **Subscribable event types** | Unknown |
| **Callback format** | Unknown |
| **Callback authentication** | Unknown |
| **Retry policy on failure** | Unknown |
| **Documented reliability** | Unknown |

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | https://www.zim.com/tools/track-a-shipment |
| **Login required?** | No -- public tracking by container number, B/L, or booking number |
| **Data available on portal but NOT in API** | Unknown (API capabilities cannot be assessed without portal access). Portal shows container movement events, ETAs, vessel information |
| **Scraping feasibility** | Not assessed -- API should be the preferred access method. Multiple third-party aggregators already support ZIM tracking |
| **Additional tracking tools** | US Inland Tracing Status: https://www.zim.com/tools/us-inland-tracing-status |

### myZIM Platform

| Detail | Value |
|--------|-------|
| **URL** | https://www.zim.com/digital-solutions/myzim-personal-area |
| **Login required?** | Yes |
| **Features** | Personalized dashboard for all import/export shipments. B/L approval and editing online. 24/7 cargo tracking with temperature data for reefer containers. Shipping instruction submission for confirmed bookings. Commodity code lookup. Document management (booking confirmations, arrival notices, delivery orders). PayCargo integration for online payment |
| **Note** | eZIM platform closed end of December 2025; all functionality migrated to myZIM |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Yes |
| **EDI message types** | Bilateral EDI supported. eVGM via INTTRA confirmed (VERMAS). Full message type list not publicly documented but likely includes IFTMIN, COPARN, IFTSTA, BAPLIE based on carrier size and INTTRA partnership |
| **EDI connection method** | Bilateral EDI (direct connection). Also via INTTRA, Infor Nexus, CargoSmart portals |
| **EDI documentation** | Contact ZIM directly or use partner portal integration |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Yes | ZIM included in project44's ocean visibility coverage (98%+ of global ocean freight). Source: https://www.project44.com/platform/visibility/ocean/ |
| **FourKites** | Yes (reported) | FourKites covers 85+ ocean carriers; ZIM as a top-10 carrier is almost certainly included. Not explicitly confirmed in search results |
| **Vizion** | Yes | ZIMU listed as supported carrier. B/L and Booking tracking confirmed. Source: https://docs.vizionapi.com/docs/supported-carriers |
| **INTTRA / E2open** | Yes | ZIM is an INTTRA carrier partner for booking, tracking, eVGM. Source: https://www.zim.com/tools/ecommerce-partners |
| **CargoSmart** | Yes | Listed as ZIM eCommerce partner. Source: https://www.zim.com/tools/ecommerce-partners |
| **Infor Nexus** | Yes | Listed as ZIM eCommerce partner (formerly GT Nexus). Source: https://www.zim.com/tools/ecommerce-partners |
| **Other**: TrackingMore | Yes | Third-party tracking API supporting ZIM. Source: https://www.trackingmore.com/zim-tracking-api |
| **Other**: WAVE BL | Yes | Digital release of original Bills of Lading. Source: https://www.zim.com/tools/ecommerce-partners |

> **Aggregator note:** Given that ZIM's direct API documentation is not publicly accessible, aggregator platforms (particularly Vizion and project44) may provide the fastest path to ZIM tracking data for SSL. Vizion explicitly supports B/L and booking-based tracking for ZIM. This could serve as an interim solution while direct API access is being established, or as a permanent approach if direct API onboarding proves difficult.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown -- not published | Unknown |
| **API uptime/reliability** | Unknown -- no published SLA or status page | Unknown |
| **Historical data depth** | Unknown | Unknown |
| **Timezone handling** | Expected ISO 8601 with timezone per DCSA specification (if DCSA TNT implemented) | Estimated (DCSA spec) |
| **Character encoding** | Expected UTF-8 | Estimated |

### Known Issues & Gotchas

- **Documentation opacity**: ZIM's API documentation is entirely behind authentication. This is the single biggest challenge for pre-integration assessment. Unlike carriers like Maersk, Hapag-Lloyd, or CMA CGM that publish at least partial API documentation publicly, ZIM reveals nothing about endpoint structure, parameters, or response shapes without portal login.

- **Hapag-Lloyd acquisition**: The announced acquisition of ZIM by Hapag-Lloyd (signed 2026-02-17, expected to close late 2026) creates uncertainty for long-term API investment. Post-merger, ZIM's APIs may be migrated to, or replaced by, Hapag-Lloyd's API platform (https://api-portal.hlag.com). SSL should factor this transition risk into integration planning.

- **DCSA adoption depth unknown**: While ZIM adopted DCSA T&T standards, the depth of implementation is unclear. Some DCSA members implement only basic event types, while others provide comprehensive event coverage including all equipment, transport, and shipment events. ZIM's specific implementation level cannot be assessed without API access.

- **Azure API Management platform**: ZIM uses Microsoft Azure API Management, which has specific characteristics: subscription keys typically passed as `Ocp-Apim-Subscription-Key` header, standard rate limiting and throttling mechanisms, and developer portal that may require Azure AD authentication.

- **Multiple documentation sites**: Both api.zim.com and docs.zimconnections.com appear to host API documentation, which could indicate either multiple API versions/products or a migration between platforms.

### Recently Deprecated or Changed

- **eZIM platform**: Closed end of December 2025. Booking and Shipping Instruction functionality migrated to myZIM. Any integrations built against eZIM endpoints are now deprecated.

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | Partial -- ZIM has an API portal and is a DCSA member with T&T adoption, so a tracking adapter is likely feasible. However, detailed endpoint documentation is required before implementation can begin. Aggregator-based access (Vizion, project44) is an alternative |
| **Implementation effort** | Unknown until API documentation is accessed. If ZIM's API is DCSA-compliant: Low-Medium (DCSA passthrough + minor deviations). If proprietary: High |
| **DCSA base adapter usable?** | Likely yes -- ZIM adopted DCSA T&T standards, so the base adapter should handle event parsing. Extent of deviations unknown |

### Recommended Approach

**Phase 1 (Immediate): Aggregator Integration**
For fastest time-to-value, integrate ZIM tracking through Vizion (confirmed B/L and booking support for ZIMU) or project44. This provides tracking visibility without needing to navigate ZIM's API onboarding process.

**Phase 2 (After API Access): Direct Integration Assessment**
Register for ZIM's API portal at api.zim.com and obtain API documentation. Once endpoint details are known, assess whether a direct adapter is worthwhile or whether aggregator access is sufficient. Key evaluation criteria: (a) does ZIM's direct API provide data not available through aggregators (cutoffs, booking lifecycle, detailed event types)? (b) is the DCSA TNT implementation standard enough to reuse the base adapter?

**Phase 3 (Post-Acquisition Consideration): Hapag-Lloyd Migration**
Given the pending Hapag-Lloyd acquisition, SSL should monitor the integration timeline. If ZIM's API will be absorbed into Hapag-Lloyd's platform within 12-18 months of SSL's integration, it may be more efficient to use aggregators for ZIM in the interim and invest in the Hapag-Lloyd adapter (already audited) for long-term coverage.

### Recommended Lookup Method

**Bill of Lading (B/L) number** -- consistent with other carrier adapters and confirmed supported on ZIM's web portal and through Vizion. ZIM B/L numbers use the format ZIMU + 8-12 alphanumeric characters.

**Booking reference** as secondary -- supported on web portal and Vizion.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Every 2-4 hours for active shipments (adjust based on rate limits once known). Via aggregator: follow aggregator's recommended polling interval |
| **Incremental filter** | If DCSA TNT: use `eventCreatedDateTime > lastPollTime`. If via aggregator: use aggregator's delta mechanism |
| **Batch tracking** | One call per shipment (standard for DCSA TNT). Via Vizion: supports individual container/B/L tracking |

### Auth Implementation Notes

Specific auth implementation details cannot be provided without API portal access. Based on the Azure API Management platform:

- Expect subscription key-based authentication (`Ocp-Apim-Subscription-Key` header) or potentially OAuth2
- Tokens obtained through registration and may have configurable rate limits
- No token sharing with unapproved third parties (per API Terms)

### Edge Cases to Handle

- **Hapag-Lloyd merger transition**: The adapter should be designed to handle a potential migration to Hapag-Lloyd's API platform. Abstract the carrier-specific layer to make swapping backends straightforward.
- **DCSA compliance depth**: If ZIM's DCSA implementation is partial, the adapter must gracefully handle missing event types (e.g., no transshipment events, no shipment events).
- **Multiple API endpoints**: The existence of both api.zim.com and api.zimconnections.com suggests possible API versioning or product separation. The adapter may need to call multiple base URLs.

### Mapping Complexity

**Unknown until documentation is accessed.** If ZIM implements standard DCSA TNT v2.2, mapping complexity is Low (direct reuse of DCSA base adapter event mapping). If ZIM uses proprietary event codes or non-standard response shapes, complexity could be Medium-High. The safest estimate is Medium given the documentation opacity.

---

## Open Questions

- [ ] **What specific APIs are available on api.zim.com?** -- Need portal access to enumerate API products (tracking, schedules, booking, etc.)
- [ ] **What DCSA TNT version does ZIM implement?** -- v2.2? v3.0? Critical for determining base adapter compatibility
- [ ] **Does ZIM's API support webhooks/event subscriptions?** -- Determines whether push-based tracking is possible
- [ ] **What are the exact endpoint paths, parameters, and response shapes?** -- Required for adapter implementation
- [ ] **What are the specific rate limits?** -- Per-minute and per-day limits, defined during registration
- [ ] **What is the relationship between api.zim.com and api.zimconnections.com?** -- Different API products? Different versions? Migration?
- [ ] **Does ZIM expose cutoff data (ERD, EFC, DCO, VCO, FCO, LCO) via API?** -- Critical for full field coverage
- [ ] **What is the API auth mechanism?** -- Azure subscription key? OAuth2? API key header? Need portal access to confirm
- [ ] **Does SSL have or can it establish a business relationship with ZIM?** -- May be required for API access
- [ ] **What is the timeline for Hapag-Lloyd integration of ZIM's systems?** -- Affects long-term investment decision
- [ ] **Is there a sandbox/test environment?** -- Needed for adapter development

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | https://www.zim.com |
| Developer Portal | https://api.zim.com/ |
| Secondary API Documentation | https://docs.zimconnections.com/ |
| API Terms and Conditions | https://www.zim.com/help/api-terms-and-conditions |
| API Support | https://www.zim.com/contact-us/zim-api-support |
| Web Tracking | https://www.zim.com/tools/track-a-shipment |
| Schedules | https://www.zim.com/schedules |
| US Inland Tracing | https://www.zim.com/tools/us-inland-tracing-status |
| Digital Solutions | https://www.zim.com/digital-solutions |
| myZIM Platform | https://www.zim.com/digital-solutions/myzim-personal-area |
| eCommerce Partners / EDI | https://www.zim.com/tools/ecommerce-partners |
| Vizion ZIM Support | https://docs.vizionapi.com/docs/supported-carriers |
| Vizion ZIM Performance Blog | https://www.vizionapi.com/blog/zim-container-tracking-and-performance-insights-across-global-trade-lanes |
| project44 Ocean Visibility | https://www.project44.com/platform/visibility/ocean/ |
| DCSA T&T Adoption Announcement | https://splash247.com/top-carriers-adopting-dcsa-track-and-trace-standards/ |
| DCSA Members | https://dcsa.org/about-us-our-work-and-what-we-do-dcsa/members/ |
| DCSA OpenAPI Specs (GitHub) | https://github.com/dcsaorg/DCSA-OpenAPI |
| Hapag-Lloyd Acquisition Announcement | https://www.hapag-lloyd.com/en/company/press/releases/2026/02/hapag-lloyd-signs-merger-agreement-with-zim.html |
| ZIM Acquisition Investor Details | https://investors.zim.com/news/news-details/2026/ZIM-to-be-Acquired-by-Hapag-Lloyd-for-35-00-per-Share-in-Cash-at-Aggregate-Cash-Consideration-of-Approximately-4-2-Billion-New-Israeli-Company-New-ZIM-to-Acquire-Portion-of-ZIMs-Business/default.aspx |
| INTTRA eVGM Adoption | https://www.scmr.com/article/zim_is_latest_ocean_carrier_to_opt_for_inttras_evgm_service/news/news/more |
