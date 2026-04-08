# WECO Shipping -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing
> **Researched by**: Agent
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | WECO Shipping (formerly Dannebrog Rederi) |
| **SCAC Code** | None found -- WECO is not a container shipping line and likely does not have a SCAC code |
| **Parent Company** | Privately owned by the Wedell-Wedellsborg family (Johan Wedell-Wedellsborg, owner since 2001) |
| **Alliance** | None / Independent |
| **Primary Services** | Dry bulk (Handy/Supra/Ultramax), product tankers (MR segment), RoRo (tonnage provider), project cargo (heavy lift) |
| **Market Position** | Niche operator -- dry bulk and tanker specialist with ~50 vessels. Not a container line. Fleet of 49 vessels, 17,694 voyage days and 9.6M+ tonnes transported in 2024 |
| **Headquarters** | Rungsted, Denmark |
| **Website** | https://wecoshipping.com/ |

**Important context:** WECO Shipping is NOT a container shipping line. The company operates exclusively in dry bulk, product tankers, RoRo (as tonnage provider), and project cargo. They do not operate container vessels, do not offer container liner services, and do not have container booking/tracking infrastructure. This fundamentally limits the applicability of the SSL SDK, which is designed for container shipment tracking.

### Business Units

| Unit | Focus | Notes |
|------|-------|-------|
| **Weco Bulk** | Dry bulk maritime transport (Handy, Supra, Ultramax vessels) | Agricultural goods, steel, scrap, aluminum, cement, coal, petcoke, iron ore, wood pellets |
| **Weco Tankers** | MR product tankers (30-50,000 DWT) | Tankers commercially operated through Stena Weco joint venture. IMO II-III cargoes and petroleum products |
| **Weco RoRo** | RoRo and break bulk liner services | Tonnage provider only (not operator). Formerly Nordana Line (acquired from DFDS). Services from Europe to Americas and Europe to Africa |
| **Weco Projects** | Multi-purpose heavy lift vessels | Tonnage provider of specialized project cargo vessels |

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | No |
| **Developer portal URL** | N/A |
| **API documentation URL(s)** | N/A |
| **Documentation quality** | None -- no API documentation exists |
| **OpenAPI/Swagger spec available?** | No |
| **Sandbox/test environment?** | No |
| **Developer registration** | N/A |
| **Developer support channels** | General contact: +45 4517 7777; no developer-specific channels |
| **Community/third-party libraries** | None found |
| **API changelog / release notes** | N/A |

WECO Shipping has no digital platform, API, or developer ecosystem. Their website is a corporate presence site with company information, fleet details, and contact forms. There is no tracking portal, booking system, or any programmatic interface available.

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | No -- DCSA is specifically for container shipping lines; WECO does not operate container vessels |
| **DCSA APIs implemented** | None |
| **DCSA TNT version** | N/A |
| **DCSA Booking version** | N/A |
| **DCSA Schedules version** | N/A |
| **Known DCSA deviations** | N/A -- not applicable to non-container carriers |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Unknown | No information found. Dry bulk and tanker operators typically use voyage charterparty fixtures rather than EDI for container-style transactions |
| **INTTRA integration** | No | INTTRA is a container shipping platform; not relevant for bulk/tanker operators |
| **BIC (Bureau International des Containers)** | No | BIC is a container identification standard; WECO does not operate containers |
| **UN/LOCODE** | Unknown | Ports are referenced on their website but no structured port data is exposed |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | N/A -- no API exists |
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

