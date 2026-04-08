# Shipping Corporation of India (SCI) -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing
> **Researched by**: Agent
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | The Shipping Corporation of India Ltd. (commonly "SCI") |
| **SCAC Code** | SCIU |
| **Parent Company** | Government of India (Ministry of Ports, Shipping and Waterways) -- public sector undertaking |
| **Alliance** | Independent (no alliance membership) |
| **Primary Services** | Container, Tankers (crude and product), Bulk Carriers, Offshore Supply Vessels, Break Bulk, Passenger-cum-Cargo, LPG Carriers |
| **Market Position** | India's national shipping line and largest domestic carrier. Owns/operates approx. 35% of Indian tonnage. Fleet of ~55 vessels (as of 2025). Niche carrier focused on Indian subcontinent trade; not among global top-20 container lines |
| **Headquarters** | Mumbai, India |
| **Website** | https://www.shipindia.com |

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | No |
| **Developer portal URL** | N/A |
| **API documentation URL(s)** | N/A -- no public API documentation found |
| **Documentation quality** | None |
| **OpenAPI/Swagger spec available?** | No |
| **Sandbox/test environment?** | No |
| **Developer registration** | N/A |
| **Developer support channels** | General contact via shipindia.com; no developer-specific channels |
| **Community/third-party libraries** | None found for direct SCI integration. Third-party aggregator APIs (Portcast, ShipsGo, GoComet, SeaRates, Vizion) provide SCI tracking via scraping/aggregation |
| **API changelog / release notes** | N/A |

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
| **Known DCSA deviations** | N/A -- SCI does not implement any DCSA APIs |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Unknown | No public documentation of EDI capabilities found. As a government-owned carrier with significant bulk/tanker operations, some EDI support is plausible but unconfirmed for container services |
| **INTTRA integration** | Unknown | SCI is not listed as an INTTRA carrier partner in available materials. Given its niche regional focus, INTTRA integration is unlikely |
| **BIC (Bureau International des Containers)** | Yes | Standard container ID format used (B/L prefixes include SCJU) |
| **UN/LOCODE** | Unknown | Likely used in internal systems for Indian ports but not confirmed |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | N/A -- no public API exists |
| **Auth documentation** | N/A |
| **Registration process** | N/A |
| **Registration URL** | N/A |
| **Partner program required?** | N/A |
| **Partner program URL** | N/A |
| **Credential type** | N/A |
| **Token refresh supported?** | N/A |
| **Token lifetime** | N/A |
| **Access tiers** | N/A |
| **IP whitelisting required?** | N/A |

### Access Requirements Summary for SSL

SCI does not offer any public API for tracking, booking, schedules, or any other shipping data. There is no developer portal, no API documentation, and no known partner program for API access. The only digital interface is their web portal tracking page at `shipindia.com/frontcontroller/track_trace`.

