# Bahri (National Shipping Company of Saudi Arabia) -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing. Research based on Bahri's public website (bahri.sa), Bahri Logistics portal (bahrilogistics.sa), DCSA membership records, INTTRA carrier network listing, Vizion supported carriers documentation, ShipsGo carrier pages, third-party tracking aggregator listings, and community resources. No API credentials were obtained or used because Bahri does not offer a public API.
> **Researched by**: Agent (carrier API audit workflow)
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | Bahri (National Shipping Company of Saudi Arabia / NSCSA) |
| **SCAC Code** | NSAU |
| **Parent Company** | Bahri (publicly listed on Saudi Exchange as 4030; PIF holds 22.55%, Saudi Aramco Development Company holds 20%, remainder public float) |
| **Alliance** | Independent (Saudi Arabia) |
| **Primary Services** | Multipurpose/Con-Ro (containerized cargo, RoRo, breakbulk, project cargo, heavy-lift). Also operates VLCCs (crude oil), chemical tankers, and dry bulk carriers through other business units |
| **Market Position** | National shipping carrier of Saudi Arabia. Largest VLCC and chemical tanker operator in the Middle East. Niche liner service operator with 6-7 multipurpose Con-Ro vessels on fixed trade routes (not a major container-only carrier) |
| **Headquarters** | Riyadh, Saudi Arabia |
| **Website** | [https://www.bahri.sa](https://www.bahri.sa) |

### Bahri Business Units

| Unit | Focus |
|------|-------|
| **Bahri Oil** | VLCC crude oil transportation (50 VLCCs) |
| **Bahri Chemicals** | Chemical/product tanker fleet (31 tankers) |
| **Bahri Logistics** | Liner service -- Con-Ro multipurpose vessels (6-7 vessels, ~26,000 DWT each) |
| **Bahri Dry Bulk** | Dry bulk carrier fleet (13 vessels) |
| **Bahri Ship Management** | Technical ship management |
| **Bahri Marine** | Marine services |

> **Note**: Bahri Logistics is the relevant business unit for this audit. It operates the liner service with multipurpose Con-Ro vessels that carry containers, rolling stock, project cargo, and breakbulk. This is a niche service compared to major container carriers -- Bahri is primarily a tanker company with a liner logistics arm.

### Trade Routes

Bahri Logistics operates two main liner services:

1. **US Trade**: Mexico, US Gulf (Houston, Pensacola), US East Coast (Baltimore, Wilmington) to Middle East (Dammam, Jeddah, Jebel Ali, Kuwait, Bahrain) and Indian subcontinent (Mumbai, Mundra, Ennore)
2. **Europe Trade**: North-West Europe (Genova, Livorno, Iskenderun, Mersin) to Middle East and Indian subcontinent

Port calls include: Dammam, Jeddah, Jebel Ali (UAE), Kuwait, Bahrain, Oman, Mumbai, Mundra, Ennore (India), Houston, Baltimore, Pensacola, Wilmington (US), Genova, Livorno (Italy), Iskenderun, Mersin (Turkey), and various ports in East Africa (Djibouti, Kenya, Tanzania, South Africa) and Egypt/Sudan.

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | **No** |
| **Developer portal URL** | N/A |
| **API documentation URL(s)** | N/A -- no public API documentation exists |
| **Documentation quality** | **None** -- no API documentation available. Web portal and logistics pages exist but do not describe REST/SOAP APIs |
| **OpenAPI/Swagger spec available?** | No |
| **Sandbox/test environment?** | No |
| **Developer registration** | N/A -- no developer registration process exists |
| **Developer support channels** | General customer service only (info@bahri.sa, +966-11-4785454). No developer-specific support |
| **Community/third-party libraries** | None found -- no GitHub repos, npm packages, or PyPI packages for Bahri API integration |
| **API changelog / release notes** | N/A |

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | **No** -- Bahri is not among the nine DCSA member carriers (MSC, Maersk, CMA CGM, Hapag-Lloyd, ONE, Evergreen, Yang Ming, HMM, ZIM). Bahri is primarily a tanker operator with a niche liner service, not a major container-only carrier |
| **DCSA APIs implemented** | **None** |
| **DCSA TNT version** | N/A |
| **DCSA Booking version** | N/A |
| **DCSA Schedules version** | N/A |
| **Known DCSA deviations** | N/A |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Unknown | No public documentation of EDI support found. Given the carrier's size and niche focus, EDI support may be limited or handled through agents |
| **INTTRA integration** | **No** | Bahri is NOT listed on INTTRA/E2open's ocean carrier network. Confirmed absent from their carrier list. Source: [INTTRA Ocean Carrier Network](https://www.inttra.com/ocean-carrier-network/) |
| **BIC (Bureau International des Containers)** | Yes | Container IDs follow BIC ISO 6346 format (NSAU prefix) |
| **UN/LOCODE** | Unknown | Likely used in operational systems but not confirmed from public documentation |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | N/A -- no public API |
| **Auth documentation** | N/A |
| **Registration process** | N/A for API. Bahri Logistics web portal (bahrilogistics.sa) requires customer account for cargo tracking. Registration available on the portal |
| **Registration URL** | Web portal: [bahrilogistics.sa](https://bahrilogistics.sa/) and [bahri.sa cargo tracking](https://www.bahri.sa/en/logistic-services/cargo-tracking/) |
| **Partner program required?** | N/A for API. Web portal access requires customer registration |
| **Partner program URL** | N/A |
| **Credential type** | Web portal: Username/Password |
| **Token refresh supported?** | N/A |
| **Token lifetime** | N/A |
| **Access tiers** | N/A |
| **IP whitelisting required?** | Unknown |

### Access Requirements Summary for SSL

Bahri does not offer a public REST/SOAP API. To access Bahri data programmatically, SSL has limited options:

1. **Third-party aggregator** -- ShipsGo explicitly supports Bahri container tracking through their API (confirmed on their carrier tracking page). ShipsGo provides a Container Tracking API with unlimited calls. This is the most practical REST API path. Vizion does NOT currently support Bahri (confirmed absent from their supported carriers list).

2. **Web portal scraping** -- Bahri's cargo tracking page at bahri.sa requires login and allows search by vessel, port, or House B/L number. The Bahri Logistics portal (bahrilogistics.sa) is a JavaScript-heavy application. Both require authentication, making scraping more complex. Not recommended for production use.

3. **Direct contact with Bahri** -- Given Bahri's niche market position and relatively small liner operation, SSL could explore a direct partnership for data exchange. This would likely be a manual/semi-automated arrangement rather than a standard API.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field must have a row.
> Available via API: ✅ | Not available: ❌ | Partial / limited: ⚠️ | Unknown: ❓
>
> **Important context**: Bahri has no public API. The assessments below reflect availability through the web portal only. Fields marked with ⚠️ are visible on the web portal but cannot be accessed via a REST API.

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ⚠️ | Web: [Master Schedule](https://www.bahri.sa/en/logistic-services/master-schedule/), [Voyage Schedules](https://www.bahri.sa/en/logistic-services/voyage-schedules/) | N/A | N/A | Available on web portal. No API endpoint. Small fleet (6-7 vessels) with fixed liner schedules |
| 1.2 | Point-to-Point Route Options | ⚠️ | Web: [Service Line](https://www.bahri.sa/en/logistic-services/service-line/) | N/A | N/A | Fixed routes (US trade, Europe trade) available on website. No API endpoint |
| 1.3 | Booking Lifecycle | ❌ | N/A | N/A | N/A | No API or known EDI for booking. Booking handled through agents and Bahri Logistics portal |
| 1.4 | Shipping Instructions | ❌ | N/A | N/A | N/A | No API for shipping instructions. Handled through agents and portal |
| 1.5 | Rates | ⚠️ | Web: Quote request form on portal | N/A | N/A | Rate quotes available through web portal and direct contact. No API |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❓ | Unknown | Unknown | `ECP` | No public documentation. May be communicated through agents |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❓ | Unknown | Unknown | `EFC` | No public documentation |
| 2.3 | Documentation Cutoff | DCO | ❓ | Unknown | Unknown | `DCO` | Likely communicated through booking confirmation/agents but not available via API |
| 2.4 | VGM Cutoff | VCO | ❓ | Unknown | Unknown | `VCO` | SOLAS requirement applies but cutoff availability unknown |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ❓ | Unknown | Unknown | `FCO` | Likely communicated by agents for confirmed bookings |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❓ | Unknown | Unknown | `LCO` | Bahri primarily handles FCL, project cargo, and RoRo. LCL relevance uncertain |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ❓ | Unknown | Unknown | Inferred from first EquipmentEvent | Not confirmed from public documentation |
| 3.2 | Empty Container Gate-Out (Pickup) | ❓ | Unknown | Unknown | `GTOT` + `EMPTY` | May be available via web portal tracking (login required). Bahri's Con-Ro operation may have different milestone patterns than pure container carriers |
| 3.3 | Full Container Gate-In | ❓ | Unknown | Unknown | `GTIN` + `LADEN` | May be available via web portal tracking (login required) |
| 3.4 | Container Loaded on Vessel | ⚠️ | Web: Cargo tracking (login required) | Unknown | `LOAD` + `LADEN` | Load events likely visible on web portal. Third-party tracking sites (ShipsGo, SeaRates, expresstracking.org) can provide this |
| 3.5 | Container Discharged at Transshipment | ❓ | Unknown | Unknown | `DISC` + `LADEN` + transshipment | Bahri operates mostly direct services with limited transshipment. Availability unknown |
| 3.6 | Container Loaded at Transshipment | ❓ | Unknown | Unknown | `LOAD` + `LADEN` + transshipment | Same as 3.5 -- limited transshipment in Bahri's liner network |
| 3.7 | Container Discharged at Destination | ⚠️ | Web: Cargo tracking (login required) | Unknown | `DISC` + `LADEN` | Discharge events likely visible on web portal |
| 3.8 | Full Container Gate-Out (Delivery) | ❓ | Unknown | Unknown | `GTOT` + `LADEN` | May be visible on web portal |
| 3.9 | Empty Container Returned | ❓ | Unknown | Unknown | `GTIN` + `EMPTY` | Unknown availability |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ⚠️ | Web: [Voyage Schedules](https://www.bahri.sa/en/logistic-services/voyage-schedules/), [Vessel Tracking](https://www.bahri.sa/en/logistic-services/vessel-tracking/) | N/A | `DEPA` + classifier | Available on web portal and via third-party tracking (ShipsGo). No API |
| 4.2 | Estimated Time of Arrival | ETA | ⚠️ | Web: Voyage Schedules, Vessel Tracking | N/A | `ARRI` + classifier | Available on web portal and via third-party tracking. No API |
| 4.3 | Vessel Arrival at Transshipment | -- | ❓ | Unknown | Unknown | `ARRI` at intermediate | Bahri's liner service is mostly direct. Transshipment visibility unknown |
| 4.4 | Vessel Departure from Transshipment | -- | ❓ | Unknown | Unknown | `DEPA` at intermediate | Same as 4.3 |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❌ | No webhook/push API available |
| Event Polling with timestamp filter | ❌ | No API to poll |
| Event Classifier Progression (PLN->EST->ACT) | ❌ | No API-level event classifier progression |
| Retracted Events | ❌ | No API mechanism for retracted events |
| Change Remarks | ❌ | No API mechanism for change remarks |
| Delay Reason Codes | ❌ | No API mechanism for delay reason codes |

### Coverage Summary

| Category | Fields Available | Fields Unavailable | Fields Unknown | Coverage % |
|----------|-----------------|-------------------|----------------|-----------|
| API Domains (1.x) | 0/5 | 2/5 | 0/5 | 0% (3 partial via web portal) |
| Cutoffs (2.x) | 0/6 | 0/6 | 6/6 | 0% (all unknown) |
| Container Milestones (3.x) | 0/9 | 0/9 | 7/9 | 0% (2 partial via web portal, 7 unknown) |
| Transport Events (4.x) | 0/4 | 0/4 | 2/4 | 0% (2 partial via web portal, 2 unknown) |
| Change Detection (5.x) | 0/6 | 6/6 | 0/6 | 0% |
| **Total** | **0/30** | **8/30** | **15/30** | **0% via API (7 partial via web, 15 unknown, 8 unavailable)** |

> **Coverage note**: Bahri has **zero fields available via a REST/SOAP API**. Only 7 of 30 fields (23%) have partial availability through the web portal. 15 fields (50%) have unknown availability because the web portal requires login and detailed milestone tracking has not been confirmed. All 6 change detection mechanisms are unavailable. For SDK integration, the only confirmed REST API path is through ShipsGo as an aggregator. Bahri's niche market position (multipurpose Con-Ro liner, not a pure container carrier) means the tracking data model may differ from standard container carriers.

---

## Endpoint Reference

Bahri has no public REST/SOAP API endpoints. This section is not applicable.

### Lookup Methods Summary

| Identifier Type | Supported? | Which Endpoints? | Notes |
|----------------|-----------|-----------------|-------|
| **Bill of Lading (B/L) number** | Web portal only | Cargo tracking page | House B/L number lookup available on bahri.sa portal (requires login) |
| **Booking reference** | Web portal only | Cargo tracking page | Available through portal |
| **Container number** | Web portal + ShipsGo | Cargo tracking page, ShipsGo API | Format: NSAU + 7 digits. ShipsGo provides API access for container tracking |
| **Carrier booking number** | Web portal only | Cargo tracking page | Same as booking reference |
| **Vessel IMO / voyage** | Web portal only | Vessel tracking, voyage schedules | Available on bahri.sa |

---

## Rate Limits & Quotas

N/A -- Bahri has no public API. No rate limits apply.

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | [https://www.bahri.sa/en/logistic-services/cargo-tracking/](https://www.bahri.sa/en/logistic-services/cargo-tracking/) |
| **Login required?** | **Yes** -- login required to view and track shipments. Registration available on the portal |
| **Data available on portal but NOT in API** | All tracking data is portal-only since there is no API. Includes: cargo tracking by vessel/port/HBL, vessel tracking with daily positions, master schedule, voyage schedules, container specifications |
| **Scraping feasibility** | **Difficult** -- portal requires authentication (login). Bahri Logistics portal (bahrilogistics.sa) is a JavaScript-heavy application (Dojo Toolkit). Anti-bot measures unknown. Not recommended for production use |

### Additional Web Services

Bahri's website provides:
- **Vessel Tracking** -- daily vessel position tracking
- **Master Schedule** -- vessel rotation schedules
- **Voyage Schedules** -- per-voyage port call schedules
- **Service Line** -- fixed trade route information
- **Container Specifications** -- container type and dimension details
- **Quote Requests** -- rate inquiry through web form

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Unknown |
| **EDI message types** | Unknown -- no public documentation of EDI support found |
| **EDI connection method** | Unknown |
| **EDI documentation** | N/A |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Unknown | project44 claims 98%+ ocean freight coverage, but Bahri is a niche carrier. Not individually confirmed |
| **FourKites** | Unknown | Not individually confirmed for Bahri |
| **Vizion** | **No** | Bahri/NSAU is NOT listed on Vizion's supported carriers page. Confirmed absent. Source: [Vizion Supported Carriers](https://docs.vizionapi.com/docs/supported-carriers) |
| **INTTRA / E2open** | **No** | Bahri is NOT listed on INTTRA's ocean carrier network. Confirmed absent. Source: [INTTRA Ocean Carrier Network](https://www.inttra.com/ocean-carrier-network/) |
| **CargoSmart** | Unknown | Not individually confirmed for Bahri |
| **ShipsGo** | **Yes** | ShipsGo explicitly supports Bahri container tracking through their API. Provides container tracking by B/L, booking, or container number with unlimited API calls. Source: [ShipsGo Bahri Tracking](https://shipsgo.com/ocean/carriers/bahri/container-tracking) |
| **SeaRates** | **Yes** | SeaRates provides Bahri container tracking. Source: [SeaRates Bahri](https://www.searates.com/sealine/bahri) |
| **Fluent Cargo** | **Yes** | Lists Bahri sailing schedules under SCAC NSAU. Source: [Fluent Cargo Bahri](https://www.fluentcargo.com/carriers/scac/NSAU) |

> **Aggregator note**: Bahri is not supported by either Vizion or INTTRA, the two most commonly used aggregators for direct carrier integration. ShipsGo is the only confirmed aggregator with explicit Bahri container tracking API support. SeaRates and Fluent Cargo provide tracking/schedule data but their API availability and suitability for SDK integration need further evaluation.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown -- no published data on event delay | Unknown |
| **API uptime/reliability** | N/A -- no API | N/A |
| **Historical data depth** | Unknown | Unknown |
| **Timezone handling** | Unknown -- web portal likely shows local port times given Middle East/India focus | Estimated |
| **Character encoding** | Unknown | Unknown |

### Known Issues & Gotchas

- **No public API**: Bahri does not offer a public REST/SOAP API for any function (tracking, booking, schedules, or rates). This is the most significant limitation
- **Not a DCSA member**: Bahri is primarily a tanker company with a niche liner service. DCSA membership is limited to nine major container carriers, and Bahri's liner operation is too small to warrant DCSA adoption
- **Not on INTTRA or Vizion**: The two most common integration platforms for ocean carriers do not support Bahri, limiting aggregator options
- **Multipurpose/Con-Ro operation**: Bahri's liner vessels carry a mix of containers, RoRo cargo, breakbulk, and project cargo. The tracking data model may differ from pure container carriers -- milestone patterns for RoRo and project cargo differ from standard container tracking
- **Login-gated portal**: All web tracking requires authentication, making even web portal data harder to access programmatically
- **Small fleet**: Only 6-7 multipurpose vessels in the liner service. Small enough that schedule changes may be communicated through agents rather than automated systems
- **Saudi Arabia focus**: Bahri's primary role is as Saudi Arabia's national carrier for crude oil and chemical transport. The liner service is a secondary business line focused on Saudi import/export trade routes

### Recently Deprecated or Changed

- No known deprecations (no API to deprecate)
- No known recent digital platform changes from public sources

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | **Partial** -- only through ShipsGo as a third-party aggregator. No direct API integration is possible |
| **Implementation effort** | **Very High** (no direct API) -- requires aggregator integration via ShipsGo (medium effort but adds dependency and may have limited data depth) |
| **DCSA base adapter usable?** | **No** -- Bahri does not implement DCSA APIs and is not a DCSA member |

### Recommended Approach

The recommended approach for Bahri integration is a **single-tier strategy via ShipsGo**:

**Primary: Aggregator integration via ShipsGo** -- ShipsGo is the only confirmed aggregator with explicit Bahri container tracking API support. Their API provides container tracking by B/L, booking, or container number. The SDK adapter would talk to ShipsGo's API, not Bahri directly. ShipsGo claims unlimited API calls, which is favorable for polling-based tracking.

However, SSL should evaluate whether Bahri integration is worth the effort given Bahri's niche market position. Bahri carries primarily Saudi import/export cargo (crude oil equipment, industrial machinery, vehicles, project cargo) on two fixed trade routes. Unless SSL's client base includes Saudi-focused importers/exporters, Bahri may be a low-priority carrier.

If Bahri integration is required, an alternative is to **defer integration** and monitor whether Bahri develops digital capabilities as part of Saudi Arabia's Vision 2030 logistics modernization initiatives. The Saudi government has been investing heavily in logistics infrastructure and digitalization.

### Recommended Lookup Method

**Container number** (NSAU prefix) is the recommended primary lookup method when using ShipsGo, as aggregator APIs typically normalize on container-level tracking. B/L number and booking reference are secondary options supported by ShipsGo.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Every 6-12 hours -- Bahri's small fleet and fixed schedules mean less frequent updates than major container carriers. ShipsGo's unlimited API calls make frequent polling feasible if needed |
| **Incremental filter** | ShipsGo-dependent. Check ShipsGo API documentation for incremental/delta query support |
| **Batch tracking** | ShipsGo-dependent. Likely one container per API call |

### Auth Implementation Notes

For ShipsGo-based integration:
- ShipsGo uses API key authentication
- Standard REST API patterns apply
- No Bahri-specific auth required -- all auth is with ShipsGo
- ShipsGo API docs at [api.shipsgo.com/docs/v2/](https://api.shipsgo.com/docs/v2/)

### Edge Cases to Handle

- **Multipurpose cargo types**: Bahri vessels carry containers alongside RoRo and breakbulk cargo. Container tracking milestones may differ from pure container vessel operations
- **Limited transshipment**: Bahri operates mostly direct liner services. Transshipment events (3.5, 3.6, 4.3, 4.4) are unlikely to be relevant for most Bahri shipments
- **Aggregator data lag**: Data from ShipsGo may have a delay compared to what Bahri shows on their own portal
- **Container number prefix**: NSAU format. Ensure the SDK correctly handles this less-common prefix
- **Small fleet vessel identification**: Only 6-7 vessels (Bahri Abha, Bahri Jazan, Bahri Jeddah, Bahri Yanbu, etc.). Vessel identification is straightforward

### Mapping Complexity

**Low complexity for ShipsGo path** -- ShipsGo normalizes tracking data into their standard format. Mapping from ShipsGo's API to the canonical data model should be straightforward, though the available milestone granularity may be less than what DCSA-compliant carriers provide.

**High uncertainty on data depth** -- Given Bahri's niche nature, ShipsGo may only provide basic milestone data (loaded, departed, arrived, discharged) without the full DCSA event spectrum. Cutoff data is unlikely to be available through any aggregator.

---

## Open Questions

- [ ] Does SSL have any clients that ship on Bahri routes (US/Europe to Middle East/India)?
- [ ] Is Bahri a priority carrier for SSL, or can integration be deferred?
- [ ] Does ShipsGo provide sufficient milestone granularity for Bahri shipments?
- [ ] Is Bahri available on project44? (Worth checking with project44 sales given their broad coverage claims)
- [ ] Does Bahri support EDI messaging? (Not confirmed from public sources -- direct inquiry may be needed)
- [ ] Is Bahri developing an API as part of Saudi Vision 2030 digital transformation?
- [ ] What specific events does ShipsGo return for Bahri container tracking? (Requires ShipsGo API testing)
- [ ] Are cutoff dates communicated through Bahri's portal or only through booking agents?

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | [https://www.bahri.sa](https://www.bahri.sa) |
| Bahri Logistics Portal | [https://bahrilogistics.sa](https://bahrilogistics.sa/) |
| Cargo Tracking (login required) | [https://www.bahri.sa/en/logistic-services/cargo-tracking/](https://www.bahri.sa/en/logistic-services/cargo-tracking/) |
| Vessel Tracking | [https://www.bahri.sa/en/logistic-services/vessel-tracking/](https://www.bahri.sa/en/logistic-services/vessel-tracking/) |
| Voyage Schedules | [https://www.bahri.sa/en/logistic-services/voyage-schedules/](https://www.bahri.sa/en/logistic-services/voyage-schedules/) |
| Master Schedule | [https://www.bahri.sa/en/logistic-services/master-schedule/](https://www.bahri.sa/en/logistic-services/master-schedule/) |
| Service Line | [https://www.bahri.sa/en/logistic-services/service-line/](https://www.bahri.sa/en/logistic-services/service-line/) |
| Container Specifications | (available on portal) |
| INTTRA Carrier Network | [https://www.inttra.com/ocean-carrier-network/](https://www.inttra.com/ocean-carrier-network/) |
| Vizion Supported Carriers | [https://docs.vizionapi.com/docs/supported-carriers](https://docs.vizionapi.com/docs/supported-carriers) |
| ShipsGo Bahri Tracking | [https://shipsgo.com/ocean/carriers/bahri/container-tracking](https://shipsgo.com/ocean/carriers/bahri/container-tracking) |
| ShipsGo API Docs | [https://api.shipsgo.com/docs/v2/](https://api.shipsgo.com/docs/v2/) |
| SeaRates Bahri Tracking | [https://www.searates.com/sealine/bahri](https://www.searates.com/sealine/bahri) |
| Fluent Cargo Bahri Schedules | [https://www.fluentcargo.com/carriers/scac/NSAU](https://www.fluentcargo.com/carriers/scac/NSAU) |
| DCSA Members | [https://dcsa.org/about-us/](https://dcsa.org/about-us/) |
| Bahri Investor Relations | [https://investors.bahri.sa](https://investors.bahri.sa/2024/about-bahri.html) |
| DKT Allseas - Bahri Partner | [https://dktallseas.com/bahri.html](https://dktallseas.com/bahri.html) |
