# Trailer Bridge -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing
> **Researched by**: Agent
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | Trailer Bridge, Inc. (commonly "Trailer Bridge") |
| **SCAC Code** | TRLD (ocean); TRBR (trucking) |
| **Parent Company** | Privately held (independent); founded by Malcom McLean in 1991 |
| **Alliance** | None / Independent |
| **Primary Services** | Container shipping, RoRo (vehicle transport), breakbulk, integrated truck-barge freight |
| **Market Position** | Niche regional carrier -- one of three Jones Act carriers serving Puerto Rico from Jacksonville. Primarily US-Caribbean trade (Puerto Rico, Dominican Republic, USVI) |
| **Headquarters** | Jacksonville, Florida, USA |
| **Website** | https://www.trailerbridge.com |

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | No |
| **Developer portal URL** | N/A |
| **API documentation URL(s)** | N/A |
| **Documentation quality** | None -- no public API documentation exists |
| **OpenAPI/Swagger spec available?** | No |
| **Sandbox/test environment?** | No |
| **Developer registration** | N/A |
| **Developer support channels** | General: info@trailerbridge.com, +1 (844) 827-4477 |
| **Community/third-party libraries** | None found. Third-party tracking aggregators (ShipsGo, Shippingline.org) provide web-scraping-based Trailer Bridge tracking |
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
| **Known DCSA deviations** | N/A -- Trailer Bridge does not implement any DCSA APIs |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Unknown | No public documentation of EDI capabilities found. As a Jones Act carrier, likely supports basic EDI for US government/military shipments (USTRANSCOM work documented) |
| **INTTRA integration** | Unknown | No confirmed INTTRA partnership found |
| **BIC (Bureau International des Containers)** | Unknown | Standard container numbering likely used but not confirmed |
| **UN/LOCODE** | Unknown | Operates from known ports (USJAX, PRSJU, DOPOP) but UN/LOCODE usage in systems not confirmed |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | N/A -- no public API |
| **Auth documentation** | N/A |
| **Registration process** | N/A -- no developer registration available |
| **Registration URL** | N/A |
| **Partner program required?** | N/A |
| **Partner program URL** | N/A |
| **Credential type** | N/A |
| **Token refresh supported?** | N/A |
| **Token lifetime** | N/A |
| **Access tiers** | N/A |
| **IP whitelisting required?** | N/A |

### Access Requirements Summary for SSL

Trailer Bridge does not offer a public API or developer portal. The only programmatic access paths are:

1. **Web portal scraping**: The QuickTrack portal (https://quicktrack.trailerbridge.com/) allows tracking by booking number, equipment number, or VIN without login. This could potentially be scraped, subject to ToS review.

2. **Customer portal**: A registered customer portal exists at transit.trailerbridge.com with login-protected access, which may expose additional data.

3. **Third-party aggregators**: ShipsGo provides Trailer Bridge tracking via their platform. Vizion and project44 do not appear to support Trailer Bridge.

4. **Direct partnership**: SSL could contact Trailer Bridge directly to negotiate data sharing or EDI connectivity. Given Trailer Bridge's use of Mastery Logistics MasterMind TMS, there may be integration options through that platform.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field has a row.
> Availability legend: check = Available | x = Not available | warning = Partial / limited | question = Unknown

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ❌ | N/A | N/A | N/A | No API. Schedules available on website but not programmatically |
| 1.2 | Point-to-Point Route Options | ❌ | N/A | N/A | N/A | No API. Limited route network (JAX-SJU, JAX-DR, JAX-USVI) |
| 1.3 | Booking Lifecycle | ❌ | N/A | N/A | N/A | No API. Booking done via phone, email, or customer portal |
| 1.4 | Shipping Instructions | ❌ | N/A | N/A | N/A | No API |
| 1.5 | Rates | ❌ | N/A | N/A | N/A | No API. Rates via direct quote requests |

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
| 3.2 | Empty Container Gate-Out (Pickup) | ⚠️ | QuickTrack portal (web) | Unknown | `GTOT` + `EMPTY` | May be visible on QuickTrack portal but no API access |
| 3.3 | Full Container Gate-In | ⚠️ | QuickTrack portal (web) | Unknown | `GTIN` + `LADEN` | May be visible on QuickTrack portal but no API access |
| 3.4 | Container Loaded on Vessel | ⚠️ | QuickTrack portal (web) | Unknown | `LOAD` + `LADEN` | May be visible on QuickTrack portal but no API access |
| 3.5 | Container Discharged at Transshipment | ❌ | N/A | N/A | `DISC` + `LADEN` + transshipment | Trailer Bridge operates direct services with minimal transshipment |
| 3.6 | Container Loaded at Transshipment | ❌ | N/A | N/A | `LOAD` + `LADEN` + transshipment | Same as 3.5 -- direct services, rarely transships |
| 3.7 | Container Discharged at Destination | ⚠️ | QuickTrack portal (web) | Unknown | `DISC` + `LADEN` | May be visible on QuickTrack portal but no API access |
| 3.8 | Full Container Gate-Out (Delivery) | ⚠️ | QuickTrack portal (web) | Unknown | `GTOT` + `LADEN` | May be visible on QuickTrack portal but no API access |
| 3.9 | Empty Container Returned | ⚠️ | QuickTrack portal (web) | Unknown | `GTIN` + `EMPTY` | May be visible on QuickTrack portal but no API access |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ⚠️ | QuickTrack portal (web) | Unknown | `DEPA` + classifier | May be visible on portal but no API access |
| 4.2 | Estimated Time of Arrival | ETA | ⚠️ | QuickTrack portal (web) | Unknown | `ARRI` + classifier | May be visible on portal but no API access |
| 4.3 | Vessel Arrival at Transshipment | -- | ❌ | N/A | N/A | `ARRI` at intermediate | Direct services -- transshipment rare |
| 4.4 | Vessel Departure from Transshipment | -- | ❌ | N/A | N/A | `DEPA` at intermediate | Direct services -- transshipment rare |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❌ | No API, no webhook support |
| Event Polling with timestamp filter | ❌ | No API |
| Event Classifier Progression (PLN->EST->ACT) | ❌ | No API |
| Retracted Events | ❌ | No API |
| Change Remarks | ❌ | No API |
| Delay Reason Codes | ❌ | No API |

### Coverage Summary

| Category | Fields Available | Fields Unavailable | Fields Unknown | Coverage % |
|----------|-----------------|-------------------|----------------|-----------|
| API Domains (1.x) | 0/5 | 5/5 | 0/5 | 0% |
| Cutoffs (2.x) | 0/6 | 6/6 | 0/6 | 0% |
| Container Milestones (3.x) | 0/9 | 3/9 | 0/9 | 0% (6 partial -- portal only) |
| Transport Events (4.x) | 0/4 | 2/4 | 0/4 | 0% (2 partial -- portal only) |
| Change Detection (5.x) | 0/6 | 6/6 | 0/6 | 0% |
| **Total** | **0/30** | **22/30** | **0/30** | **0% confirmed (27% portal-only partial)** |

> **Notes on Coverage:**
> - Trailer Bridge has no public API whatsoever. All "partial" ratings reflect data that may be visible on the QuickTrack web portal but is not accessible programmatically.
> - The QuickTrack portal (https://quicktrack.trailerbridge.com/) supports lookup by booking number, equipment number, or VIN and provides shipment status updates without login.
> - The customer portal at transit.trailerbridge.com may expose additional data behind authentication.
> - Third-party aggregators like ShipsGo provide tracking for Trailer Bridge shipments, likely via web scraping, and offer their own API access to that data.
> - Trailer Bridge operates primarily direct services (Jacksonville to San Juan, Dominican Republic, USVI) with minimal transshipment, so transshipment-related fields (3.5, 3.6, 4.3, 4.4) are operationally less relevant.

---

## Endpoint Reference

Trailer Bridge does not expose any public API endpoints. This section is intentionally left minimal.

### Tracking / Events

| Endpoint | Method | Lookup Params | Pagination | Response Format | Notes |
|----------|--------|--------------|------------|----------------|-------|
| N/A -- no API | -- | -- | -- | -- | QuickTrack web portal only |

### Schedules

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| N/A -- no API | -- | -- | -- | -- | Schedule info on website only |

### Booking

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| N/A -- no API | -- | -- | -- | -- | Booking via phone/email/portal |

### Lookup Methods Summary

| Identifier Type | Supported? | Which Endpoints? | Notes |
|----------------|-----------|-----------------|-------|
| **Bill of Lading (B/L) number** | ❌ (API) / ⚠️ (portal) | QuickTrack web portal | Not listed as a QuickTrack field but may be supported |
| **Booking reference** | ❌ (API) / ✅ (portal) | QuickTrack web portal | One of three lookup fields on QuickTrack |
| **Container number** | ❌ (API) / ✅ (portal) | QuickTrack web portal | Listed as "Equipment Number" on QuickTrack |
| **Carrier booking number** | ❌ (API) / ✅ (portal) | QuickTrack web portal | Same as booking reference |
| **Vessel IMO / voyage** | ❌ | N/A | Not supported for lookup |
| **VIN (Vehicle ID)** | ❌ (API) / ✅ (portal) | QuickTrack web portal | Unique to Trailer Bridge -- supports vehicle tracking by last 8 VIN digits |

---

## Rate Limits & Quotas

| Detail | Value | Source |
|--------|-------|--------|
| **Global rate limit** | N/A -- no API | N/A |
| **Per-endpoint limits** | N/A | N/A |
| **Daily/monthly quota** | N/A | N/A |
| **Rate limit response** | N/A | N/A |
| **Rate limit by** | N/A | N/A |
| **Burst allowance** | N/A | N/A |
| **Different tiers** | N/A | N/A |

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | https://quicktrack.trailerbridge.com/ |
| **Login required?** | No -- QuickTrack allows tracking without a User ID |
| **Data available on portal but NOT in API** | All data is portal-only. QuickTrack provides shipment status by booking number, equipment number, or VIN. Customer portal at transit.trailerbridge.com likely has additional detail behind login |
| **Scraping feasibility** | Potentially feasible -- no login required for QuickTrack. Anti-bot measures and ToS not assessed. ShipsGo and other third-party trackers appear to successfully aggregate Trailer Bridge tracking data, suggesting scraping is viable |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Unknown |
| **EDI message types** | Unknown |
| **EDI connection method** | Unknown |
| **EDI documentation** | Unknown -- contact carrier directly |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | No | Not listed in project44's supported ocean carrier SCAC list |
| **FourKites** | Unknown | No confirmation found |
| **Vizion** | No | Not listed in Vizion's supported carriers list |
| **INTTRA / E2open** | Unknown | No confirmed partnership |
| **CargoSmart** | Unknown | No confirmation found |
| **ShipsGo** | Yes | ShipsGo provides Trailer Bridge container tracking via their platform and API. Supports B/L, booking, and container number lookup |
| **Terminal49** | Unknown | Terminal49 offers multi-carrier tracking API but Trailer Bridge support not confirmed |

> **Aggregator note:** Trailer Bridge is a small regional carrier not covered by major aggregators like project44 or Vizion. ShipsGo appears to be the most viable aggregator option, likely obtaining data via web scraping of the QuickTrack portal. For programmatic tracking, ShipsGo's API may be the path of least resistance compared to building a custom scraper.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown | Unknown |
| **API uptime/reliability** | N/A -- no API | N/A |
| **Historical data depth** | Unknown | Unknown |
| **Timezone handling** | Unknown -- likely US Eastern (Jacksonville HQ) or Atlantic (San Juan) | Estimated |
| **Character encoding** | Unknown | Unknown |

### Known Issues & Gotchas

- **No API at all**: Trailer Bridge is a small regional carrier with no public API, no developer portal, and no published EDI documentation. All digital integration must go through web scraping, third-party aggregators, or direct partnership negotiation.

- **Jones Act carrier**: Trailer Bridge is one of only three Jones Act carriers serving Puerto Rico from Jacksonville (alongside Crowley and TOTE Maritime). Jones Act compliance means US-built, US-flagged, US-crewed vessels. This is relevant for understanding the carrier's regulatory context but does not affect API integration.

- **Integrated truck-barge model**: Trailer Bridge operates an unusual integrated truck-and-barge system rather than traditional container vessels. This means their shipment tracking may use different event concepts than standard container shipping (e.g., barge loading vs. vessel loading).

- **VIN tracking**: QuickTrack supports tracking by Vehicle Identification Number (last 8 digits), reflecting the carrier's significant RoRo/vehicle shipping business. This is unusual for ocean carriers and may indicate a tracking data model oriented around vehicles rather than containers.

- **MasterMind TMS**: Trailer Bridge adopted Mastery Logistics Systems' MasterMind TMS in 2022, with plans to extend it to ocean operations. This modern TMS platform could eventually expose integration points, but no public-facing API has been announced.

- **Logistics division sold**: In October 2025, Trailer Bridge announced the sale of its logistics division to ATS. This may affect the scope of services and technology investments going forward. The ocean shipping operations appear to be retained.

### Recently Deprecated or Changed

- No deprecation notices found (no API to deprecate). The logistics division sale to ATS (October 2025) may restructure the company's technology footprint.

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | No -- not via direct API. Partial via web scraping or ShipsGo aggregator |
| **Implementation effort** | Very High (no API) -- would require web scraping or aggregator integration |
| **DCSA base adapter usable?** | No -- no API exists, let alone a DCSA-compliant one |

### Recommended Approach

Trailer Bridge cannot be integrated via a direct API adapter because no API exists. There are three possible approaches, listed in order of preference:

1. **ShipsGo aggregator integration**: ShipsGo provides Trailer Bridge tracking data via their own API. Building a ShipsGo adapter that covers Trailer Bridge (and potentially other small carriers) would be the most maintainable approach. The trade-off is dependency on a third-party aggregator and whatever data ShipsGo can extract.

2. **Web scraping adapter**: Build a scraper targeting QuickTrack (https://quicktrack.trailerbridge.com/) to extract tracking status by booking or equipment number. This is fragile (UI changes break the scraper) and may violate Trailer Bridge's Terms of Service. Not recommended for production use.

3. **Direct partnership/EDI**: Contact Trailer Bridge to negotiate EDI connectivity or a data feed. Given their adoption of MasterMind TMS (a modern cloud platform), there may be integration possibilities not publicly documented. This requires business development effort.

Given Trailer Bridge's niche market (US-Caribbean, primarily Puerto Rico), the volume of SSL shipments through this carrier should determine the investment level. For low volume, manual tracking via the QuickTrack portal may be sufficient.

### Recommended Lookup Method

**Booking number** is the recommended primary lookup, as it is one of the three fields supported by QuickTrack and is the most universal identifier in the booking workflow.

**Equipment (container) number** as secondary -- also supported by QuickTrack.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | N/A -- no API to poll. If using ShipsGo, follow their recommended polling interval |
| **Incremental filter** | N/A |
| **Batch tracking** | N/A |

### Auth Implementation Notes

No authentication implementation needed -- there is no API. If integrating via ShipsGo, follow ShipsGo's auth requirements.

### Edge Cases to Handle

- **Barge vs. vessel**: Trailer Bridge uses barges rather than traditional container ships. Event terminology and tracking milestones may differ from standard container shipping.
- **VIN-based tracking**: The carrier's RoRo business uses VIN-based tracking, which has no DCSA equivalent and would need special handling.
- **Limited route network**: Only a handful of routes (JAX-SJU, JAX-DR, JAX-USVI), so transshipment events are essentially non-existent.
- **Logistics division sale**: The 2025 sale of the logistics division to ATS may change the carrier's technology stack and integration capabilities.

### Mapping Complexity

**N/A -- no data to map.** There is no API response to transform into the canonical data model. If data is obtained via ShipsGo or web scraping, the mapping complexity depends on the data source's response format rather than Trailer Bridge's own systems.

---

## Webhook / Push Support

No webhook or push notification support available.

---

## Open Questions

- [ ] Does Trailer Bridge support EDI (IFTSTA, COPARN, etc.) for any customers? -- Would enable tracking data exchange without an API
- [ ] Does the MasterMind TMS platform expose any integration APIs that Trailer Bridge could make available? -- Mastery Logistics promotes API capabilities in their platform
- [ ] What data fields are available on the QuickTrack portal? -- Would determine scraping viability and data coverage
- [ ] What data is available behind the customer portal login at transit.trailerbridge.com? -- May have richer data than public QuickTrack
- [ ] Does ShipsGo's Trailer Bridge tracking provide sufficient milestone data for SSL's needs? -- Determines aggregator viability
- [ ] What is SSL's volume of shipments via Trailer Bridge? -- Determines whether integration investment is justified
- [ ] How will the logistics division sale to ATS (October 2025) affect Trailer Bridge's technology investments? -- May impact future API development
- [ ] Does Trailer Bridge participate in any US government/military EDI networks (given USTRANSCOM work)? -- Could provide an alternate data feed

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | https://www.trailerbridge.com |
| QuickTrack Portal | https://quicktrack.trailerbridge.com/ |
| Customer Portal | https://transit.trailerbridge.com |
| Puerto Rico Services | https://www.trailerbridge.com/shipping-solutions/caribbean-shipping/puerto-rico/ |
| Caribbean Shipping | https://www.trailerbridge.com/shipping-solutions/caribbean-shipping/ |
| Vehicle Shipping | https://www.trailerbridge.com/shipping-solutions/caribbean-shipping/vehicle-shipping/ |
| MasterMind TMS Launch | https://www.trailerbridge.com/insights-resources/news/2022/trailer-bridge-launches-mastermind-tms-with-mastery-logistics-systems-inc/ |
| Company History (FundingUniverse) | https://www.fundinguniverse.com/company-histories/trailer-bridge-inc-history/ |
| Panjiva SCAC Profile (TRLD) | https://panjiva.com/scac_profiles/profile/TRLD |
| ShipsGo Tracking | https://shipsgo.com/ocean/carriers/trailerbridge/container-tracking |
| Logistics Division Sale (2025) | https://www.jaxdailyrecord.com/news/2025/oct/07/trailer-bridge-selling-its-logistics-division-to-ats/ |