To obtain SCI shipment data programmatically, SSL would need to either: (a) contact SCI directly to inquire about any private/unpublished API or EDI capabilities, (b) use a third-party aggregator (Portcast, Vizion, ShipsGo, GoComet) that provides SCI tracking data through web scraping or other means, or (c) implement web scraping of the SCI tracking portal (subject to ToS and reliability concerns).

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field has a row.
> Availability legend: check = Available | x = Not available | warning = Partial / limited | question = Unknown

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ❌ | N/A | N/A | N/A | No API. Vessel schedule information available on web portal only |
| 1.2 | Point-to-Point Route Options | ❌ | N/A | N/A | N/A | No API. Route information available on web portal only |
| 1.3 | Booking Lifecycle | ❌ | N/A | N/A | N/A | No API. Bookings handled via email, phone, or agents |
| 1.4 | Shipping Instructions | ❌ | N/A | N/A | N/A | No API. SI submission via traditional channels |
| 1.5 | Rates | ❌ | N/A | N/A | N/A | No API. Rates obtained via direct inquiry |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❌ | N/A | N/A | `ECP` | No API |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❌ | N/A | N/A | `EFC` | No API |
| 2.3 | Documentation Cutoff | DCO | ❌ | N/A | N/A | `DCO` | No API |
| 2.4 | VGM Cutoff | VCO | ❌ | N/A | N/A | `VCO` | No API |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ❌ | N/A | N/A | `FCO` | No API |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❌ | N/A | N/A | `LCO` | No API |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ❌ | N/A | N/A | Inferred from first EquipmentEvent | No API |
| 3.2 | Empty Container Gate-Out (Pickup) | ❌ | N/A | N/A | `GTOT` + `EMPTY` | No API. Some milestone data may be visible on web tracking portal |
| 3.3 | Full Container Gate-In | ❌ | N/A | N/A | `GTIN` + `LADEN` | No API |
| 3.4 | Container Loaded on Vessel | ❌ | N/A | N/A | `LOAD` + `LADEN` | No API. Web portal shows loading status |
| 3.5 | Container Discharged at Transshipment | ❌ | N/A | N/A | `DISC` + `LADEN` + transshipment | No API |
| 3.6 | Container Loaded at Transshipment | ❌ | N/A | N/A | `LOAD` + `LADEN` + transshipment | No API |
| 3.7 | Container Discharged at Destination | ❌ | N/A | N/A | `DISC` + `LADEN` | No API. Web portal shows discharge status |
| 3.8 | Full Container Gate-Out (Delivery) | ❌ | N/A | N/A | `GTOT` + `LADEN` | No API |
| 3.9 | Empty Container Returned | ❌ | N/A | N/A | `GTIN` + `EMPTY` | No API |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ❌ | N/A | N/A | `DEPA` + classifier | No API. Schedule information on web portal only |
| 4.2 | Estimated Time of Arrival | ETA | ❌ | N/A | N/A | `ARRI` + classifier | No API |
| 4.3 | Vessel Arrival at Transshipment | -- | ❌ | N/A | N/A | `ARRI` at intermediate | No API |
| 4.4 | Vessel Departure from Transshipment | -- | ❌ | N/A | N/A | `DEPA` at intermediate | No API |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❌ | No API exists |
| Event Polling with timestamp filter | ❌ | No API exists |
| Event Classifier Progression (PLN->EST->ACT) | ❌ | No API exists |
| Retracted Events | ❌ | No API exists |
| Change Remarks | ❌ | No API exists |
| Delay Reason Codes | ❌ | No API exists |

### Coverage Summary

| Category | Fields Available | Fields Unavailable | Fields Unknown | Coverage % |
|----------|-----------------|-------------------|----------------|-----------|
| API Domains (1.x) | 0/5 | 5/5 | 0/5 | 0% |
| Cutoffs (2.x) | 0/6 | 6/6 | 0/6 | 0% |
| Container Milestones (3.x) | 0/9 | 9/9 | 0/9 | 0% |
| Transport Events (4.x) | 0/4 | 4/4 | 0/4 | 0% |
| Change Detection (5.x) | 0/6 | 6/6 | 0/6 | 0% |
| **Total** | **0/30** | **30/30** | **0/30** | **0%** |

> **Notes on Coverage:**
> SCI has zero API coverage. The carrier does not expose any public API for any shipping data domain. All data access is limited to the web tracking portal (container, B/L, and booking reference lookup) and traditional communication channels (email, phone, agents). Third-party aggregators provide some tracking data coverage for SCI through web scraping, but this is not a direct API integration.

---

## Endpoint Reference

SCI does not expose any public API endpoints. This section is intentionally empty.

---

## Rate Limits & Quotas

