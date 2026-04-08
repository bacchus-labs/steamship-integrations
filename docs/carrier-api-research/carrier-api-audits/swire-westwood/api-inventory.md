# Swire Shipping (Westwood) -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing
> **Researched by**: Agent
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | Swire Shipping US Inc. (formerly Westwood Shipping Lines, Inc.; commonly "Westwood" or "Swire Shipping North America") |
| **SCAC Code** | WWSU (Westwood service); SSBF (Swire Shipping US shipments); CHVW (Swire Shipping international) |
| **Parent Company** | The China Navigation Company (CNCo), a wholly owned subsidiary of John Swire & Sons Limited (Swire Group) |
| **Alliance** | Independent (no alliance membership) |
| **Primary Services** | Container, breakbulk, project cargo, heavy lift, oversized cargo, forest products -- Pacific Northwest to Northeast Asia trade |
| **Market Position** | Niche regional carrier specializing in Pacific Northwest (US/Canada) to North Asia (Japan, South Korea, China) trade. Acquired by Swire Shipping in 2022; rebranded February 1, 2024 |
| **Headquarters** | Puyallup, WA, USA (North America operations); Swire Shipping global HQ in Singapore |
| **Website** | https://na.swireshipping.com |

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | No |
| **Developer portal URL** | N/A |
| **API documentation URL(s)** | N/A -- no public API documentation found |
| **Documentation quality** | None -- no public API documentation exists |
| **OpenAPI/Swagger spec available?** | No |
| **Sandbox/test environment?** | No / Unknown |
| **Developer registration** | N/A -- no developer program exists |
| **Developer support channels** | General contact via na.swireshipping.com; phone: (1) 253 200 3800; email: @swireshipping.com domain |
| **Community/third-party libraries** | None found for direct integration. Third-party tracking aggregators (Terminal49, ShipsGo, Portcast, SeaRates) support Swire/Westwood container tracking |
| **API changelog / release notes** | N/A |

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | No -- Swire Shipping is not a DCSA member. DCSA members are the top 9 container carriers (MSC, Maersk, CMA CGM, Hapag-Lloyd, ONE, Evergreen, Yang Ming, HMM, ZIM) |
| **DCSA APIs implemented** | None |
| **DCSA TNT version** | N/A |
| **DCSA Booking version** | N/A |
| **DCSA Schedules version** | N/A |
| **Known DCSA deviations** | N/A -- Swire does not implement DCSA APIs |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Unknown | No public documentation on EDI capabilities found. May support EDI through INTTRA/E2open given industry norms, but not confirmed |
| **INTTRA integration** | Unknown | No confirmed INTTRA partnership found in research. Swire's customer portal handles booking and SI submission directly |
| **BIC (Bureau International des Containers)** | Yes | Standard container ID format used in tracking |
| **UN/LOCODE** | Unknown | Port codes used in schedules not confirmed as UN/LOCODE |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | N/A -- no public API |
| **Auth documentation** | N/A |
| **Registration process** | N/A for API. Customer portal registration at https://online-na.swireshipping.com for booking/SI/tracking |
| **Registration URL** | https://online-na.swireshipping.com (customer portal, not API) |
| **Partner program required?** | N/A -- no API program exists |
| **Partner program URL** | N/A |
| **Credential type** | N/A |
| **Token refresh supported?** | N/A |
| **Token lifetime** | N/A |
| **Access tiers** | N/A |
| **IP whitelisting required?** | N/A |

### Access Requirements Summary for SSL

Swire Shipping (Westwood) does not offer a public API or developer portal. There is no documented programmatic access method for tracking, schedules, booking, or any other shipping data. The carrier provides a web-based customer portal at https://online-na.swireshipping.com where registered customers can manage bookings, submit shipping instructions, track shipments, and print bills of lading.