There is no API access to obtain. WECO Shipping does not provide any programmatic interface for tracking, booking, or schedule information. As a dry bulk and tanker operator (not a container line), WECO's business operations are conducted through traditional chartering and commercial management channels rather than digital platforms. SSL would need to contact WECO directly for any data integration, which would likely involve manual processes or custom arrangements.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field has a row.
> Availability legend: check = Available | x = Not available | warning = Partial / limited | question = Unknown

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ❌ | N/A | N/A | N/A | No schedule API. WECO operates tramp (non-liner) services; schedules are not published |
| 1.2 | Point-to-Point Route Options | ❌ | N/A | N/A | N/A | No routing API. Tramp shipping routes are determined per-fixture |
| 1.3 | Booking Lifecycle | ❌ | N/A | N/A | N/A | No booking API. Chartering done via brokers and direct negotiation |
| 1.4 | Shipping Instructions | ❌ | N/A | N/A | N/A | No shipping instructions API |
| 1.5 | Rates | ❌ | N/A | N/A | N/A | No rates API. Dry bulk and tanker rates negotiated per-fixture |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❌ | N/A | N/A | `ECP` | Not applicable -- WECO does not operate containers |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❌ | N/A | N/A | `EFC` | Not applicable -- no container operations |
| 2.3 | Documentation Cutoff | DCO | ❌ | N/A | N/A | `DCO` | Not applicable in container context |
| 2.4 | VGM Cutoff | VCO | ❌ | N/A | N/A | `VCO` | Not applicable -- VGM is a container-specific requirement |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ❌ | N/A | N/A | `FCO` | Not applicable -- no FCL operations |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❌ | N/A | N/A | `LCO` | Not applicable -- no LCL operations |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ❌ | N/A | N/A | Inferred from first EquipmentEvent | Not applicable -- no container operations |
| 3.2 | Empty Container Gate-Out (Pickup) | ❌ | N/A | N/A | `GTOT` + `EMPTY` | Not applicable |
| 3.3 | Full Container Gate-In | ❌ | N/A | N/A | `GTIN` + `LADEN` | Not applicable |
| 3.4 | Container Loaded on Vessel | ❌ | N/A | N/A | `LOAD` + `LADEN` | Not applicable |
| 3.5 | Container Discharged at Transshipment | ❌ | N/A | N/A | `DISC` + `LADEN` + transshipment | Not applicable |
| 3.6 | Container Loaded at Transshipment | ❌ | N/A | N/A | `LOAD` + `LADEN` + transshipment | Not applicable |
| 3.7 | Container Discharged at Destination | ❌ | N/A | N/A | `DISC` + `LADEN` | Not applicable |
| 3.8 | Full Container Gate-Out (Delivery) | ❌ | N/A | N/A | `GTOT` + `LADEN` | Not applicable |
| 3.9 | Empty Container Returned | ❌ | N/A | N/A | `GTIN` + `EMPTY` | Not applicable |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ❌ | N/A | N/A | `DEPA` + classifier | No API; vessel positions available via third-party AIS services (MarineTraffic, VesselFinder) |
| 4.2 | Estimated Time of Arrival | ETA | ❌ | N/A | N/A | `ARRI` + classifier | Same as 4.1 |
| 4.3 | Vessel Arrival at Transshipment | -- | ❌ | N/A | N/A | `ARRI` at intermediate | Not applicable -- bulk/tanker vessels typically make direct port calls |
| 4.4 | Vessel Departure from Transshipment | -- | ❌ | N/A | N/A | `DEPA` at intermediate | Not applicable |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❌ | No API infrastructure |
| Event Polling with timestamp filter | ❌ | No API infrastructure |
| Event Classifier Progression (PLN->EST->ACT) | ❌ | No API infrastructure |
| Retracted Events | ❌ | No API infrastructure |
| Change Remarks | ❌ | No API infrastructure |
| Delay Reason Codes | ❌ | No API infrastructure |

### Coverage Summary

| Category | Fields Available | Fields Partial | Fields Unavailable | Fields Unknown | Coverage % |
|----------|-----------------|---------------|-------------------|----------------|-----------|
| API Domains (1.x) | 0/5 | 0/5 | 5/5 | 0/5 | 0% |
| Cutoffs (2.x) | 0/6 | 0/6 | 6/6 | 0/6 | 0% |
| Container Milestones (3.x) | 0/9 | 0/9 | 9/9 | 0/9 | 0% |
| Transport Events (4.x) | 0/4 | 0/4 | 4/4 | 0/4 | 0% |
| Change Detection (5.x) | 0/6 | 0/6 | 6/6 | 0/6 | 0% |
| **Total** | **0/30** | **0/30** | **30/30** | **0/30** | **0%** |

> **Notes on Coverage:**
> WECO Shipping has 0% field coverage because it is not a container shipping line. All 30 required data fields are designed for container shipping operations (container milestones, container cutoffs, container booking lifecycle). WECO operates dry bulk carriers and product tankers, which use fundamentally different operational workflows (voyage charterparties, laytime calculations, demurrage) that are outside the scope of the SSL SDK's canonical data model.

---

## Endpoint Reference

WECO Shipping has no API endpoints. This section is intentionally empty.

---

## Rate Limits & Quotas