N/A -- no API exists.

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | https://www.shipindia.com/frontcontroller/track_trace |
| **Login required?** | No -- basic tracking available without login |
| **Data available on portal but NOT in API** | All data is portal-only since no API exists. Portal supports lookup by container number, Bill of Lading number, and booking reference number. Returns container status/milestone information, vessel details, and schedule data |
| **Scraping feasibility** | Potentially feasible -- the portal is a standard web form without visible anti-bot protection (uses standard HTML form submission). However, ToS may prohibit automated access, and the portal's reliability for automated scraping is unknown. Third-party aggregators (Portcast, ShipsGo, GoComet) already scrape/aggregate SCI tracking data |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Unknown |
| **EDI message types** | Unknown -- no public documentation |
| **EDI connection method** | Unknown |
| **EDI documentation** | Contact SCI directly |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Unknown | SCI not explicitly listed in project44 carrier coverage. Given SCI's small container fleet and regional focus, coverage is unlikely |
| **FourKites** | Unknown | No explicit SCI coverage confirmed |
| **Vizion** | Unknown | Vizion claims 99% ocean freight coverage; SCI may be covered but not explicitly confirmed |
| **INTTRA / E2open** | Unknown | SCI not listed as an INTTRA carrier partner |
| **CargoSmart** | Unknown | No explicit SCI coverage confirmed |
| **Portcast** | Yes | Portcast explicitly lists SCI in carrier coverage. Provides real-time and predictive container tracking via web app and API. Supports container, booking, and B/L tracking. Source: https://www.portcast.io/carrier-coverage/sci-shipping-corporation-of-india-container-tracking |
| **ShipsGo** | Yes | ShipsGo provides SCI container tracking by container number, booking number, or B/L. Source: https://shipsgo.com/ocean/carriers/sci/container-tracking |
| **GoComet** | Yes | GoComet provides SCI container tracking on their unified dashboard. Uses SCIU SCAC code. Source: https://www.gocomet.com/online-container-tracking/carriers/sciu |
| **SeaRates** | Yes | SeaRates provides SCI container tracking. Source: https://www.searates.com/sealine/sci |

> **Aggregator note:** Since SCI has no direct API, aggregator integration is the only viable path for programmatic tracking data. Portcast appears to be the most established aggregator with explicit SCI coverage and offers both a web interface and a "ready-to-integrate API." ShipsGo, GoComet, and SeaRates also provide SCI tracking but may rely on web scraping. The aggregator approach adds a dependency and potential latency but is the only realistic option short of SCI developing their own API.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown -- no API. Web portal updates are likely delayed compared to carriers with real-time APIs | Unknown |
| **API uptime/reliability** | N/A -- no API | N/A |
| **Historical data depth** | Unknown -- web portal likely shows current shipment status only | Unknown |
| **Timezone handling** | Unknown -- likely IST (UTC+5:30) given Indian headquarters, but not confirmed | Estimated |
| **Character encoding** | Unknown | Unknown |

### Known Issues & Gotchas

- **No API whatsoever**: SCI is one of the least digitally mature carriers among those tracked by SSL. There is no public API, no developer portal, no published EDI documentation, and no DCSA compliance. This makes SCI one of the most challenging carriers to integrate with.

- **Government-owned bureaucracy**: As a public sector undertaking under the Indian government, SCI's pace of digital transformation is constrained by government procurement and approval processes. API development is not a near-term priority based on available information.

- **Container is a small part of SCI's business**: SCI's fleet is heavily weighted toward tankers, bulk carriers, and offshore vessels. Container shipping is a smaller service line, which further reduces the priority of container-focused API development.

- **Multiple SCAC codes**: SCI appears associated with both SCIU and SCJU in various industry databases. The B/L prefix is typically SCJU. Ensure both codes are handled in any integration.

- **Slot sharing and feeder arrangements**: SCI's container services rely on slot sharing, slot charters, and feeder arrangements with other carriers rather than operating large container fleets directly. This means SCI container tracking may involve containers on other carriers' vessels.

### Recently Deprecated or Changed

- No API has ever existed, so nothing to deprecate.

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | No -- direct integration is not possible. Partial -- via aggregator (Portcast API) |
| **Implementation effort** | Very High (no API) -- direct integration would require web scraping. Medium via aggregator (Portcast) |
| **DCSA base adapter usable?** | No -- SCI has no DCSA implementation and no API of any kind |

### Recommended Approach

Direct API integration with SCI is not feasible as the carrier exposes no public API. There are two realistic options:

