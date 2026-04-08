# Crowley Maritime Corporation -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing. Research based on Crowley's public website, C Sight tracking portal, My Crowley customer portal, LogX platform pages, DCSA membership records, third-party aggregator listings (project44, Vizion, INTTRA/E2open, Terminal49), and community resources. No API credentials were obtained or used because Crowley does not offer a public API.
> **Researched by**: Agent (carrier API audit workflow)
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | Crowley Maritime Corporation (commonly "Crowley") |
| **SCAC Code** | CMCU (also CLAM, CWLQ, CPRC, CAMN for different service branches) |
| **Parent Company** | Crowley Holdings Inc. (privately held, family-owned since 1892) |
| **Alliance** | Independent |
| **Primary Services** | Container shipping (FCL, LCL), RoRo, breakbulk, project cargo, vehicle shipping, LNG-powered ConRo vessels |
| **Market Position** | Leading US-flag Jones Act carrier. Dominant in US-Caribbean, US-Central America, and US-Puerto Rico trades. Regional specialist, not a global deep-sea liner. Over $2.5B annual revenue, ~6,300 employees, 160+ vessels, 45,000+ pieces of container equipment |
| **Headquarters** | Jacksonville, Florida, USA |
| **Website** | [https://www.crowley.com](https://www.crowley.com) |

### Crowley Digital Ecosystem

| Entity | Role | URL |
|--------|------|-----|
| **Crowley Website** | Corporate site, route finder, public tracking | [crowley.com](https://www.crowley.com) |
| **C Sight** | Salesforce-based shipment tracking portal (public) | [csight.crowley.com](https://csight.crowley.com/crowley/s/shipment-tracking) |
| **My Crowley** | Customer portal for booking, B/L, tracking, documentation | [mycrowley.com](https://mycrowley.com) |
| **LogX Platform** | Customer logistics portal (newer platform) | [logx-prod.logxplus.com](https://logx-prod.logxplus.com/) |
| **LogX Carrier Portal** | Carrier-facing logistics portal | [logx-carrier-prod.logxplus.com](https://logx-carrier-prod.logxplus.com/) |
| **DFTS** | Defense Freight Transportation Services tracking | [dfts.crowley.com](https://dfts.crowley.com) |

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | **No** |
| **Developer portal URL** | N/A |
| **API documentation URL(s)** | N/A -- no public API documentation exists |
| **Documentation quality** | **None** -- no API documentation available. Customer portal and EDI service pages exist but do not describe REST/SOAP APIs |
| **OpenAPI/Swagger spec available?** | No |
| **Sandbox/test environment?** | No (for API). LogX has a development environment (`logx-development.solutions.logxplus.com`) but it appears to be an internal/customer portal environment, not an API sandbox |
| **Developer registration** | N/A -- no developer registration process exists |
| **Developer support channels** | General customer service only. No developer-specific support. Contact via [crowley.com](https://www.crowley.com) |
| **Community/third-party libraries** | None found -- no GitHub repos, npm packages, or PyPI packages for Crowley API integration |
| **API changelog / release notes** | N/A |

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | **No** -- Crowley is not among the nine DCSA member carriers (MSC, Maersk, CMA CGM, Hapag-Lloyd, ONE, Evergreen, Yang Ming, HMM, ZIM). Source: [DCSA About Us](https://dcsa.org/about-us/) |
| **DCSA APIs implemented** | **None** |
| **DCSA TNT version** | N/A |
| **DCSA Booking version** | N/A |
| **DCSA Schedules version** | N/A |
| **Known DCSA deviations** | N/A |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | **Yes** | Crowley supports EDI for automated information exchange. Specific EDIFACT message types not publicly documented. Tideworks case study references "EDI Porter" deployment. Source: [Crowley Ocean Freight](https://www.crowley.com/logistics/supply-chain/ocean/) |
| **INTTRA integration** | **Yes** | Crowley is listed on INTTRA/E2open's ocean carrier network. Source: [INTTRA Ocean Carrier Network](https://www.inttra.com/ocean-carrier-network/) |
| **BIC (Bureau International des Containers)** | Yes | Container IDs follow BIC ISO 6346 format |
| **UN/LOCODE** | Unknown | Likely used in EDI messages but not confirmed from public documentation |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | N/A -- no public API |
| **Auth documentation** | N/A |
| **Registration process** | N/A for API. My Crowley portal requires existing customer account. C Sight public tracking does not require login |
| **Registration URL** | My Crowley: [mycrowley.com](https://mycrowley.com) |
| **Partner program required?** | N/A for API. EDI integration requires business relationship with Crowley |
| **Partner program URL** | N/A |
| **Credential type** | My Crowley: Username/Password. EDI: implementation-specific credentials |
| **Token refresh supported?** | N/A |
| **Token lifetime** | N/A |
| **Access tiers** | N/A |
| **IP whitelisting required?** | Unknown for EDI |

### Access Requirements Summary for SSL

Crowley does not offer a public REST/SOAP API. To access Crowley data programmatically, SSL has three options:

1. **Third-party aggregator** (recommended) -- Use Vizion (confirmed CMCU support with B/L and booking lookup) or project44 (confirmed Crowley container tracking page). This provides container tracking via a modern REST API without direct Crowley integration. Requires commercial agreement with the aggregator.

2. **INTTRA/E2open platform** -- Crowley is on the INTTRA carrier network, enabling EDI-based booking, shipping instructions, and tracking through INTTRA's platform. Requires INTTRA onboarding and commercial agreement.

3. **EDI integration** -- Establish a direct EDI connection with Crowley. Requires business relationship and EDI infrastructure (SFTP/AS2/VAN). Specific message types and connection procedures not publicly documented -- requires contacting Crowley directly.

Web portal scraping of C Sight is technically possible (public, no login required) but fragile, may violate Terms of Service, and is not recommended for production use.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field must have a row.
> Available via direct API: None (Crowley has no public API)
> Icons reflect practical availability through aggregators and portal:
> ✅ = Available (via aggregator) | ❌ = Not available | ⚠️ = Partial / limited | ❓ = Unknown
>
> **Important context**: Crowley has no public API. The assessments below reflect availability through third-party aggregators (Vizion, project44) and the web portal. There is no direct API integration path.

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ⚠️ | Web: [Route Finder](https://www.crowley.com/logistics/route/) | N/A | N/A | Available on web portal route finder. No API endpoint. Covers US-Caribbean-Central America routes |
| 1.2 | Point-to-Point Route Options | ⚠️ | Web: [Route Finder](https://www.crowley.com/logistics/route/) | N/A | N/A | Route finder provides origin-destination routing. No API endpoint |
| 1.3 | Booking Lifecycle | ⚠️ | My Crowley portal + EDI + INTTRA | N/A | N/A | Booking via My Crowley portal (login required) or INTTRA platform. No REST API |
| 1.4 | Shipping Instructions | ⚠️ | My Crowley portal + EDI + INTTRA | N/A | N/A | SI submission via My Crowley portal, EDI, or INTTRA. No REST API |
| 1.5 | Rates | ❌ | N/A | N/A | N/A | No rate API. Rates via sales contact or freight forwarding platforms |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❓ | Unknown | Unknown | `ECP` | May be available in EDI booking confirmation or My Crowley portal. Not confirmed from public documentation |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❓ | Unknown | Unknown | `EFC` | May be available in EDI booking confirmation or My Crowley portal. Not confirmed |
| 2.3 | Documentation Cutoff | DCO | ❓ | Unknown | Unknown | `DCO` | Likely provided in booking confirmation via My Crowley or EDI. Not confirmed from public sources |
| 2.4 | VGM Cutoff | VCO | ❓ | Unknown | Unknown | `VCO` | Likely provided with booking. SOLAS requirement. Not confirmed from public sources |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ❓ | Unknown | Unknown | `FCO` | Likely provided in booking confirmation. Not confirmed from public sources |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❓ | Unknown | Unknown | `LCO` | Not confirmed from public documentation. Crowley offers LCL service |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ❓ | Unknown | Unknown | Inferred from first EquipmentEvent | Not confirmed. May be visible in My Crowley or EDI |
| 3.2 | Empty Container Gate-Out (Pickup) | ⚠️ | C Sight portal, aggregators | Milestone on tracking portal | `GTOT` + `EMPTY` | Visible on C Sight tracking portal. Available via Vizion/project44 aggregators. No direct API |
| 3.3 | Full Container Gate-In | ⚠️ | C Sight portal, aggregators | Milestone on tracking portal | `GTIN` + `LADEN` | Visible on C Sight portal. Available via aggregators. No direct API |
| 3.4 | Container Loaded on Vessel | ⚠️ | C Sight portal, aggregators | Milestone on tracking portal | `LOAD` + `LADEN` | Visible on C Sight portal. Available via aggregators. No direct API |
| 3.5 | Container Discharged at Transshipment | ⚠️ | C Sight portal, aggregators | Discharge event at intermediate port | `DISC` + `LADEN` + transshipment | Visible on portal for multi-leg shipments. Available via aggregators. No direct API |
| 3.6 | Container Loaded at Transshipment | ⚠️ | C Sight portal, aggregators | Load event at transshipment port | `LOAD` + `LADEN` + transshipment | Visible on portal for multi-leg shipments. Available via aggregators. No direct API |
| 3.7 | Container Discharged at Destination | ⚠️ | C Sight portal, aggregators | Milestone on tracking portal | `DISC` + `LADEN` | Visible on C Sight portal. Available via aggregators. No direct API |
| 3.8 | Full Container Gate-Out (Delivery) | ⚠️ | C Sight portal, aggregators | Milestone on tracking portal | `GTOT` + `LADEN` | Visible on portal. Available via aggregators. No direct API |
| 3.9 | Empty Container Returned | ⚠️ | C Sight portal, aggregators | Milestone on tracking portal | `GTIN` + `EMPTY` | Visible on portal. Available via aggregators. No direct API |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ⚠️ | C Sight portal, aggregators | ETD shown in tracking | `DEPA` + classifier | Available on C Sight portal and via aggregators. No direct API |
| 4.2 | Estimated Time of Arrival | ETA | ⚠️ | C Sight portal, aggregators | ETA shown in tracking | `ARRI` + classifier | Available on C Sight portal and via aggregators. No direct API |
| 4.3 | Vessel Arrival at Transshipment | -- | ⚠️ | C Sight portal, aggregators | Vessel arrival at intermediate port | `ARRI` at intermediate | Available for multi-leg shipments via portal/aggregators. No direct API |
| 4.4 | Vessel Departure from Transshipment | -- | ⚠️ | C Sight portal, aggregators | Vessel departure from intermediate port | `DEPA` at intermediate | Available for multi-leg shipments via portal/aggregators. No direct API |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❌ | No webhook/push API available from Crowley directly. Aggregators (Vizion, project44) provide webhooks |
| Event Polling with timestamp filter | ❌ | No API to poll. Aggregators provide polling capabilities |
| Event Classifier Progression (PLN->EST->ACT) | ❌ | No API-level event classifier progression. Portal may show ETA updates but not in structured PLN->EST->ACT format |
| Retracted Events | ❌ | No API mechanism for retracted events |
| Change Remarks | ❌ | No API mechanism for change remarks |
| Delay Reason Codes | ❌ | No API mechanism for delay reason codes |

### Coverage Summary

| Category | Fields Available | Fields Unavailable | Fields Unknown | Coverage % |
|----------|-----------------|-------------------|----------------|-----------|
| API Domains (1.x) | 0/5 | 1/5 | 0/5 | 0% (4 partial via web/EDI/INTTRA) |
| Cutoffs (2.x) | 0/6 | 0/6 | 0/6 | 0% (6 partial via EDI/INTTRA) |
| Container Milestones (3.x) | 0/9 | 0/9 | 1/9 | 0% (8 partial via portal/aggregators, 1 unknown) |
| Transport Events (4.x) | 0/4 | 0/4 | 0/4 | 0% (4 partial via portal/aggregators) |
| Change Detection (5.x) | 0/6 | 6/6 | 0/6 | 0% |
| **Total** | **0/30** | **7/30** | **7/30** | **0% via direct API (53% partial via portal/aggregators, 23% unknown)** |

> **Coverage note**: Crowley has **zero fields available via a direct REST/SOAP API**. However, 16 of 30 fields (53%) have partial availability through the C Sight tracking portal and third-party aggregators (Vizion, project44). All 6 cutoff fields are unknown -- they are likely provided in booking confirmations via My Crowley or EDI but could not be confirmed from public documentation. All 6 change detection mechanisms are unavailable via direct API but aggregators provide some webhook/polling capability. For SDK integration, the most viable path is through a third-party aggregator.

---

## Endpoint Reference

Crowley has no public REST/SOAP API endpoints. This section is not applicable.

### Lookup Methods Summary

| Identifier Type | Supported? | Which Endpoints? | Notes |
|----------------|-----------|-----------------|-------|
| **Bill of Lading (B/L) number** | Web portal + EDI + aggregators | C Sight, My Crowley, Vizion, project44 | Confirmed as lookup method on C Sight and Vizion |
| **Booking reference** | Web portal + EDI + aggregators | C Sight, My Crowley, Vizion | Confirmed as lookup method. Booking number returned immediately upon submission in My Crowley |
| **Container number** | Web portal + aggregators | C Sight, project44, Terminal49 | Standard BIC format. Primary lookup for aggregator APIs |
| **Carrier booking number** | Web portal + EDI | My Crowley, C Sight | Same as booking reference |
| **Vessel IMO / voyage** | Unknown | Unknown | Not confirmed as a tracking lookup method |

---

## Rate Limits & Quotas

N/A -- Crowley has no public API. No rate limits apply.

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | [https://csight.crowley.com/crowley/s/shipment-tracking](https://csight.crowley.com/crowley/s/shipment-tracking) |
| **Login required?** | No (public tracking). My Crowley portal requires login for advanced features |
| **Data available on portal but NOT in API** | All tracking data is portal-only since there is no API. Includes: milestone events, vessel details, ETD/ETA, container status |
| **Scraping feasibility** | Difficult -- C Sight is built on Salesforce Lightning (confirmed from page source). Salesforce-based portals use dynamic JavaScript rendering and may employ anti-bot measures. ToS review required. Not recommended for production use |

### Additional Web Services

Crowley's website and My Crowley portal provide:
- **Booking** -- online booking submission via My Crowley
- **Route Finder** -- search by origin/destination for FCL, LCL, vehicles, breakbulk
- **Sailing Schedules** -- available via Fluent Cargo at `fluentcargo.com/carriers/scac/CMCU`
- **Shipping Instructions / B/L** -- submit via My Crowley with express release of Bill of Lading
- **Documentation Management** -- access ocean freight documentation via My Crowley
- **Rate Requests** -- via sales contact (no automated rate API)

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | **Yes** |
| **EDI message types** | Specific EDIFACT/ANSI X.12 message types not publicly documented. General EDI capability confirmed for booking and tracking. Source: [Crowley Ocean Freight](https://www.crowley.com/logistics/supply-chain/ocean/) |
| **EDI connection method** | Not publicly documented. Industry standard is SFTP/AS2/VAN. Tideworks "EDI Porter" deployment suggests managed EDI infrastructure |
| **EDI documentation** | Not publicly available. Requires contacting Crowley directly |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | **Yes** | Explicit Crowley container tracking page. Source: [project44 Crowley](https://www.project44.com/tracking/container/crowley/) |
| **FourKites** | **Unknown** | FourKites covers 85+ carriers. Crowley not individually confirmed but likely given US domestic importance |
| **Vizion** | **Yes** | Confirmed supported. Carrier code CMCU. Supports B/L and booking number lookup. Source: [Vizion Supported Carriers](https://docs.vizionapi.com/docs/supported-carriers) |
| **INTTRA / E2open** | **Yes** | Crowley listed on INTTRA's ocean carrier network. Enables EDI-based booking and tracking through INTTRA platform. Source: [INTTRA Carrier Network](https://www.inttra.com/ocean-carrier-network/) |
| **CargoSmart** | **Unknown** | Not confirmed from available sources |
| **Terminal49** | **Yes** | Lists Crowley as "CLAM" in supported shipping lines. Source: [Terminal49 Crowley](https://terminal49.com/shipping-lines/clam-crowley-container-tracking) |
| **Portcast** | **Yes** | Predictive container tracking for Crowley across Americas, Africa, Europe, Middle East, Asia-Pacific. Source: [Portcast Crowley](https://www.portcast.io/carrier-coverage/crowley-liner-services-container-tracking) |
| **ShipsGo** | **Yes** | Offers Crowley tracking API with unlimited API calls. Source: [ShipsGo Crowley](https://shipsgo.com/ocean/carriers/crowley/container-tracking) |

> **Aggregator note**: Since Crowley has no public API, a third-party aggregator is the only practical path to REST API access for Crowley tracking data. Multiple aggregators confirm Crowley support, giving SSL several options. Vizion and project44 are the most robust choices for a production SDK integration. INTTRA/E2open provides EDI-level access (booking + tracking) through their platform, which may be useful if SSL already has an INTTRA relationship.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown -- no published data on event delay | Unknown |
| **API uptime/reliability** | N/A -- no API | N/A |
| **Historical data depth** | Unknown | Unknown |
| **Timezone handling** | Unknown -- web portal likely shows local port times | Estimated |
| **Character encoding** | Unknown | Unknown |

### Known Issues & Gotchas

- **No public API**: The most significant finding. Crowley is a major US domestic carrier that does not offer a public REST/SOAP API for tracking or any other function
- **Not a DCSA member**: As a regional (non-global) carrier, Crowley has not joined DCSA. No industry standard API compliance
- **Multiple SCAC codes**: Crowley uses CMCU as primary SCAC but also CLAM, CWLQ, CPRC, and CAMN for different service branches. Aggregators may use different codes (e.g., Terminal49 uses CLAM)
- **Salesforce-based portal**: C Sight runs on Salesforce Lightning, making scraping difficult due to dynamic JS rendering and potential anti-bot protections
- **Jones Act carrier**: Crowley is a US-flag carrier operating under the Jones Act for domestic maritime trade (US mainland, Puerto Rico, USVI, Hawaii). This is relevant for SSL's customer base
- **Regional focus**: Routes limited to US-Caribbean-Central America. Not a global deep-sea liner -- different customer profile than Maersk/MSC/CMA CGM

### Recently Deprecated or Changed

- No known deprecations (no API to deprecate)
- Crowley launched LNG-powered Avance Class ConRo vessels and new US Northeast-Central America route (Port of Philadelphia to Guatemala/Honduras) -- expanding service footprint

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | **Partial** -- only through a third-party aggregator (Vizion or project44 recommended). No direct API integration is possible |
| **Implementation effort** | **Very High** (no direct API) -- requires aggregator integration (medium effort but adds dependency) or EDI infrastructure (high effort, specialized) |
| **DCSA base adapter usable?** | **No** -- Crowley does not implement DCSA APIs. Fully custom or aggregator-normalized approach required |

### Recommended Approach

The recommended approach for Crowley integration is **aggregator-first**:

**Primary: Aggregator integration via Vizion or project44** -- Both explicitly support Crowley container tracking. Vizion provides REST API access with B/L and booking number lookup (carrier code CMCU). project44 provides container tracking with their broader ocean visibility platform. The SDK adapter would talk to the aggregator's API, not Crowley directly. This provides standardized milestone events, ETD/ETA, and webhook support through the aggregator layer.

**Secondary: INTTRA/E2open integration** -- Crowley is on the INTTRA carrier network, which provides EDI-based booking and tracking. If SSL has an existing INTTRA relationship, this may be a more comprehensive path (booking lifecycle + shipping instructions + tracking) than a tracking-only aggregator.

**Not recommended: Direct EDI or portal scraping** -- Direct EDI with Crowley requires business relationship negotiation and EDI infrastructure. Portal scraping of the Salesforce-based C Sight portal is fragile and likely violates ToS. Neither approach is suitable for an SDK integration.

### Recommended Lookup Method

**Container number** is the recommended primary lookup method when using aggregator APIs, as they normalize on container-level tracking. **Bill of Lading number** is a strong secondary option, confirmed as supported by Vizion for Crowley. Booking reference is also supported by Vizion.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Depends on aggregator. Vizion and project44 both support webhooks (push) which is preferred. For polling, every 4-6 hours is typical for aggregator APIs |
| **Incremental filter** | Aggregator-dependent. Vizion uses webhook-based push notifications for new events. project44 supports event subscriptions |
| **Batch tracking** | Aggregator-dependent. Both Vizion and project44 support subscribing to individual containers/shipments |

### Auth Implementation Notes

For aggregator-based integration (Vizion or project44):
- Standard REST API authentication patterns (API key or OAuth2)
- No Crowley-specific auth required -- all auth is with the aggregator
- See aggregator documentation for specific credential types

For INTTRA integration:
- INTTRA platform credentials
- EDI-style connectivity (not REST/OAuth)

### Edge Cases to Handle

- **Multiple SCAC codes**: Crowley uses CMCU, CLAM, CWLQ, CPRC, CAMN. Aggregator APIs may expect different codes. Vizion uses CMCU. Terminal49 uses CLAM. The adapter should map between these
- **Aggregator data lag**: Data from aggregators may have a delay compared to what's visible on Crowley's C Sight portal. Freshness depends on the aggregator's data pipeline
- **Limited change detection**: Without direct API access, change detection (schedule changes, ETA updates) is limited to what the aggregator provides. No PLN->EST->ACT progression available
- **Regional routing**: Crowley's routes are US-Caribbean-Central America focused. Multi-leg transshipment events are less common than with global carriers but do occur (e.g., new Philadelphia-Central America route)
- **Mixed vessel types**: Crowley operates ConRo, LO/LO, and RoRo vessels. Container tracking applies to containerized cargo; RoRo/vehicle shipments may have different tracking patterns

### Mapping Complexity

**Low complexity for aggregator path** -- the aggregator normalizes Crowley's data into their standard format. Mapping from Vizion's or project44's API to the canonical model is straightforward and follows the same pattern as any other aggregator-served carrier.

**High complexity for EDI path** -- requires EDIFACT parsing, message type mapping, and handling Crowley-specific EDI implementations. Not recommended unless aggregator costs are prohibitive at scale.

---

## Open Questions

- [ ] Does SSL have an existing business relationship with Crowley that would facilitate EDI or INTTRA integration?
- [ ] Does SSL have an existing relationship with Vizion, project44, or INTTRA/E2open?
- [ ] What specific EDIFACT message types does Crowley support? (Requires contacting Crowley EDI team directly)
- [ ] Are cutoff dates (ERD, EFC, DCO, VCO, FCO, LCO) available through aggregators for Crowley shipments?
- [ ] Is Crowley available on FourKites? (Likely but not confirmed)
- [ ] Which SCAC code do aggregators normalize on for Crowley? (CMCU vs CLAM vs others)
- [ ] Is Crowley on CargoSmart's carrier network?
- [ ] What is the data freshness/latency for Crowley events through Vizion and project44?

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | [https://www.crowley.com](https://www.crowley.com) |
| C Sight Tracking Portal | [https://csight.crowley.com/crowley/s/shipment-tracking](https://csight.crowley.com/crowley/s/shipment-tracking) |
| My Crowley Portal | [https://mycrowley.com](https://mycrowley.com) |
| LogX Customer Portal | [https://logx-prod.logxplus.com](https://logx-prod.logxplus.com/) |
| Route Finder | [https://www.crowley.com/logistics/route/](https://www.crowley.com/logistics/route/) |
| Ocean Freight Services | [https://www.crowley.com/logistics/supply-chain/ocean/](https://www.crowley.com/logistics/supply-chain/ocean/) |
| Maritime Technology | [https://www.crowley.com/solutions/maritime/technology/](https://www.crowley.com/solutions/maritime/technology/) |
| DFTS Portal | [https://dfts.crowley.com](https://dfts.crowley.com) |
| Liner Shipping Forms | [https://www.crowley.com/logistics/resources/liner-container-shipping-forms/](https://www.crowley.com/logistics/resources/liner-container-shipping-forms/) |
| Fluent Cargo Sailing Schedules | [https://www.fluentcargo.com/carriers/scac/CMCU](https://www.fluentcargo.com/carriers/scac/CMCU) |
| project44 Crowley Tracking | [https://www.project44.com/tracking/container/crowley/](https://www.project44.com/tracking/container/crowley/) |
| Vizion Supported Carriers | [https://docs.vizionapi.com/docs/supported-carriers](https://docs.vizionapi.com/docs/supported-carriers) |
| INTTRA Carrier Network | [https://www.inttra.com/ocean-carrier-network/](https://www.inttra.com/ocean-carrier-network/) |
| Terminal49 Crowley | [https://terminal49.com/shipping-lines/clam-crowley-container-tracking](https://terminal49.com/shipping-lines/clam-crowley-container-tracking) |
| ShipsGo Crowley | [https://shipsgo.com/ocean/carriers/crowley/container-tracking](https://shipsgo.com/ocean/carriers/crowley/container-tracking) |
| Portcast Crowley | [https://www.portcast.io/carrier-coverage/crowley-liner-services-container-tracking](https://www.portcast.io/carrier-coverage/crowley-liner-services-container-tracking) |
| DCSA Members | [https://dcsa.org/about-us/](https://dcsa.org/about-us/) |
| Crowley Wikipedia | [https://en.wikipedia.org/wiki/Crowley_Maritime](https://en.wikipedia.org/wiki/Crowley_Maritime) |
| Parabola Crowley API | [https://parabola.io/parabolas-apis/parabolas-crowley-maritime-api](https://parabola.io/parabolas-apis/parabolas-crowley-maritime-api) |
