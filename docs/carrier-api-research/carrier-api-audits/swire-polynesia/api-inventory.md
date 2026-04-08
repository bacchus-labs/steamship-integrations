# Swire Shipping (Polynesia Line) -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing
> **Researched by**: Agent
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | Swire Shipping (Polynesia Line) -- formerly Polynesia Line Ltd., now operating under the Swire Shipping brand |
| **SCAC Code** | PLLU (Polynesia Line services via Apia, Samoa); parent Swire Shipping also uses CHVW, SWCK, and SSBF (U.S. shipments) |
| **Parent Company** | The China Navigation Company Pte Ltd (CNCo), part of the Swire Group |
| **Alliance** | Independent (not a member of any shipping alliance) |
| **Primary Services** | Container, breakbulk, project cargo, refrigerated cargo -- South Pacific island trade |
| **Market Position** | Regional specialist, South Pacific. Sole carrier on the U.S. West Coast to South Pacific trade lane after Hamburg Sud exited in May 2023. Shares vessel space with NPDL via a VSA on the CALPAC service |
| **Headquarters** | Singapore (CNCo); Polynesia Line historically based in San Rafael, California |
| **Website** | https://www.swireshipping.com (primary); https://www.polynesialine.com (redirects to Swire Shipping) |

### Corporate History

Polynesia Line Ltd. was founded in 1967 as a specialized ocean carrier connecting the South Pacific islands to the U.S. West Coast. In 2013, it became fully owned by The China Navigation Company (CNCo), the deep-sea shipping arm of the Swire Group. The Polynesia Line brand has since been absorbed into the Swire Shipping brand, and polynesialine.com now redirects to swireshipping.com. Swire Shipping also acquired Westwood Shipping Lines in June 2022 (rebranded to Swire Shipping in February 2024). The PLY (Polynesia Line) service continues as one of Swire Shipping's 13 line services.

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | No dedicated developer portal found |
| **Developer portal URL** | N/A |
| **API documentation URL(s)** | N/A -- Swire Shipping mentions "API and EDI solutions" on their Digital Solutions page but no public API documentation was found |
| **Documentation quality** | None -- no public API documentation available |
| **OpenAPI/Swagger spec available?** | No |
| **Sandbox/test environment?** | Unknown |
| **Developer registration** | N/A -- no self-service developer registration found |
| **Developer support channels** | General contact via swireshipping.com; no dedicated developer support channels found |
| **Community/third-party libraries** | None found for direct Swire Shipping API. Third-party tracking aggregators (ShipsGo, TimeToCargo, Beacon, SeaRates) offer Swire Shipping tracking via their own APIs |
| **API changelog / release notes** | N/A |

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | No -- The China Navigation Company / Swire Shipping is not a DCSA member. DCSA members are MSC, Maersk, CMA CGM, Hapag-Lloyd, ONE, Evergreen, Yang Ming, HMM, and ZIM |
| **DCSA APIs implemented** | None |
| **DCSA TNT version** | N/A |
| **DCSA Booking version** | N/A |
| **DCSA Schedules version** | N/A |
| **Known DCSA deviations** | N/A -- Swire Shipping does not implement DCSA APIs |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Unknown | Swire Shipping mentions "EDI solutions" on their Digital Solutions page, but specific EDI message types are not publicly documented |
| **INTTRA integration** | Unknown | No confirmed INTTRA partnership found in public sources |
| **BIC (Bureau International des Containers)** | Yes | Standard container ID format used in tracking portal |
| **UN/LOCODE** | Unknown | Port codes used internally are not publicly documented |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | N/A -- no public API available |
| **Auth documentation** | N/A |
| **Registration process** | N/A -- no developer registration available. Swire Shipping mentions API/EDI integration is available but requires direct engagement with their team |
| **Registration URL** | N/A |
| **Partner program required?** | Unknown -- likely requires direct business relationship for any API/EDI access |
| **Partner program URL** | N/A |
| **Credential type** | N/A |
| **Token refresh supported?** | N/A |
| **Token lifetime** | N/A |
| **Access tiers** | N/A |
| **IP whitelisting required?** | Unknown |

### Access Requirements Summary for SSL

Swire Shipping does not offer a public API or developer portal. Their website references "API and EDI solutions" as part of their Digital Solutions offering, but access appears to require direct engagement with Swire Shipping's commercial or IT team. SSL would need to establish a business relationship and negotiate API/EDI access as part of a partnership arrangement. Given Swire Shipping's position as a regional niche carrier (rather than a top-10 global carrier), their digital integration capabilities are likely more limited than major carriers and may be gated behind commercial agreements.