1. **Aggregator integration (recommended)**: Integrate with Portcast's API, which explicitly covers SCI and provides real-time and predictive container tracking. Portcast offers a "ready-to-integrate API" with documentation at portcast.stoplight.io. This approach trades a direct carrier relationship for a working integration path. The tradeoff is an additional vendor dependency and whatever data limitations exist in Portcast's SCI coverage.

2. **Web scraping (fallback)**: Scrape the SCI tracking portal at `shipindia.com/frontcontroller/track_trace`. The portal supports container, B/L, and booking reference lookups. The form is a simple HTML submission without visible anti-bot measures. However, scraping is fragile, may violate ToS, and provides less structured data than an API.

For SSL's use case, the aggregator approach via Portcast is strongly recommended. If SCI container volumes are low enough for SSL's business, it may also be acceptable to defer SCI integration entirely and handle SCI shipments via manual tracking.

### Recommended Lookup Method

**Bill of Lading number** (via aggregator or web portal) -- B/L is the standard shipping document and is supported by both the SCI web portal and aggregator platforms. The B/L prefix SCJU can be used to identify SCI shipments.

**Container number** as secondary -- for per-container tracking through aggregators.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Every 4-6 hours via aggregator API. If web scraping, limit to every 6-12 hours to reduce detection risk |
| **Incremental filter** | Full re-fetch required -- no timestamp-based filtering available via aggregator or portal |
| **Batch tracking** | Depends on aggregator capabilities. Portcast may support batch queries. Via scraping, one query per shipment |

### Auth Implementation Notes

No direct auth needed since SCI has no API. If using Portcast as aggregator, follow Portcast's API authentication flow (likely API key or OAuth2 -- refer to portcast.stoplight.io documentation).

### Edge Cases to Handle

- **SCAC code ambiguity**: SCI is associated with both SCIU and SCJU. The adapter should recognize both codes when identifying SCI shipments.

- **Slot-shared containers**: SCI containers may physically travel on other carriers' vessels due to slot sharing arrangements. Tracking data may reference non-SCI vessels.

- **Aggregator data gaps**: Aggregator-sourced data may be less complete or less timely than direct carrier API data. Milestone granularity may be limited compared to carriers with native APIs.

- **Portal changes**: If using web scraping, the SCI portal could change its HTML structure without notice, breaking the scraper.

### Mapping Complexity

**Low complexity (via aggregator)**: Portcast and similar aggregators return normalized tracking data, reducing the mapping effort. The main work is mapping the aggregator's data model to SSL's canonical model.

**High complexity (via scraping)**: If scraping the SCI portal, the response is HTML that must be parsed for status milestones, dates, and vessel information. The HTML structure is undocumented and subject to change.

---

## Open Questions

- [ ] Does SCI have any private/unpublished API available to business partners? Contact SCI IT department to inquire
- [ ] Does SCI support EDI (EDIFACT) for container shipping? If so, which message types and connection methods?
- [ ] What is Portcast's data quality and freshness for SCI specifically? How often is SCI tracking data updated?
- [ ] Does SSL have sufficient SCI container volume to justify integration effort, or can SCI shipments be handled manually?
- [ ] Is SCI planning any digital transformation or API development? Government of India has digitization initiatives (e.g., Sagarmala project) that could accelerate this
- [ ] Are there other aggregators beyond Portcast with confirmed SCI coverage and API access?

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | https://www.shipindia.com |
| Container Services Page | https://www.shipindia.com/services/servicedetails/container |
| Web Portal Tracking | https://www.shipindia.com/frontcontroller/track_trace |
| Wikipedia | https://en.wikipedia.org/wiki/Shipping_Corporation_of_India |
| Portcast SCI Tracking | https://www.portcast.io/carrier-coverage/sci-shipping-corporation-of-india-container-tracking |
| ShipsGo SCI Tracking | https://shipsgo.com/ocean/carriers/sci/container-tracking |
| GoComet SCI Tracking | https://www.gocomet.com/online-container-tracking/carriers/sciu |
| SeaRates SCI Tracking | https://www.searates.com/sealine/sci |
| Chaine SCAC Codes (confirms SCIU) | https://handbook.chaineapp.com/api/docs/ocean-visibility/supported-scac-codes/ |
