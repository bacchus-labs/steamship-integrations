# Emirates Shipping Line (ESL) -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing
> **Researched by**: Agent
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | Emirates Shipping Line (commonly "ESL") |
| **SCAC Code** | ESPU (primary); EMIV (used for US/Canada AMS filings per ESL advisory) |
| **Parent Company** | Independent (privately held, UAE-based) |
| **Alliance** | Independent -- not a member of any vessel-sharing alliance |
| **Primary Services** | Container shipping (FCL/LCL), special cargo, dangerous goods, inland/intermodal solutions |
| **Market Position** | Regional specialist -- Intra-Asia, Middle East, Indian Subcontinent, East Africa. Ranked ~49th globally by Alphaliner. ~750,000 TEU annual capacity, 60+ terminal calls weekly |
| **Headquarters** | Jebel Ali Free Zone, Dubai, United Arab Emirates |
| **Website** | https://www.emiratesline.com |

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | No -- no public developer portal exists |
| **Developer portal URL** | N/A |
| **API documentation URL(s)** | N/A -- ESL states they "build APIs to suit business needs" on request, but no public API documentation is published |
| **Documentation quality** | None -- no public API documentation available |
| **OpenAPI/Swagger spec available?** | No |
| **Sandbox/test environment?** | Unknown -- no public sandbox documented |
| **Developer registration** | N/A -- no self-service registration; custom API access requires contacting ESL directly |
| **Developer support channels** | General contact via https://www.emiratesline.com/contact-us/; no developer-specific channels found |
| **Community/third-party libraries** | None found -- no GitHub repos, npm packages, or PyPI packages specific to ESL APIs |
| **API changelog / release notes** | Not published |

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | No -- ESL is not a DCSA member. DCSA members are: MSC, Maersk, CMA CGM, Hapag-Lloyd, ONE, Evergreen, Yang Ming, HMM, ZIM, and PIL |
| **DCSA APIs implemented** | None |
| **DCSA TNT version** | N/A |
| **DCSA Booking version** | N/A |
| **DCSA Schedules version** | N/A |
| **Known DCSA deviations** | N/A |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Yes | ESL's digital portals page confirms "customised electronic data interchange (EDI) solutions"; specific message types not publicly documented |
| **INTTRA integration** | Unknown | No public evidence found |
| **BIC (Bureau International des Containers)** | Unknown | Container prefix codes in use (ESL containers observed) but BIC compliance not documented |
| **UN/LOCODE** | Unknown | Likely used in schedules, but not explicitly documented |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | Unknown -- no public API; custom APIs built on request likely use proprietary auth |
| **Auth documentation** | N/A |
| **Registration process** | Contact ESL directly to request custom API or EDI integration |
| **Registration URL** | https://www.emiratesline.com/contact-us/ |
| **Partner program required?** | Yes -- for any API access (custom build required) |
| **Partner program URL** | N/A (no formal partner program documented) |
| **Credential type** | Unknown |
| **Token refresh supported?** | Unknown |
| **Token lifetime** | Unknown |
| **Access tiers** | Unknown -- custom arrangements per client |
| **IP whitelisting required?** | Unknown |

### Access Requirements Summary for SSL

