# HMM (Hyundai Merchant Marine) -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing
> **Researched by**: Claude (automated research agent)
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | HMM Co., Ltd. (formerly Hyundai Merchant Marine) |
| **SCAC Code** | HDMU |
| **Parent Company** | HMM (independent, majority-owned by Korea Development Bank) |
| **Alliance** | THE Alliance (with ONE, Hapag-Lloyd, Yang Ming) |
| **Primary Services** | Container shipping |
| **Market Position** | 8th largest container shipping line globally; South Korea's largest carrier |
| **Headquarters** | Seoul, South Korea |
| **Website** | [https://www.hmm21.com](https://www.hmm21.com) |

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | Yes |
| **Developer portal URL** | [https://apiportal.hmm21.com/api](https://apiportal.hmm21.com/api) |
| **API documentation URL(s)** | [https://apiportal.hmm21.com/api](https://apiportal.hmm21.com/api) (Swagger UI per API) |
| **Documentation quality** | Fair -- Swagger specs are available per-API, but portal requires registration with admin approval to view full docs |
| **OpenAPI/Swagger spec available?** | Yes (per-API within the portal; e.g. [TNT Swagger](https://apiportal.hmm21.com/api/apiopenapi/ce5ebc84-e638-4afc-9de9-2c1a7a1d8efd)) |
| **Sandbox/test environment?** | Yes -- portal mentions a "Testbed" for testing APIs before implementation |
| **Developer registration** | Requires approval -- sign up with ID/Password/Email/Company Name, then admin reviews and approves |
| **Developer support channels** | Not publicly documented; likely via e-service contact |
| **Community/third-party libraries** | None found |
| **API changelog / release notes** | Not published |

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | Yes -- founding member (April 2019) |
| **DCSA APIs implemented** | TNT (live), BKG (piloted Nov 2025), EDoc/BL (piloted Nov 2025) |
| **DCSA TNT version** | Estimated ~v2.2 (unverified) -- based on response schema containing shipment/transport/equipment events and transport calls |
| **DCSA Booking version** | Piloted (version not publicly specified) |
| **DCSA Schedules version** | Unknown -- schedule APIs exist but DCSA CS alignment not confirmed |
| **Known DCSA deviations** | TNT endpoint requires both `carrierBookingReference` AND `equipmentReference` simultaneously, which is more restrictive than the DCSA spec that allows querying by either |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Yes | EDI integration services documented; COPARN referenced; VGM via EDI confirmed |
| **INTTRA integration** | Yes | Adopted INTTRA eVGM solution for SOLAS compliance; longstanding INTTRA relationship |
| **BIC (Bureau International des Containers)** | Unknown | |
| **UN/LOCODE** | Yes | Used in transport call location references in TNT API responses |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | API Key (header-based) |
| **Auth documentation** | [https://apiportal.hmm21.com/info](https://apiportal.hmm21.com/info) |
| **Registration process** | 1. Sign up with ID, Password, Email, Company Name. 2. Admin reviews. 3. Approval sent via email. 4. Apply for specific API access. 5. Access token issued. |
| **Registration URL** | [https://apiportal.hmm21.com](https://apiportal.hmm21.com) |
| **Partner program required?** | No -- registration is open but requires admin approval |
| **Partner program URL** | N/A |
| **Credential type** | API Key (issued per service application) |
| **Token refresh supported?** | Unknown -- API Key based, likely static |
| **Token lifetime** | Unknown |
| **Access tiers** | Single tier (after approval) |
| **IP whitelisting required?** | Unknown |

### Access Requirements Summary for SSL

SSL would need to register on the HMM API Portal at apiportal.hmm21.com, providing company details for admin review. Once approved, SSL would apply for access to specific APIs (Track and Trace, Schedule APIs). Access tokens are issued automatically upon service application approval. The process is not fully self-service -- it requires HMM admin approval, which may take business days. No explicit partner agreement or business relationship documentation was found as a requirement, but the admin review step could involve verification. SSL should plan for a registration lead time of several days.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field must have a row.
> Available = Available | Unavailable = Not available | Partial = Partial / limited | Unknown = Unknown

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ✅ | Vessel Schedule (v1), By Calling Port Schedule (v1) | Vessel schedule data | CS (if aligned) | Three schedule APIs available |
| 1.2 | Point-to-Point Route Options | ✅ | Port-to-Port Schedule (v1) | P2P schedule data | CS P2P | Rate limited to 300 calls/hour (Official) |
| 1.3 | Booking Lifecycle | ⚠️ | Not yet on public portal | Piloted via DCSA BKG | BKG v2 (piloted) | Piloted Nov 2025 with Genesis/Samsung SDS/HelloContainer; not yet production |
| 1.4 | Shipping Instructions | ⚠️ | Not yet on public portal | Piloted via DCSA BL | EDoc (piloted) | Piloted Nov 2025; not yet production |
| 1.5 | Rates | ❌ | N/A | N/A | N/A | No rates API found |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❓ | Unknown | Unknown | `ECP` | May be in schedule or booking response; not confirmed without live access |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❓ | Unknown | Unknown | `EFC` | May be in schedule or booking response; not confirmed |
| 2.3 | Documentation Cutoff | DCO | ❓ | Unknown | Unknown | `DCO` | May be in schedule or booking response; not confirmed |
| 2.4 | VGM Cutoff | VCO | ❓ | Unknown | Unknown | `VCO` | VGM is supported via INTTRA eVGM; cutoff in API unknown |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ❓ | Unknown | Unknown | `FCO` | May be in schedule or booking response; not confirmed |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❓ | Unknown | Unknown | `LCO` | May be in schedule or booking response; not confirmed |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ⚠️ | Track and Trace (DCSA) (v1) | Inferred from first equipment event | Inferred from first EquipmentEvent | Requires both carrierBookingReference and equipmentReference |
| 3.2 | Empty Container Gate-Out (Pickup) | ✅ | Track and Trace (DCSA) (v1) | Equipment event: gate-out + empty | `GTOT` + `EMPTY` | Part of DCSA TNT equipment events |
| 3.3 | Full Container Gate-In | ✅ | Track and Trace (DCSA) (v1) | Equipment event: gate-in + laden | `GTIN` + `LADEN` | Part of DCSA TNT equipment events |
| 3.4 | Container Loaded on Vessel | ✅ | Track and Trace (DCSA) (v1) | Equipment event: load + laden | `LOAD` + `LADEN` | Part of DCSA TNT equipment events |
| 3.5 | Container Discharged at Transshipment | ✅ | Track and Trace (DCSA) (v1) | Equipment event: discharge + laden + transshipment | `DISC` + `LADEN` + transshipment | Part of DCSA TNT equipment events |
| 3.6 | Container Loaded at Transshipment | ✅ | Track and Trace (DCSA) (v1) | Equipment event: load + laden + transshipment | `LOAD` + `LADEN` + transshipment | Part of DCSA TNT equipment events |
| 3.7 | Container Discharged at Destination | ✅ | Track and Trace (DCSA) (v1) | Equipment event: discharge + laden | `DISC` + `LADEN` | Part of DCSA TNT equipment events |
| 3.8 | Full Container Gate-Out (Delivery) | ✅ | Track and Trace (DCSA) (v1) | Equipment event: gate-out + laden | `GTOT` + `LADEN` | Part of DCSA TNT equipment events |
| 3.9 | Empty Container Returned | ✅ | Track and Trace (DCSA) (v1) | Equipment event: gate-in + empty | `GTIN` + `EMPTY` | Part of DCSA TNT equipment events |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ✅ | Track and Trace (DCSA) (v1) + Schedule APIs | Transport event: departure | `DEPA` + classifier | Available in both TNT and schedule endpoints |
| 4.2 | Estimated Time of Arrival | ETA | ✅ | Track and Trace (DCSA) (v1) + Schedule APIs + DCSA Arrival Notice | Transport event: arrival | `ARRI` + classifier | Arrival Notice API provides dedicated ETA data |
| 4.3 | Vessel Arrival at Transshipment | -- | ✅ | Track and Trace (DCSA) (v1) | Transport event: arrival at intermediate | `ARRI` at intermediate | Part of transport events in TNT response |
| 4.4 | Vessel Departure from Transshipment | -- | ✅ | Track and Trace (DCSA) (v1) | Transport event: departure from intermediate | `DEPA` at intermediate | Part of transport events in TNT response |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❌ | No webhook/push subscription endpoint found in public API portal |
| Event Polling with timestamp filter | ❓ | TNT endpoint exists but timestamp-based filtering not confirmed in available documentation |
| Event Classifier Progression (PLN->EST->ACT) | ✅ | DCSA TNT response includes transport events with classifier codes |
| Retracted Events | ❓ | Unknown -- not confirmed in available documentation |
| Change Remarks | ❓ | Unknown -- not confirmed in available documentation |
| Delay Reason Codes | ❓ | Unknown -- not confirmed in available documentation |

### Coverage Summary

| Category | Fields Available | Fields Partial | Fields Unavailable | Fields Unknown | Coverage % |
|----------|-----------------|---------------|-------------------|----------------|-----------|
| API Domains (1.x) | 2/5 | 2/5 | 1/5 | 0/5 | 40% |
| Cutoffs (2.x) | 0/6 | 0/6 | 0/6 | 6/6 | 0% |
| Container Milestones (3.x) | 8/9 | 1/9 | 0/9 | 0/9 | 89% |
| Transport Events (4.x) | 4/4 | 0/4 | 0/4 | 0/4 | 100% |
| Change Detection (5.x) | 1/6 | 0/6 | 1/6 | 4/6 | 17% |
| **Total** | **15/30** | **3/30** | **2/30** | **10/30** | **50%** |

> Note: Coverage % counts only fully Available fields. The 2 partial API Domain fields (Booking, Shipping Instructions) were piloted via DCSA in Nov 2025 but are not yet in production on the public portal. Container milestone 3.1 (Container Assigned) is partial because it is inferred rather than explicitly reported. Cutoffs are all Unknown because the API may expose them in schedule or booking responses, but this could not be confirmed without live access. The effective coverage could be significantly higher once registration and live testing confirm cutoff and change detection fields.

---

## Endpoint Reference

### Tracking / Events

| Endpoint | Method | Lookup Params | Pagination | Response Format | Notes |
|----------|--------|--------------|------------|----------------|-------|
| `GET /gateway/dcsaCargoTracking/v1/cargo-tracking-dcsa` | GET | carrierBookingReference (required), equipmentReference (required) | None documented | JSON | DCSA-aligned TNT; both params required simultaneously |

### Schedules

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| Port-to-Port Schedule (v1) | GET | Unknown (requires portal login) | Unknown | JSON | 300 calls/hour limit (Official) |
| Vessel Schedule (v1) | GET | Unknown (requires portal login) | Unknown | JSON | |
| By Calling Port Schedule (v1) | GET | Unknown (requires portal login) | Unknown | JSON | |
| DCSA Arrival Notice API (v1) | GET | Unknown (requires portal login) | Unknown | JSON | DCSA-aligned arrival notice |

### Lookup Methods Summary

| Identifier Type | Supported? | Which Endpoints? | Notes |
|----------------|-----------|-----------------|-------|
| **Bill of Lading (B/L) number** | ❌ | None found | Not a documented lookup parameter; may need to use booking reference instead |
| **Booking reference** | ✅ | Track and Trace (DCSA) | `carrierBookingReference` parameter (required) |
| **Container number** | ✅ | Track and Trace (DCSA) | `equipmentReference` parameter (required); must be used WITH booking reference |
| **Carrier booking number** | ✅ | Track and Trace (DCSA) | Same as carrierBookingReference |
| **Vessel IMO / voyage** | ❓ | Possibly schedule endpoints | Schedule APIs likely accept vessel identifiers but params not confirmed |

---

## Rate Limits & Quotas

| Detail | Value | Source |
|--------|-------|--------|
| **Global rate limit** | Unpublished (varies by API) | Unknown |
| **Per-endpoint limits** | Port-to-Port Schedule: 300 calls/hour | Official (portal listing) |
| **Daily/monthly quota** | Unpublished | Unknown |
| **Rate limit response** | 429 Too Many Requests (Retry-After header advisory) | Official (Swagger spec) |
| **Rate limit by** | Unknown (likely API key) | Estimated |
| **Burst allowance** | Unknown | Unknown |
| **Different tiers** | Single tier after approval | Official (portal) |

---

## Webhook / Push Support

| Detail | Value |
|--------|-------|
| **Webhooks supported?** | No -- no webhook/push subscription endpoint found in public API portal |

> HMM's API portal does not list any event subscription or webhook API. All tracking data must be obtained via polling.

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | [https://www.hmm21.com/e-service/general/trackNTrace/TrackNTrace.do](https://www.hmm21.com/e-service/general/trackNTrace/TrackNTrace.do) |
| **Login required?** | Partially -- some tracking may be available without login but full features require login |
| **Data available on portal but NOT in API** | B/L lookup (portal supports B/L, Booking, Container, P/O number search), booking management, document download |
| **Scraping feasibility** | Difficult -- page returned "Access Denied" during research; likely has anti-bot measures |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Yes |
| **EDI message types** | COPARN confirmed; VGM via EDI (INTTRA eVGM). Full message type list not publicly documented |
| **EDI connection method** | Not publicly documented |
| **EDI documentation** | Contact carrier -- [HMM Digitalization Brochure](https://www.hmm21.com/data_files/company/files/download/HMM%20Digitalization%20Brochure(ENG)%20v1.1.pdf) |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Yes | [project44 HMM Tracking](https://www.project44.com/container-tracking/hmm/) |
| **FourKites** | Yes (reported) | Listed in aggregator comparisons as supporting HMM |
| **Vizion** | Yes | [Vizion HMM Tracking](https://www.vizionapi.com/carrier-tracking/hmm) |
| **INTTRA / E2open** | Yes | [Longstanding relationship; eVGM adoption](https://www.inttra.com/newsroom/press-releases/hmm-press-release/) |
| **CargoSmart** | Yes (reported) | Listed in aggregator comparisons |
| **Other**: Portcast | Yes | [Portcast HMM Tracking](https://www.portcast.io/carrier-coverage/hyundai-merchant-marine-hmm-container-tracking) |
| **Other**: Terminal49 | Yes | [Terminal49 HMM](https://terminal49.com/shipping-lines/hdmu-hyundai-merchant-marine-container-tracking) |
| **Other**: Dockflow | Yes | [Dockflow HMM](https://dockflow.com/container-tracking/hmm/) |

> **Aggregator note**: HMM is widely supported across all major aggregators. Given that HMM's direct API requires both booking reference AND container number simultaneously (no B/L lookup), aggregators like Vizion or project44 may provide more flexible lookup options and broader data coverage. This could influence whether SSL integrates directly or through an aggregator.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown | Unknown |
| **API uptime/reliability** | Unknown | Unknown |
| **Historical data depth** | Unknown | Unknown |
| **Timezone handling** | Unknown (likely UTC based on DCSA alignment) | Estimated |
| **Character encoding** | Unknown | Unknown |

### Known Issues & Gotchas

- TNT endpoint requires BOTH `carrierBookingReference` AND `equipmentReference` -- you cannot query by just one. This is more restrictive than typical DCSA implementations and means you must know the container number upfront.
- No B/L number lookup is available via the API. The web portal supports B/L lookup, but the API does not.
- Admin approval for API registration may introduce delays of several business days.
- Schedule API parameters are not publicly documented without portal login -- specific request/response formats need to be confirmed after registration.
- Portal pages at hmm21.com/company/digital/ returned "Access Denied" during research, suggesting some documentation is restricted.

### Recently Deprecated or Changed

- HMM completed DCSA Booking and Bill of Lading pilots in November 2025 -- these APIs may appear on the portal in the near future, but are not yet listed as production endpoints.

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | Yes -- for tracking and schedules. Booking/SI not yet available. |
| **Implementation effort** | Medium (DCSA-aligned TNT + proprietary schedule endpoints + restrictive lookup requirements) |
| **DCSA base adapter usable?** | Yes with overrides -- TNT is DCSA-aligned but requires both booking ref and container number simultaneously |

### Recommended Approach

The primary integration path is through HMM's DCSA-aligned Track and Trace API for container milestones and transport events, supplemented by the schedule APIs for vessel/port schedule data. The adapter should extend the DCSA base adapter but override the query construction to always supply both `carrierBookingReference` and `equipmentReference`.

Because HMM does not support B/L lookup via the API, the adapter will need to either: (a) require upstream callers to provide both booking reference and container number, or (b) maintain a mapping from B/L to booking reference + container number, potentially populated from the web portal or a third-party aggregator.

If B/L lookup is a hard requirement, SSL should consider integrating through an aggregator (Vizion or project44) for tracking, and using HMM's direct API only for schedule data where aggregators may not provide equivalent coverage.

### Recommended Lookup Method

Carrier booking reference + container number (both required). This is the only lookup method supported by HMM's TNT API. B/L-based lookup is not available through the direct API.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Every 2-4 hours -- rate limits are partially published (300/hr for schedules), TNT limits unknown |
| **Incremental filter** | Unknown whether timestamp filtering is supported; may require full re-fetch per shipment |
| **Batch tracking** | One call per booking+container combination; no batch endpoint documented |

### Auth Implementation Notes

Authentication uses a static API Key passed in the `x-Gateway-APIKey` header. No OAuth flow, no token refresh needed. The API key is issued during the service application process on the portal. Implementation is straightforward -- store the key and include it in all requests.

### Edge Cases to Handle

- Both `carrierBookingReference` and `equipmentReference` are required -- adapter must validate both are provided before making API calls
- No B/L lookup means the adapter cannot serve users who only have a B/L number
- Schedule API parameters are unknown -- adapter should gracefully handle discovery of these after portal registration
- 429 responses should be handled with Retry-After header parsing
- Admin approval for API access may fail -- adapter should clearly surface credential/access issues

### Mapping Complexity

Low to Medium. The TNT response follows DCSA structure with shipment events, transport events, equipment events, and transport calls. Standard DCSA event code mapping applies. The main complexity is in the restrictive query requirements (dual-parameter lookup) and the unknown coverage of cutoff data and change detection fields.

---

## Open Questions

- [ ] Does the TNT API support querying by B/L number (not documented but may be possible)?
- [ ] What are the specific parameters for the schedule APIs (Port-to-Port, Vessel, By Calling Port)?
- [ ] Does the TNT API support timestamp-based event filtering for incremental polling?
- [ ] Are cutoff times (ERD, EFC, DCO, VCO, FCO, LCO) included in schedule or booking responses?
- [ ] What is the global rate limit for the TNT endpoint?
- [ ] Does HMM plan to add the Booking and BL APIs to the public portal (following the Nov 2025 pilots)?
- [ ] Does SSL have an existing business relationship with HMM that could expedite API registration?
- [ ] Are retracted events and change remarks supported in HMM's TNT implementation?

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | [https://www.hmm21.com](https://www.hmm21.com) |
| Developer Portal | [https://apiportal.hmm21.com/api](https://apiportal.hmm21.com/api) |
| API Documentation | [https://apiportal.hmm21.com/api](https://apiportal.hmm21.com/api) |
| OpenAPI/Swagger Spec (TNT) | [https://apiportal.hmm21.com/api/apiopenapi/ce5ebc84-e638-4afc-9de9-2c1a7a1d8efd](https://apiportal.hmm21.com/api/apiopenapi/ce5ebc84-e638-4afc-9de9-2c1a7a1d8efd) |
| Portal Registration Info | [https://apiportal.hmm21.com/info](https://apiportal.hmm21.com/info) |
| Web Tracking Portal | [https://www.hmm21.com/e-service/general/trackNTrace/TrackNTrace.do](https://www.hmm21.com/e-service/general/trackNTrace/TrackNTrace.do) |
| Schedule Portal | [https://www.hmm21.com/e-service/general/schedule/ScheduleMain.do](https://www.hmm21.com/e-service/general/schedule/ScheduleMain.do) |
| DCSA Membership | [https://dcsa.org/about-us/members](https://dcsa.org/about-us/members) |
| DCSA Pilot Announcement | [https://dcsa.org/newsroom/hmm-leads-three-industry-pilots](https://dcsa.org/newsroom/hmm-leads-three-industry-pilots) |
| INTTRA eVGM Adoption | [https://www.inttra.com/newsroom/press-releases/hmm-press-release/](https://www.inttra.com/newsroom/press-releases/hmm-press-release/) |
| HMM Digitalization Brochure | [https://www.hmm21.com/data_files/company/files/download/HMM%20Digitalization%20Brochure(ENG)%20v1.1.pdf](https://www.hmm21.com/data_files/company/files/download/HMM%20Digitalization%20Brochure(ENG)%20v1.1.pdf) |
| project44 HMM Tracking | [https://www.project44.com/container-tracking/hmm/](https://www.project44.com/container-tracking/hmm/) |
| Vizion HMM Tracking | [https://www.vizionapi.com/carrier-tracking/hmm](https://www.vizionapi.com/carrier-tracking/hmm) |