The most viable path to tracking data for Swire Shipping shipments may be through third-party aggregators (ShipsGo, Portcast, Beacon, etc.) or web portal scraping, rather than a direct API integration.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field has a row.
> Availability legend: check = Available | x = Not available | warning = Partial / limited | question = Unknown

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ❌ | N/A | N/A | N/A | No public API. Schedule search available on web portal at swireshipping.com |
| 1.2 | Point-to-Point Route Options | ❌ | N/A | N/A | N/A | No public API. Route search available on web portal |
| 1.3 | Booking Lifecycle | ❌ | N/A | N/A | N/A | No public API. Online booking available on web portal for registered users |
| 1.4 | Shipping Instructions | ❌ | N/A | N/A | N/A | No public API. Possibly available via EDI (unconfirmed) |
| 1.5 | Rates | ❌ | N/A | N/A | N/A | No public API. "Instant rates" feature available on web portal |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❌ | N/A | N/A | `ECP` | No public API |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❌ | N/A | N/A | `EFC` | No public API |
| 2.3 | Documentation Cutoff | DCO | ❌ | N/A | N/A | `DCO` | No public API |
| 2.4 | VGM Cutoff | VCO | ❌ | N/A | N/A | `VCO` | No public API |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ❌ | N/A | N/A | `FCO` | No public API |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❌ | N/A | N/A | `LCO` | No public API |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ❌ | N/A | N/A | Inferred from first EquipmentEvent | No public API |
| 3.2 | Empty Container Gate-Out (Pickup) | ❌ | N/A | N/A | `GTOT` + `EMPTY` | No public API. Web portal tracking may show this milestone |
| 3.3 | Full Container Gate-In | ❌ | N/A | N/A | `GTIN` + `LADEN` | No public API |
| 3.4 | Container Loaded on Vessel | ❌ | N/A | N/A | `LOAD` + `LADEN` | No public API. Web portal shows tracking milestones |
| 3.5 | Container Discharged at Transshipment | ❌ | N/A | N/A | `DISC` + `LADEN` + transshipment | No public API |
| 3.6 | Container Loaded at Transshipment | ❌ | N/A | N/A | `LOAD` + `LADEN` + transshipment | No public API |
| 3.7 | Container Discharged at Destination | ❌ | N/A | N/A | `DISC` + `LADEN` | No public API |
| 3.8 | Full Container Gate-Out (Delivery) | ❌ | N/A | N/A | `GTOT` + `LADEN` | No public API |
| 3.9 | Empty Container Returned | ❌ | N/A | N/A | `GTIN` + `EMPTY` | No public API |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ❌ | N/A | N/A | `DEPA` + classifier | No public API. Schedule data available on web portal |
| 4.2 | Estimated Time of Arrival | ETA | ❌ | N/A | N/A | `ARRI` + classifier | No public API. Schedule data available on web portal |
| 4.3 | Vessel Arrival at Transshipment | -- | ❌ | N/A | N/A | `ARRI` at intermediate | No public API |
| 4.4 | Vessel Departure from Transshipment | -- | ❌ | N/A | N/A | `DEPA` at intermediate | No public API |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❌ | No public API |
| Event Polling with timestamp filter | ❌ | No public API |
| Event Classifier Progression (PLN->EST->ACT) | ❌ | No public API |
| Retracted Events | ❌ | No public API |
| Change Remarks | ❌ | No public API |
| Delay Reason Codes | ❌ | No public API |

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
> - Swire Shipping does not expose any public API endpoints. All 30 fields are marked as unavailable via direct API.
> - However, the web portal at swireshipping.com does provide tracking (by container, booking, or B/L number), schedule search, rate quotes, and online booking for registered users. The data exists -- it is just not accessible via a documented API.
> - Swire Shipping's Digital Solutions page mentions "API and EDI solutions" which suggests some form of programmatic access may be available to commercial partners, but no documentation is publicly accessible.
> - Third-party aggregators (ShipsGo, Portcast, Beacon, TimeToCargo, SeaRates) offer tracking data for Swire Shipping, likely obtained via web scraping or private data-sharing arrangements.

---

## Endpoint Reference

Swire Shipping does not expose any publicly documented API endpoints. This section is intentionally left empty.

---

## Rate Limits & Quotas

N/A -- no public API available.

---

## Webhook / Push Support