For SSL to obtain programmatic tracking data from Swire/Westwood shipments, the recommended path is through a third-party aggregator such as Terminal49 (confirmed support for both CHVW and WWSU SCAC codes), ShipsGo, or Portcast. Direct API integration is not possible without a private partnership arrangement with Swire Shipping, which would require contacting their North America operations team directly to inquire about any unpublished API capabilities.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field has a row.
> Availability legend: check = Available | x = Not available | warning = Partial / limited | question = Unknown

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ❌ | N/A (no API) | N/A | N/A | Schedule data visible on web portal at na.swireshipping.com/Schedules but no API access |
| 1.2 | Point-to-Point Route Options | ❌ | N/A (no API) | N/A | N/A | Route information on website only |
| 1.3 | Booking Lifecycle | ❌ | N/A (no API) | N/A | N/A | Booking managed through customer portal at online-na.swireshipping.com; no API |
| 1.4 | Shipping Instructions | ❌ | N/A (no API) | N/A | N/A | SI submission via customer portal only |
| 1.5 | Rates | ❌ | N/A (no API) | N/A | N/A | Rates obtained through direct contact or portal |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❌ | N/A | N/A | `ECP` | No API access |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❌ | N/A | N/A | `EFC` | No API access |
| 2.3 | Documentation Cutoff | DCO | ❌ | N/A | N/A | `DCO` | No API access. Cutoff info may be available on portal or in booking confirmations |
| 2.4 | VGM Cutoff | VCO | ❌ | N/A | N/A | `VCO` | No API access. VGM tools available on portal |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ❌ | N/A | N/A | `FCO` | No API access |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❌ | N/A | N/A | `LCO` | No API access |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ❌ | N/A | N/A | Inferred from first EquipmentEvent | No API access |
| 3.2 | Empty Container Gate-Out (Pickup) | ❌ | N/A | N/A | `GTOT` + `EMPTY` | No API access. May be visible on web portal tracking |
| 3.3 | Full Container Gate-In | ❌ | N/A | N/A | `GTIN` + `LADEN` | No API access |
| 3.4 | Container Loaded on Vessel | ❌ | N/A | N/A | `LOAD` + `LADEN` | No API access. Web tracking shows loading milestone |
| 3.5 | Container Discharged at Transshipment | ❌ | N/A | N/A | `DISC` + `LADEN` + transshipment | No API access |
| 3.6 | Container Loaded at Transshipment | ❌ | N/A | N/A | `LOAD` + `LADEN` + transshipment | No API access |
| 3.7 | Container Discharged at Destination | ❌ | N/A | N/A | `DISC` + `LADEN` | No API access. Web tracking shows discharge milestone |
| 3.8 | Full Container Gate-Out (Delivery) | ❌ | N/A | N/A | `GTOT` + `LADEN` | No API access |
| 3.9 | Empty Container Returned | ❌ | N/A | N/A | `GTIN` + `EMPTY` | No API access |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ❌ | N/A | N/A | `DEPA` + classifier | No API access. Schedule data on website only |
| 4.2 | Estimated Time of Arrival | ETA | ❌ | N/A | N/A | `ARRI` + classifier | No API access |
| 4.3 | Vessel Arrival at Transshipment | -- | ❌ | N/A | N/A | `ARRI` at intermediate | No API access |
| 4.4 | Vessel Departure from Transshipment | -- | ❌ | N/A | N/A | `DEPA` at intermediate | No API access |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❌ | No API or webhook support |
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
| Container Milestones (3.x) | 0/9 | 9/9 | 0/9 | 0% |
| Transport Events (4.x) | 0/4 | 4/4 | 0/4 | 0% |
| Change Detection (5.x) | 0/6 | 6/6 | 0/6 | 0% |
| **Total** | **0/30** | **30/30** | **0/30** | **0%** |

> **Notes on Coverage:**
> - Swire Shipping (Westwood) has zero direct API coverage. The carrier does not provide any public API, developer portal, or documented programmatic access method.
> - Tracking, schedule, and booking data is available through the web-based customer portal at https://na.swireshipping.com and https://online-na.swireshipping.com, but only for manual/browser-based access.
> - Third-party aggregators (Terminal49, ShipsGo, Portcast, Beacon, SeaRates) support Swire/Westwood tracking, likely by scraping the carrier's web portal. These aggregators could provide a path to programmatic tracking data without direct carrier API access.
> - The coverage percentage reflects direct API availability only. Through aggregators, tracking milestones and transport events may be partially recoverable.