ESL does not offer a public API or self-service developer portal. All API and EDI integrations are built on request as custom solutions. SSL would need to contact ESL's commercial or IT team directly to negotiate API access. This would likely require a business relationship or partnership agreement. The timeline and scope of any custom API would depend on ESL's internal development capacity. For near-term tracking needs, third-party aggregators (particularly project44) are the most practical path to ESL data.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field must have a row.
> Available via direct API = N/A for all fields (no public API exists)
> Assessed via: E-Sea web portal, mobile app, third-party aggregators

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ❌ | N/A (web portal schedule search at emiratesline.com/schedule-search/) | N/A | N/A | Schedule search available on website and mobile app but no API endpoint published |
| 1.2 | Point-to-Point Route Options | ❌ | N/A (transit time calculator on website) | N/A | N/A | Transit time calculator on website, no API |
| 1.3 | Booking Lifecycle | ❌ | N/A (E-Sea platform at esea.emiratesline.com for manual booking) | N/A | N/A | Booking via E-Sea web portal only; ESL mentions custom "booking request interfaces" built on request |
| 1.4 | Shipping Instructions | ❌ | N/A (E-Sea platform for documentation) | N/A | N/A | Documentation handled through E-Sea portal |
| 1.5 | Rates | ❌ | N/A (carrier charge finder on website) | N/A | N/A | Carrier charge finder tool on website for surcharges; no rate API |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❓ | N/A | N/A | `ECP` | Unknown -- may be communicated via booking confirmation in E-Sea portal |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❓ | N/A | N/A | `EFC` | Unknown |
| 2.3 | Documentation Cutoff | DCO | ❓ | N/A | N/A | `DCO` | Likely communicated in booking confirmation but not via API |
| 2.4 | VGM Cutoff | VCO | ⚠️ | N/A | N/A | `VCO` | ESL offers VGM services via website; cutoff likely in booking confirmation, not API-accessible |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ❓ | N/A | N/A | `FCO` | Unknown -- likely in booking confirmation |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❓ | N/A | N/A | `LCO` | Unknown |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ❓ | N/A | N/A | Inferred from first EquipmentEvent | Unknown -- no API to query |
| 3.2 | Empty Container Gate-Out (Pickup) | ❓ | N/A | N/A | `GTOT` + `EMPTY` | Web tracking may show this; ESL tracking engine returns milestone data via email |
| 3.3 | Full Container Gate-In | ❓ | N/A | N/A | `GTIN` + `LADEN` | Web tracking may show this |
| 3.4 | Container Loaded on Vessel | ⚠️ | N/A | N/A | `LOAD` + `LADEN` | Likely available in web tracking; third-party aggregators (project44, Dockflow) report this milestone |
| 3.5 | Container Discharged at Transshipment | ⚠️ | N/A | N/A | `DISC` + `LADEN` + transshipment | Third-party aggregators report transshipment events for ESL |
| 3.6 | Container Loaded at Transshipment | ⚠️ | N/A | N/A | `LOAD` + `LADEN` + transshipment | Third-party aggregators report transshipment events for ESL |
| 3.7 | Container Discharged at Destination | ⚠️ | N/A | N/A | `DISC` + `LADEN` | Likely available in web tracking and through aggregators |
| 3.8 | Full Container Gate-Out (Delivery) | ❓ | N/A | N/A | `GTOT` + `LADEN` | Unknown from direct ESL sources |
| 3.9 | Empty Container Returned | ❓ | N/A | N/A | `GTIN` + `EMPTY` | Unknown |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ⚠️ | N/A | N/A | `DEPA` + classifier | Available on ESL website schedule search and mobile app; third-party aggregators provide this |
| 4.2 | Estimated Time of Arrival | ETA | ⚠️ | N/A | N/A | `ARRI` + classifier | Available on ESL website and mobile app; aggregators provide this |
| 4.3 | Vessel Arrival at Transshipment | -- | ❓ | N/A | N/A | `ARRI` at intermediate | Unknown from direct sources; possibly via aggregators |
| 4.4 | Vessel Departure from Transshipment | -- | ❓ | N/A | N/A | `DEPA` at intermediate | Unknown from direct sources; possibly via aggregators |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❌ | No webhook/push support documented |
| Event Polling with timestamp filter | ❌ | No polling API available |
| Event Classifier Progression (PLN->EST->ACT) | ❌ | No DCSA event model |
| Retracted Events | ❌ | Not supported |
| Change Remarks | ❌ | Not supported |
| Delay Reason Codes | ❌ | Not supported |

### Coverage Summary

| Category | Fields Available | Fields Unavailable | Fields Unknown | Coverage % |
|----------|-----------------|-------------------|----------------|-----------|
| API Domains (1.x) | 0/5 | 5/5 | 0/5 | 0% |
| Cutoffs (2.x) | 0/6 | 0/6 | 6/6 | 0% |
| Container Milestones (3.x) | 0/9 | 0/9 | 9/9 | 0% |
| Transport Events (4.x) | 0/4 | 0/4 | 4/4 | 0% |
| Change Detection (5.x) | 0/6 | 6/6 | 0/6 | 0% |
| **Total** | **0/30** | **11/30** | **19/30** | **0%** |

> **Note**: 0% coverage reflects the absence of any public API. Via third-party aggregators (project44, Dockflow), partial tracking data (container milestones, ETD/ETA) is accessible. The "Unknown" fields are likely available on ESL's web portal and E-Sea platform but cannot be confirmed without portal access.

---

## Endpoint Reference

ESL does not publish any public API endpoints. All digital services are accessed through:
- **E-Sea platform**: https://esea.emiratesline.com (web portal for booking, documentation, tracking -- requires login)
- **Website tracking**: https://www.emiratesline.com/track/ (email-based tracking -- sends request to ESL Tracking Engine, which returns results via email)
- **Mobile app**: iOS and Android (tracking by B/L, booking, or container number)

### Lookup Methods Summary