N/A -- no webhook or push notification system found.

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | https://na.swireshipping.com/Tracking/Public (North America); https://www.swireshipping.com/requestTrackShipment (global) |
| **Login required?** | No -- basic tracking available without login. Registered users get additional eCommerce features (bookings, documents, dashboard) |
| **Data available on portal but NOT in API** | All tracking data is portal-only since there is no public API. Portal shows container status, vessel/voyage details, ETD/ETA, and milestone events by container, booking, or B/L number |
| **Scraping feasibility** | Not assessed. Portal is web-based. Third-party aggregators successfully obtain Swire Shipping tracking data, suggesting data extraction is feasible |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Unknown -- Swire Shipping mentions "EDI solutions" on their Digital Solutions page but specific details are not publicly documented |
| **EDI message types** | Unknown |
| **EDI connection method** | Unknown |
| **EDI documentation** | Contact Swire Shipping directly |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Unknown | Not confirmed in publicly available carrier lists. project44 covers 98%+ of global ocean freight but Swire Shipping is a niche regional carrier |
| **FourKites** | Unknown | Not confirmed. FourKites covers 85+ ocean carriers but explicit Swire Shipping coverage not found |
| **Vizion** | Unknown | Not confirmed. Vizion claims 99% ocean freight coverage but explicit Swire Shipping listing not found |
| **INTTRA / E2open** | Unknown | No confirmed partnership found |
| **CargoSmart** | Unknown | No confirmed partnership found |
| **ShipsGo** | Yes | Offers Swire Shipping container tracking API with "unlimited API calls." Source: https://shipsgo.com/ocean/carriers/swire/container-tracking |
| **Portcast** | Yes | Offers real-time and predictive visibility for Swire Shipping / China Navigation Company via web app and API. Source: https://www.portcast.io/carrier-coverage/china-navigation-company-swire-shipping-container-tracking |
| **Beacon** | Yes | Offers Swire Shipping container tracking. Source: https://www.beacon.com/tracking/container/swire-shipping |
| **TimeToCargo** | Yes | Offers API for Swire Shipping and Polynesia Line tracking. Source: https://timetocargo.com/shipping-lines/swire-shipping |
| **SeaRates** | Yes | Offers Swire Shipping container tracking. Source: https://www.searates.com/sealine/swire_shipping/container-tracking |

> **Aggregator note:** Since Swire Shipping has no public API, third-party aggregators represent the most viable path to programmatic tracking data. ShipsGo, Portcast, Beacon, and TimeToCargo all confirm Swire Shipping / China Navigation Company coverage. These aggregators likely obtain data through web scraping or private data-sharing agreements with the carrier. For SDK integration, using one of these aggregators would be significantly simpler than attempting to negotiate direct API access with Swire Shipping.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown -- no API to measure | Unknown |
| **API uptime/reliability** | N/A -- no public API | N/A |
| **Historical data depth** | Unknown | Unknown |
| **Timezone handling** | Unknown | Unknown |
| **Character encoding** | Unknown | Unknown |

### Known Issues & Gotchas

- **No public API**: The most significant limitation. All programmatic access to Swire Shipping data must go through third-party aggregators or web scraping. Swire Shipping's "API and EDI solutions" appear to be available only through direct commercial engagement.

- **Multiple SCAC codes**: Swire Shipping uses different SCAC codes depending on the service: PLLU (Polynesia Line via Apia), CHVW, SWCK, and SSBF (U.S. shipments). The appropriate SCAC code depends on the ocean service carrying the cargo, which adds complexity to shipment identification and routing.

- **Niche South Pacific trade**: Swire Shipping's Polynesia Line service operates on a fortnightly frequency between the U.S. West Coast (Oakland, Long Beach) and South Pacific islands (Apia, Pago Pago, Papeete, etc.). The low frequency and small fleet size mean tracking event volume will be low compared to major carriers.

- **VSA with NPDL**: Swire Shipping has a vessel sharing agreement with NPDL on the CALPAC service between Oakland/Long Beach and the South Pacific. Shipments may appear under either carrier's vessels, complicating tracking.

- **Brand consolidation**: Polynesia Line, Westwood Shipping, and the historical China Navigation Company brands are all now under the Swire Shipping umbrella. Legacy references to these brands may appear in documentation or systems.

### Recently Deprecated or Changed

- Polynesia Line's standalone website (polynesialine.com) now redirects to swireshipping.com.
- Westwood Shipping Lines was rebranded to Swire Shipping effective February 1, 2024.
- Hamburg Sud exited the South Pacific trade in May 2023, leaving Swire Shipping as the primary U.S. West Coast to South Pacific carrier.

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | No -- not via direct API. Partial -- via third-party aggregator (ShipsGo, Portcast, etc.) |
| **Implementation effort** | Very High (no API) for direct integration; Medium for aggregator-based integration |
| **DCSA base adapter usable?** | No -- Swire Shipping is not a DCSA member and has no DCSA-compliant APIs |

### Recommended Approach

Swire Shipping does not offer a public API, which rules out a direct carrier adapter in the traditional sense. The recommended approach has two tiers:

1. **Primary (aggregator-based)**: Integrate with a third-party aggregator that covers Swire Shipping -- ShipsGo or Portcast appear to have confirmed coverage. This provides container tracking data without needing to negotiate API access with Swire Shipping directly. The aggregator adapter would normalize the aggregator's response format (which is already somewhat standardized) to the canonical data model.