---

## Endpoint Reference

Swire Shipping (Westwood) does not expose any public API endpoints. This section is intentionally omitted.

### Lookup Methods Summary

| Identifier Type | Supported? | Which Endpoints? | Notes |
|----------------|-----------|-----------------|-------|
| **Bill of Lading (B/L) number** | ❌ (direct) / ✅ (via aggregators) | N/A direct; Terminal49, ShipsGo, etc. | Web portal supports B/L tracking; aggregators expose this programmatically |
| **Booking reference** | ❌ (direct) / ✅ (via aggregators) | N/A direct; some aggregators | Web portal supports booking tracking |
| **Container number** | ❌ (direct) / ✅ (via aggregators) | N/A direct; Terminal49, ShipsGo, etc. | Web portal supports container tracking; aggregators expose this programmatically |
| **Carrier booking number** | ❌ | N/A | |
| **Vessel IMO / voyage** | ❌ | N/A | Schedule data on website only |

---

## Rate Limits & Quotas

N/A -- no API exists.

---

## Webhook / Push Support

Swire Shipping does not offer webhooks or push notifications. Third-party aggregators (ShipsGo, Terminal49) offer their own webhook/notification mechanisms for Swire shipment tracking.

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | https://na.swireshipping.com/Tracking/Public |
| **Login required?** | No -- basic tracking available without login |
| **Data available on portal but NOT in API** | All data is portal-only since no API exists. Portal provides: container tracking, export tracking, schedule lookup, booking management (with login), shipping instruction submission (with login), bill of lading printing (with login) |
| **Scraping feasibility** | Not assessed. Portal is web-based. A PDF guide for Track and Trace usage is available at https://na.swireshipping.com/documents/pdfs/Track%20and%20Trace%20-%20How%20To.pdf. ToS should be reviewed before considering scraping |

### Customer Portal (Authenticated)

| Detail | Value |
|--------|-------|
| **Portal URL** | https://online-na.swireshipping.com |
| **Features** | Online booking, shipping instruction submission, bill of lading printing, shipment tracking, booking templates for repeat shipments |
| **Registration** | Customer account required; register through the portal |
| **VGM Tools** | Available as part of eCommerce services on the portal |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Unknown |
| **EDI message types** | Unknown |
| **EDI connection method** | Unknown |
| **EDI documentation** | Unknown -- contact Swire Shipping directly |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Unknown | Not confirmed in research. project44's carrier list does not explicitly list Swire/Westwood in publicly available documentation |
| **FourKites** | Unknown | Not confirmed. FourKites covers 85+ ocean carriers but explicit Swire coverage not verified |
| **Vizion** | Unknown | Not confirmed. Vizion claims 98% global shipment coverage; Swire/Westwood may be included given aggregator breadth |
| **INTTRA / E2open** | Unknown | No confirmed INTTRA partnership found for Swire/Westwood |
| **CargoSmart** | Unknown | Not confirmed |
| **Terminal49** | Yes | Confirmed support for both CHVW (Swire Shipping) and WWSU (Westwood Shipping Lines) SCAC codes. Provides container and B/L tracking |
| **ShipsGo** | Yes | Confirmed Swire Shipping tracking by container, booking, or B/L number. Offers tracking API and notifications |
| **Portcast** | Yes | Confirmed coverage for China Navigation Company (Swire Shipping). Provides real-time and predictive visibility via web app and API |
| **Beacon** | Yes | Confirmed Swire Shipping container tracking support |
| **SeaRates** | Yes | Confirmed Swire Shipping container tracking |

> **Aggregator note:** Since Swire Shipping has no direct API, aggregator integration is the only viable path for programmatic tracking data. Terminal49 is the strongest confirmed option with explicit support for both the legacy WWSU and current CHVW SCAC codes. ShipsGo and Portcast also offer API-based tracking solutions covering Swire. For SSL, the recommended approach is to integrate with one of these aggregators rather than attempting to build a direct carrier adapter. The aggregator data coverage for milestones and ETAs is likely partial (tracking events rather than full cutoff and booking lifecycle data).

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown -- no API to measure. Aggregators report near-real-time for major milestones | Unknown |
| **API uptime/reliability** | N/A -- no API | N/A |
| **Historical data depth** | Unknown | Unknown |
| **Timezone handling** | Unknown | Unknown |
| **Character encoding** | Unknown | Unknown |