N/A -- no API exists.

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | None -- WECO does not offer a web tracking portal |
| **Login required?** | N/A |
| **Data available on portal but NOT in API** | N/A -- no portal or API exists |
| **Scraping feasibility** | N/A -- nothing to scrape |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Unknown |
| **EDI message types** | Unknown -- dry bulk/tanker operators typically do not use container EDI message types (IFTMIN, COPARN, etc.) |
| **EDI connection method** | Unknown |
| **EDI documentation** | N/A |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | No | project44's ocean container tracking does not cover non-container carriers |
| **FourKites** | No | FourKites ocean visibility focuses on container shipping |
| **Vizion** | No | Vizion covers container shipping lines, not bulk/tanker operators |
| **INTTRA / E2open** | No | INTTRA is a container shipping platform |
| **CargoSmart** | No | CargoSmart focuses on container shipping |
| **MarineTraffic** | Yes | AIS-based vessel tracking covers WECO's fleet. Not container-specific; provides vessel position, ETA, port calls |
| **VesselFinder** | Yes | AIS-based vessel tracking covers WECO's fleet |

> **Aggregator note:** Standard container shipping aggregators (project44, FourKites, Vizion, INTTRA, CargoSmart) do not cover WECO because it is not a container carrier. AIS-based vessel tracking services (MarineTraffic, VesselFinder) can provide vessel-level position data for WECO's fleet, but this is vessel tracking rather than shipment/cargo tracking. These services do not provide cargo-level milestones, cutoffs, or booking information.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | N/A -- no API | N/A |
| **API uptime/reliability** | N/A -- no API | N/A |
| **Historical data depth** | N/A -- no API | N/A |
| **Timezone handling** | N/A -- no API | N/A |
| **Character encoding** | N/A -- no API | N/A |

### Known Issues & Gotchas

- **Not a container carrier**: WECO Shipping is a dry bulk and tanker operator. The entire SSL SDK data model (container milestones, container cutoffs, DCSA event codes) does not apply to WECO's operations. Any integration would require a fundamentally different data model designed for tramp shipping (voyage charterparties, laytime, demurrage/despatch, Notice of Readiness, etc.).

- **Tramp vs. liner model**: Container shipping uses a liner model (fixed schedules, published routes). WECO operates in the tramp market (vessels go where cargo is, routes determined per-fixture). This means schedules, routes, and ETAs are not published in advance and change per voyage.

- **No digital infrastructure**: WECO has no API, no developer portal, no tracking portal, and no publicly accessible digital systems for cargo or vessel tracking. Business is conducted through traditional chartering channels.

### Recently Deprecated or Changed

- N/A -- no API has ever existed.

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | No -- WECO is not a container carrier. The SSL SDK's canonical data model (container milestones, DCSA events, container cutoffs) is fundamentally incompatible with WECO's dry bulk and tanker operations |
| **Implementation effort** | N/A -- not feasible within the current SDK scope |
| **DCSA base adapter usable?** | No -- DCSA standards are for container shipping; WECO does not operate containers |

### Recommended Approach

An adapter for WECO Shipping is not recommended within the current SSL SDK scope. The SDK is designed for container shipment tracking using the DCSA data model, and WECO does not operate container vessels.

If SSL needs to track WECO bulk or tanker shipments in the future, this would require a separate project with a different data model. The dry bulk and tanker shipping industries use different concepts (voyage charterparties, laytime, demurrage, bill of lading for bulk cargo) that do not map to the DCSA container event model. Third-party AIS vessel tracking services (MarineTraffic, VesselFinder) could provide vessel-level position data, but not cargo-level tracking.

### Recommended Lookup Method

N/A -- no API exists.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | N/A |
| **Incremental filter** | N/A |
| **Batch tracking** | N/A |

### Auth Implementation Notes

N/A -- no API exists.

### Edge Cases to Handle

- N/A -- no adapter recommended.

### Mapping Complexity

N/A -- no adapter is feasible. The WECO data model (dry bulk / tanker operations) is entirely different from the container shipping data model used by the SSL SDK.

---

## Open Questions

- [ ] Why is WECO Shipping listed in the SSL carrier index? Is SSL involved in bulk or tanker cargo that uses WECO vessels?
- [ ] Does SSL need vessel-level tracking (AIS position data) for WECO vessels, separate from container tracking?
- [ ] Does WECO's RoRo division (formerly Nordana Line) carry any containerized cargo on its RoRo/break-bulk services between Europe-Americas and Europe-Africa?
- [ ] Is there a separate WECO digital system (not publicly accessible) used for commercial operations that SSL could integrate with?

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | https://wecoshipping.com/ |
| About Page | https://wecoshipping.com/about/ |
| Fleet Page | https://wecoshipping.com/fleet/ |
| Solutions Page | https://wecoshipping.com/solutions/ |
| Parent Group (Weco) | https://weco.dk/weco-shipping/ |
| Weco RoRo | https://wecororo.com/ |
| LinkedIn (Dannebrog Rederi) | https://www.linkedin.com/company/dannebrog-rederi-as |