2. **Fallback (commercial engagement)**: If aggregator data quality or coverage is insufficient, SSL could engage Swire Shipping's commercial team to negotiate direct API or EDI access. Their Digital Solutions page suggests some form of programmatic integration exists for commercial partners, but the scope, quality, and cost are unknown.

Web portal scraping is a third option but is not recommended as a primary strategy due to fragility, maintenance burden, and potential ToS violations.

### Recommended Lookup Method

**Container number** or **Bill of Lading number** -- both are supported on the web portal tracking page, and third-party aggregators typically support both lookup methods for Swire Shipping.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Every 6-12 hours -- the PLY service runs on a fortnightly schedule with limited port calls, so events are infrequent |
| **Incremental filter** | Dependent on aggregator capabilities. Full re-fetch likely required |
| **Batch tracking** | Dependent on aggregator capabilities. Likely one call per shipment |

### Auth Implementation Notes

N/A for direct Swire Shipping integration (no public API). Auth requirements would depend on the chosen aggregator's authentication mechanism.

### Edge Cases to Handle

- **Multiple SCAC codes**: Ensure the adapter can handle shipments under any of the Swire Shipping SCAC codes (PLLU, CHVW, SWCK, SSBF) and map them correctly to the Swire Shipping carrier.
- **VSA-shared vessels**: Shipments on the CALPAC service may use NPDL vessels. Container tracking should follow the container regardless of vessel operator.
- **Low event frequency**: With fortnightly sailings and limited port calls in the South Pacific, tracking events may be sparse and widely spaced. The adapter should handle long gaps between events gracefully.

### Mapping Complexity

**Low complexity for aggregator-based integration** -- third-party aggregators typically provide pre-normalized tracking data. The main mapping work would be from the aggregator's format to the canonical model, which is generally straightforward.

**Unknown complexity for direct integration** -- if Swire Shipping's undocumented API or EDI capability is eventually accessed, the mapping complexity is unknown until the response format is understood.

---

## Open Questions

- [ ] Does Swire Shipping offer a private API to commercial partners? Their Digital Solutions page mentions "API and EDI solutions" but no documentation is publicly available.
- [ ] What EDI message types does Swire Shipping support? Are they connected to INTTRA/E2open?
- [ ] Does SSL have an existing business relationship with Swire Shipping? This would be required to negotiate direct API/EDI access.
- [ ] Which third-party aggregator provides the best data quality for Swire Shipping? ShipsGo, Portcast, Beacon, and TimeToCargo all claim coverage.
- [ ] Does project44 or Vizion cover Swire Shipping? Their broad coverage claims (98%+ and 99% respectively) might include niche carriers like Swire.
- [ ] What is the actual data freshness and event granularity available through aggregators for Swire Shipping? Do aggregators provide milestone-level events or just high-level status updates?
- [ ] Are cutoff times available through any channel (aggregator, EDI, or portal) for Swire Shipping Polynesia Line sailings?

---

## Source Links

| Resource | URL |
|----------|-----|
| Swire Shipping Website | https://www.swireshipping.com |
| Polynesia Line (redirects to Swire Shipping) | https://www.polynesialine.com |
| Swire Shipping Tracking (North America) | https://na.swireshipping.com/Tracking/Public |
| Swire Shipping Tracking (Global) | https://www.swireshipping.com/requestTrackShipment |
| Swire Shipping Digital Solutions | https://www.swireshipping.com/information/info-pages/our-solutions/digital-solutions/ |
| PLY Service Page | https://www.swireshipping.com/information/info-pages/our-solutions/ocean-services/ply/ |
| Swire Shipping FAQ (North America) | https://na.swireshipping.com/About/Faq |
| Swire Shipping SCAC Help Article | https://kb.swireshipping.com/hc/en-gb/articles/360024162614 |
| The China Navigation Company | https://www.swirecnco.com/ |
| Westwood Acquisition Announcement | https://www.businesswire.com/news/home/20220628006202/en/ |
| ShipsGo Swire Tracking | https://shipsgo.com/ocean/carriers/swire/container-tracking |
| Portcast Swire Tracking | https://www.portcast.io/carrier-coverage/china-navigation-company-swire-shipping-container-tracking |
| Beacon Swire Tracking | https://www.beacon.com/tracking/container/swire-shipping |
| TimeToCargo Swire Tracking | https://timetocargo.com/shipping-lines/swire-shipping |
| Panjiva PLLU Profile | https://panjiva.com/scac_profiles/profile/PLLU |
| Fluent Cargo CHVW Schedules | https://www.fluentcargo.com/carriers/scac/CHVW |