### Known Issues & Gotchas

- **No API whatsoever**: Swire Shipping (Westwood) has no public API, developer portal, or documented programmatic access. This is unusual even among smaller carriers. All integration must go through aggregators or web portal scraping.

- **Multiple SCAC codes**: Swire Shipping uses at least three SCAC codes (WWSU for Westwood service, SSBF for US shipments, CHVW for Swire international). The applicable code depends on the ocean service carrying the cargo. SSL must track which SCAC applies to each shipment. Canadian shipments use Cargo Control Number 9311 instead.

- **Brand transition in progress**: Westwood Shipping Lines was rebranded to Swire Shipping US Inc. effective February 1, 2024. Legacy WWSU SCAC code may still be in use alongside newer SSBF/CHVW codes. Some aggregators track under WWSU (Terminal49) while others use CHVW (Fluent Cargo).

- **Niche trade lane**: Westwood service operates exclusively between the Pacific Northwest (US/Canada) and Northeast Asia (Japan, South Korea, China). This is a specialized, low-volume trade compared to mainline carriers. The carrier operates a small fleet and limited sailing frequency.

- **Multipurpose fleet**: Unlike major container-only carriers, Swire/Westwood operates multipurpose vessels handling containers, breakbulk, project cargo, and forest products. Tracking events and data structures may differ from pure container carrier norms.

### Recently Deprecated or Changed

- **February 2024**: Westwood Shipping Lines, Inc. renamed to Swire Shipping US Inc. Email domain changed from @wsl.com to @swireshipping.com. Website moved to na.swireshipping.com. Old WWSU SCAC code may be phased out over time.

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | No (direct) / Partial (via aggregator) -- Swire has no API. A direct adapter is impossible. An aggregator-backed adapter (Terminal49, ShipsGo, or Portcast) could provide tracking data only |
| **Implementation effort** | Very High (no API) for direct; Low-Medium (aggregator passthrough) for tracking via Terminal49 or similar |
| **DCSA base adapter usable?** | No -- no DCSA compliance. Aggregator data format would depend on the chosen aggregator's API |

### Recommended Approach

Direct carrier API integration is not possible for Swire Shipping (Westwood) because no API exists. The recommended approach for SSL is:

1. **Aggregator integration for tracking**: Use Terminal49 (confirmed support for both WWSU and CHVW SCAC codes) or Portcast (confirmed Swire coverage with predictive ETAs) as the tracking data source. This provides container milestone events and ETA/ETD data through the aggregator's normalized API. The SDK adapter would wrap the aggregator's API rather than a carrier-specific API.

2. **Portal-based operations for booking/SI**: Booking creation, shipping instruction submission, and bill of lading management must continue through Swire's customer portal at https://online-na.swireshipping.com. These operations cannot be automated without web scraping or a private arrangement with Swire.

3. **De-prioritize for SDK v1**: Given the niche trade lane (Pacific NW to NE Asia only) and zero API availability, Swire/Westwood should be a low-priority integration. If SSL has significant Westwood volume, pursue an aggregator-backed tracking adapter; otherwise, defer until Swire develops API capabilities or SSL's aggregator strategy matures.

### Recommended Lookup Method

If using an aggregator: **Container number** is the most reliable lookup method for Swire/Westwood tracking across aggregators. B/L number is also widely supported.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Depends on aggregator -- Terminal49 and Portcast push updates; ShipsGo supports polling. Every 4-6 hours is reasonable for in-transit shipments |
| **Incremental filter** | Depends on aggregator API. Terminal49 supports webhook notifications for container updates |
| **Batch tracking** | Depends on aggregator -- Terminal49 supports tracking multiple containers via API; one subscription per container |

### Auth Implementation Notes