| Identifier Type | Supported? | Which Endpoints? | Notes |
|----------------|-----------|-----------------|-------|
| **Bill of Lading (B/L) number** | Yes (web/app) | Web portal, mobile app, email tracking | Not API-accessible |
| **Booking reference** | Yes (web/app) | Web portal, mobile app, email tracking | Not API-accessible |
| **Container number** | Yes (web/app) | Web portal, mobile app, email tracking | Not API-accessible |
| **Carrier booking number** | Unknown | | |
| **Vessel IMO / voyage** | Unknown | | Schedule search on website may use vessel/voyage |

---

## Rate Limits & Quotas

| Detail | Value | Source |
|--------|-------|--------|
| **Global rate limit** | N/A -- no public API | N/A |
| **Per-endpoint limits** | N/A | N/A |
| **Daily/monthly quota** | N/A | N/A |
| **Rate limit response** | N/A | N/A |
| **Rate limit by** | N/A | N/A |
| **Burst allowance** | N/A | N/A |
| **Different tiers** | N/A | N/A |

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

No webhook or push notification support available.

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | https://www.emiratesline.com/track/ |
| **Login required?** | No (for basic tracking); Yes (for E-Sea platform at esea.emiratesline.com) |
| **Data available on portal but NOT in API** | All tracking data -- there is no API. Web portal and E-Sea platform provide schedule search, booking, documentation, cargo tracking, VGM submission |
| **Scraping feasibility** | Difficult -- the tracking page sends an email request to the "ESL Tracking Engine" which generates a response via email rather than displaying results inline; not a standard web scraping target. E-Sea platform (esea.emiratesline.com) is login-gated and likely has anti-bot measures. ToS not assessed |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Yes |
| **EDI message types** | Unknown -- ESL confirms EDI availability but does not publish supported message types. Likely includes standard types (IFTMIN, COPARN, IFTSTA) based on industry norms |
| **EDI connection method** | Unknown -- "customised EDI solutions" developed per client |
| **EDI documentation** | Not public -- contact ESL directly |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Yes | project44 has a dedicated Emirates container tracking page (project44.com/tracking/container/emirates/). Tracking by MBL/BL number and container number confirmed |
| **FourKites** | Unknown | No direct evidence found; FourKites covers 98%+ of ocean freight so ESL may be included |
| **Vizion** | No | ESL is not listed on Vizion's supported carriers page (docs.vizionapi.com/docs/supported-carriers) |
| **INTTRA / E2open** | Unknown | No evidence found |
| **CargoSmart** | Unknown | No evidence found |
| **Dockflow** | Yes | dockflow.com/container-tracking/esl/ -- provides API access to ESL tracking data including milestones, transshipment events, delay alerts. Sources data from carrier feeds, AIS, GPS, satellite |
| **ShipsGo** | Yes | shipsgo.com/ocean/carriers/emirates/container-tracking -- container tracking API with unlimited calls |
| **Portcast** | Yes | portcast.io/carrier-coverage/emirates-shipping-line-container-tracking -- comprehensive coverage across Americas, Africa, Europe, Middle East, Asia-Pacific |

> **Aggregator note**: Since ESL has no public API, third-party aggregators are the only programmatic path to ESL tracking data. project44 and Dockflow provide the most documented coverage. These aggregators likely scrape ESL's web portal or have private data-sharing agreements. The aggregator integration path should be the primary consideration for the SDK adapter.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown | Unknown |
| **API uptime/reliability** | N/A -- no public API | N/A |
| **Historical data depth** | Unknown | Unknown |
| **Timezone handling** | Unknown | Unknown |
| **Character encoding** | Unknown | Unknown |

### Known Issues & Gotchas

- ESL's web tracking is email-based: submitting a tracking request sends an email to the "ESL Tracking Engine" which generates a response email. This is not a real-time web response and is unsuitable for programmatic access.
- SCAC code confusion: ESL uses ESPU as their primary SCAC code, but EMIV for US/Canada AMS filings. Some databases also reference ESGN. The SDK must handle multiple SCAC codes for carrier identification.
- ESL is a relatively small regional carrier (~49th globally). Their digital infrastructure is significantly less mature than the top-10 carriers.
- Custom API integrations are built on request, meaning ESL likely has internal APIs that are not publicly documented. Negotiating direct API access may be possible but would require a business relationship.

### Recently Deprecated or Changed

- No deprecation information available -- ESL does not publish changelogs or API versioning.

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | Partial -- only via third-party aggregator integration (project44, Dockflow); no direct API adapter is feasible without a custom arrangement with ESL |
| **Implementation effort** | Very High (no API) for direct integration; Medium for aggregator passthrough |
| **DCSA base adapter usable?** | No -- ESL is not DCSA-compliant and has no public API; fully custom approach required |