N/A for direct carrier integration. Auth would be against the chosen aggregator's API (e.g., Terminal49 API key, Portcast API credentials).

### Edge Cases to Handle

- **SCAC code ambiguity**: A single Swire/Westwood shipment may appear under WWSU, SSBF, or CHVW depending on the data source. The adapter must handle SCAC code normalization and lookups across all three codes.

- **Legacy vs. new brand data**: During the transition period, some systems may reference "Westwood Shipping Lines" while others use "Swire Shipping." Container prefixes and identifiers may vary.

- **Multipurpose cargo**: Breakbulk and project cargo shipments may have different tracking event patterns than standard containerized cargo. The adapter should handle missing container-specific milestones gracefully.

### Mapping Complexity

**Low (if via aggregator)**: Aggregators like Terminal49 provide pre-normalized tracking data. The mapping would be from the aggregator's canonical format to SSL's DCSA-based model, not from a proprietary carrier format. This is significantly simpler than mapping a proprietary carrier API.

**N/A (direct)**: No direct carrier data to map.

---

## Open Questions

- [ ] Does SSL have significant shipment volume on Swire/Westwood services? -- Determines priority of integration effort
- [ ] Does Swire Shipping offer any unpublished API or EDI capabilities to established customers? -- Direct inquiry to Swire NA sales team needed
- [ ] Which aggregator does SSL already use or plan to use? -- Terminal49, Portcast, and ShipsGo all confirm Swire coverage; selecting one would determine the adapter approach
- [ ] Will the WWSU SCAC code be deprecated in favor of SSBF or CHVW? -- Affects long-term identifier strategy
- [ ] Does Swire Shipping support EDI (IFTSTA, IFTMIN) through INTTRA/E2open? -- Would provide an alternative programmatic access path for booking and tracking
- [ ] What is Swire Shipping's roadmap for API development? -- The parent company (Swire Group / CNCo) may be investing in digital capabilities globally

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website (North America) | https://na.swireshipping.com |
| Carrier Website (Global) | https://www.swireshipping.com |
| Customer Portal (North America) | https://online-na.swireshipping.com |
| Web Tracking | https://na.swireshipping.com/Tracking/Public |
| Export Tracking | https://na.swireshipping.com/Tracking/ExportTrackingPublic |
| Schedules | https://na.swireshipping.com/Schedules |
| Track and Trace Instructions (PDF) | https://na.swireshipping.com/documents/pdfs/Track%20and%20Trace%20-%20How%20To.pdf |
| Westwood-to-Swire Rebranding Announcement | https://na.swireshipping.com/News/Releases/Westwood-Shipping-Lines-integration-into-Swire-Shipping-2024-01-25 |
| Rebranding FAQ | https://na.swireshipping.com/News/Releases/Frequently-Asked-Questions-FAQ-2024-02-01 |
| NA FAQ (SCAC codes) | https://na.swireshipping.com/About/Faq |
| Swire Shipping SCAC Help Article | https://kb.swireshipping.com/hc/en-gb/articles/360024162614 |
| Swire Group Marine Services | https://www.swire.com/en/businesses/marine_services.php |
| CNCo (Parent) | https://www.swirecnco.com/ |
| Swire Acquisition of Westwood (BusinessWire) | https://www.businesswire.com/news/home/20220428006372/en/ |
| Terminal49 -- Swire (CHVW) | https://www2.terminal49.com/shipping-lines/chvw-swire-shipping-container-tracking/ |
| Terminal49 -- Westwood (WWSU) | https://terminal49.com/shipping-lines/wwsu-westwood-shipping-lines-container-tracking |
| ShipsGo -- Swire Tracking | https://shipsgo.com/ocean/carriers/swire/container-tracking |
| Portcast -- Swire Tracking | https://www.portcast.io/carrier-coverage/china-navigation-company-swire-shipping-container-tracking |
| Fluent Cargo -- Swire Schedules (CHVW) | https://www.fluentcargo.com/carriers/scac/CHVW |
| Fluent Cargo -- Westwood Schedules (WWSU) | https://www.fluentcargo.com/carriers/scac/WWSU |