### Recommended Approach

The recommended approach for ESL is an aggregator-mediated adapter rather than a direct carrier integration. project44 is the best-documented aggregator with confirmed ESL coverage and provides tracking by BL and container number. Dockflow is a viable alternative with a documented API and ESL-specific tracking page.

The adapter should implement the standard `CarrierAdapter` interface but delegate all data retrieval to the aggregator's API. The adapter would: (1) accept tracking requests with BL or container number identifiers, (2) translate them to aggregator API calls, (3) normalize the aggregator's response to the canonical DCSA-based data model.

If SSL establishes a direct business relationship with ESL, a custom API or EDI integration could be negotiated. ESL's digital portals page explicitly states they build custom APIs. This would be a longer-term option that could replace or supplement the aggregator path. EDI integration (likely IFTSTA for tracking status) is another possibility if SSL has EDI infrastructure.

### Recommended Lookup Method

**Container number** is the most reliable identifier for ESL tracking via aggregators. BL number is also supported by project44. Booking reference support through aggregators is less certain.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Every 4-6 hours via aggregator API (subject to aggregator rate limits and data freshness) |
| **Incremental filter** | Depends on aggregator API capabilities; project44 and Dockflow may support event-based filtering |
| **Batch tracking** | Depends on aggregator -- project44 supports batch requests; assess per aggregator |

### Auth Implementation Notes

Authentication will be with the aggregator (project44, Dockflow), not with ESL directly. project44 uses OAuth2-based authentication. Dockflow uses API key authentication. The adapter should be configured with aggregator credentials, not ESL credentials.

### Edge Cases to Handle

- SCAC code ambiguity: ESL uses ESPU, EMIV, and possibly ESGN. The adapter should recognize all three.
- Email-based tracking: If aggregator data is unavailable for a particular shipment, there is no fallback API to query directly.
- Regional coverage gaps: ESL primarily serves Intra-Asia, Middle East, Indian Subcontinent, and East Africa. Aggregator coverage may vary by trade lane.
- Data latency through aggregators: Event freshness depends on how quickly the aggregator receives data from ESL, which may introduce additional delay compared to direct API carriers.

### Mapping Complexity

Low to medium if using an aggregator, since aggregators typically normalize data to their own standard models which can then be mapped to the canonical DCSA model. The main complexity is in determining which aggregator milestones map to which DCSA event codes, as ESL does not use DCSA natively. Transshipment event identification may require heuristic logic based on port codes in the route.

---

## Open Questions

- [ ] Does SSL have an existing business relationship with ESL that could facilitate direct API or EDI access?
- [ ] Which aggregator (project44, Dockflow) does SSL already have a relationship with?
- [ ] What specific EDI message types does ESL support? (Requires direct inquiry to ESL)
- [ ] Does the E-Sea platform (esea.emiratesline.com) expose any internal APIs that could be accessed with credentials?
- [ ] What is the data freshness of ESL tracking data through project44 and Dockflow?
- [ ] Is ESL's custom API offering a full REST API or limited to specific data feeds (e.g., schedule feeds)?
- [ ] Does FourKites or CargoSmart cover ESL? (Could not confirm)

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | https://www.emiratesline.com |
| Digital Portals Page | https://www.emiratesline.com/digital-portals/ |
| Web Tracking | https://www.emiratesline.com/track/ |
| Cargo Tracking Info | https://www.emiratesline.com/cargo-tracking/ |
| E-Sea Platform | https://esea.emiratesline.com/ecomonline/Welcome.do |
| Schedule Search | https://www.emiratesline.com/schedule-search/ |
| Mobile App (iOS) | https://apps.apple.com/us/app/esl-mobile-app/id1565711836 |
| US/Canada SCAC Advisory | https://www.emiratesline.com/advisories/advanced-cargo-declration-for-shipments-to-usa-and-canada/ |
| project44 ESL Tracking | https://www.project44.com/tracking/container/emirates/ |
| Dockflow ESL Tracking | https://dockflow.com/container-tracking/esl/ |
| ShipsGo ESL Tracking | https://shipsgo.com/ocean/carriers/emirates/container-tracking |
| Portcast ESL Coverage | https://www.portcast.io/carrier-coverage/emirates-shipping-line-container-tracking |
| Fluent Cargo (ESPU schedules) | https://www.fluentcargo.com/carriers/scac/ESPU |
| Vizion Supported Carriers | https://docs.vizionapi.com/docs/supported-carriers |
| Routescanner ESL | https://www.routescanner.com/partners/ESL |
