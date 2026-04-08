# Wallenius Wilhelmsen -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing
> **Researched by**: Agent
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | Wallenius Wilhelmsen ASA (commonly "WW" or "WWL") |
| **SCAC Code** | WLWH |
| **Parent Company** | Wallenius Wilhelmsen ASA (publicly listed, Oslo Bors: WAWI) |
| **Alliance** | Independent (not a member of any container shipping alliance) |
| **Primary Services** | RoRo (Roll-on/Roll-off) ocean transportation, finished vehicle logistics, breakbulk, heavy equipment, high & heavy machinery |
| **Market Position** | World's largest RoRo and vehicle carrier, operating ~125-128 vessels on 15 trade routes to six continents |
| **Headquarters** | Oslo, Norway (and Stockholm, Sweden) |
| **Website** | https://www.walleniuswilhelmsen.com |

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | No |
| **Developer portal URL** | N/A |
| **API documentation URL(s)** | N/A -- no public API documentation found |
| **Documentation quality** | None |
| **OpenAPI/Swagger spec available?** | No |
| **Sandbox/test environment?** | No / Unknown |
| **Developer registration** | N/A -- no developer program exists |
| **Developer support channels** | Regional Customer Service teams via website contact forms |
| **Community/third-party libraries** | None found for direct WW API. Third-party tracking aggregators (ShipsGo, Portcast, SeaRates, GoComet) offer WW tracking via scraping or data partnerships |
| **API changelog / release notes** | N/A |

### Digital Modernization Note

On February 17, 2026, Cognizant announced an expanded partnership with Wallenius Wilhelmsen to modernize legacy technology portfolios, introduce AI-driven efficiencies, and build a stronger digital foundation. This partnership covers core applications and infrastructure, suggesting WW's digital capabilities may evolve significantly in the near term, but no public API offering has been announced.

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | No -- DCSA is focused on container shipping; WW is primarily a RoRo/vehicle carrier |
| **DCSA APIs implemented** | None |
| **DCSA TNT version** | N/A |
| **DCSA Booking version** | N/A |
| **DCSA Schedules version** | N/A |
| **Known DCSA deviations** | N/A -- DCSA standards are designed for containerized shipping and do not directly apply to RoRo cargo |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Unknown | No explicit EDI documentation found on WW's public materials. Given the size and scale of their operations, EDI is likely supported for major OEM automotive customers but details are not publicly available |
| **INTTRA integration** | Unknown | INTTRA/E2open primarily serves container carriers. WW as a RoRo carrier may not participate in INTTRA's network |
| **BIC (Bureau International des Containers)** | Unknown | BIC standards are container-focused. WW handles RoRo cargo (vehicles, machinery) which uses different identification schemes (VIN numbers, unit IDs) |
| **UN/LOCODE** | Yes (likely) | Port codes in schedule searches use standard port identifiers |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | N/A -- no public API available |
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

Wallenius Wilhelmsen does not offer a public API or developer portal. There is no self-service or partner-gated API access path. Programmatic access to WW shipment data would need to come through one of the following channels:

1. **Third-party aggregator** (primarily project44, which has explicit RoRo visibility support including WW).
2. **Direct business relationship** -- SSL could approach WW about data integration, but this would be a bespoke arrangement rather than an established developer program.
3. **Web portal scraping** -- WW's Track & Trace portal at walleniuswilhelmsen.com/track-trace provides tracking data, but this approach would be fragile and likely violates ToS.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field has a row.
> Availability legend: check = Available | x = Not available | warning = Partial / limited | question = Unknown
>
> **Important context**: Wallenius Wilhelmsen is a RoRo carrier, not a container liner. Many DCSA-defined container milestones and cutoff codes do not map directly to RoRo operations. RoRo cargo (vehicles, heavy equipment) has a different handling lifecycle than containers. The fields below are assessed against WW's web portal data and third-party aggregator capabilities.

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ⚠️ | Web portal only (walleniuswilhelmsen.com/schedules) | Voyage, port, trade route search | N/A | Schedule search available on website by voyage, port, or trade route. No API endpoint |
| 1.2 | Point-to-Point Route Options | ⚠️ | Web portal only | Route search results | N/A | Website allows searching routes but no programmatic access |
| 1.3 | Booking Lifecycle | ❌ | N/A | N/A | N/A | No booking API. Bookings handled via direct customer service, email, or WW's internal systems |
| 1.4 | Shipping Instructions | ❌ | N/A | N/A | N/A | No SI API. Documentation handled via direct communication |
| 1.5 | Rates | ❌ | Web portal only (walleniuswilhelmsen.com/rate-request) | Rate request form | N/A | Rates available only via manual request form on website. No programmatic rate API |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❌ | N/A | N/A | `ECP` | Not applicable -- RoRo cargo does not use container release workflows |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❌ | N/A | N/A | `EFC` | Not applicable -- RoRo cargo does not use container delivery workflows |
| 2.3 | Documentation Cutoff | DCO | ❓ | Unknown | Unknown | `DCO` | WW likely has documentation cutoffs for cargo but they are not exposed via any API |
| 2.4 | VGM Cutoff | VCO | ❌ | N/A | N/A | `VCO` | VGM is a container-specific SOLAS requirement. Does not apply to standard RoRo cargo |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ❓ | Unknown | Unknown | `FCO` | RoRo equivalent would be cargo receiving cutoff at terminal. Not exposed via API |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❌ | N/A | N/A | `LCO` | LCL is a container shipping concept. Not applicable to RoRo |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ❌ | N/A | N/A | Inferred from first EquipmentEvent | Not applicable -- RoRo does not assign containers to bookings. Cargo units (vehicles/equipment) are tracked by VIN or unit ID |
| 3.2 | Empty Container Gate-Out (Pickup) | ❌ | N/A | N/A | `GTOT` + `EMPTY` | Not applicable -- no empty container pickup in RoRo operations |
| 3.3 | Full Container Gate-In | ❌ | N/A | N/A | `GTIN` + `LADEN` | Not applicable. RoRo equivalent: cargo received at terminal. Track & Trace shows "received at terminal" status |
| 3.4 | Container Loaded on Vessel | ⚠️ | Track & Trace portal | Cargo loaded status | `LOAD` + `LADEN` | Track & Trace shows cargo loaded on vessel. Available on web portal but not via API |
| 3.5 | Container Discharged at Transshipment | ❓ | Track & Trace portal (possibly) | Unknown | `DISC` + `LADEN` + transshipment | Unknown whether transshipment events are shown on the portal |
| 3.6 | Container Loaded at Transshipment | ❓ | Track & Trace portal (possibly) | Unknown | `LOAD` + `LADEN` + transshipment | Unknown whether transshipment loading events are shown |
| 3.7 | Container Discharged at Destination | ⚠️ | Track & Trace portal | Cargo discharged status | `DISC` + `LADEN` | Track & Trace shows discharge at destination. Available on web portal but not via API |
| 3.8 | Full Container Gate-Out (Delivery) | ⚠️ | Track & Trace portal | Line released status | `GTOT` + `LADEN` | Track & Trace tracks cargo from terminal receipt to "discharge and line release." Available on web portal only |
| 3.9 | Empty Container Returned | ❌ | N/A | N/A | `GTIN` + `EMPTY` | Not applicable -- no empty container return in RoRo operations |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ⚠️ | Schedule portal (walleniuswilhelmsen.com/schedules) | ETD in schedule results | `DEPA` + classifier | Available on web schedule portal. No API access |
| 4.2 | Estimated Time of Arrival | ETA | ⚠️ | Schedule portal; Track & Trace portal | ETA in schedule/tracking results | `ARRI` + classifier | Available on web portals. Track & Trace shows expected arrival |
| 4.3 | Vessel Arrival at Transshipment | -- | ❓ | Unknown | Unknown | `ARRI` at intermediate | Unknown -- RoRo routes tend to have fewer transshipments than container services |
| 4.4 | Vessel Departure from Transshipment | -- | ❓ | Unknown | Unknown | `DEPA` at intermediate | Unknown |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❌ | No webhook or push notification capability found |
| Event Polling with timestamp filter | ❌ | No API available for polling |
| Event Classifier Progression (PLN->EST->ACT) | ❌ | No event classifier system |
| Retracted Events | ❌ | No retraction mechanism |
| Change Remarks | ❌ | No change remark capability |
| Delay Reason Codes | ❌ | No delay reason code system |

### Coverage Summary

| Category | Fields Available | Fields Partial | Fields Unavailable | Fields Unknown | Coverage % |
|----------|-----------------|---------------|-------------------|----------------|-----------|
| API Domains (1.x) | 0/5 | 2/5 | 3/5 | 0/5 | 0% (+ 2 portal-only) |
| Cutoffs (2.x) | 0/6 | 0/6 | 4/6 | 2/6 | 0% |
| Container Milestones (3.x) | 0/9 | 3/9 | 4/9 | 2/9 | 0% (+ 3 portal-only) |
| Transport Events (4.x) | 0/4 | 2/4 | 0/4 | 2/4 | 0% (+ 2 portal-only) |
| Change Detection (5.x) | 0/6 | 0/6 | 6/6 | 0/6 | 0% |
| **Total** | **0/30** | **7/30** | **17/30** | **6/30** | **0% via API (23% portal-only, 20% unknown)** |

> **Notes on Coverage:**
> - Wallenius Wilhelmsen has **zero API coverage**. No public API exists for any data category.
> - Several fields are marked "partial" because the data is visible on WW's web portal (Track & Trace, Schedules) but is not accessible programmatically.
> - Many container-specific fields (ERD, EFC, VGM, empty container events) are fundamentally **not applicable** to RoRo operations. WW handles vehicles, machinery, and breakbulk cargo -- not containers.
> - The most promising path to programmatic data access is through **project44**, which explicitly supports RoRo visibility and lists WW as a supported carrier.
> - WW's Track & Trace portal tracks cargo "from the time the cargo is received at the terminal to the time it discharges and is line released," confirming that receive, load, discharge, and release milestones exist in their systems even though they are not API-accessible.

---

## Endpoint Reference

Wallenius Wilhelmsen does not expose any public API endpoints. This section is intentionally omitted.

---

## Rate Limits & Quotas

N/A -- no API available.

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | https://www.walleniuswilhelmsen.com/track-trace |
| **Login required?** | No -- basic tracking available without login |
| **Lookup identifiers** | Booking number, Bill of Lading number, Customer reference number (VIN / Cargo ID search was previously available but removed "due to security concerns") |
| **Data available on portal** | Cargo status from terminal receipt through discharge and line release. Expected arrival dates. Vessel/voyage information |
| **Scraping feasibility** | Difficult -- tracking interface is loaded in a dynamic iframe (`iFrameResize`), suggesting JavaScript-rendered content. ToS likely prohibits scraping |

### Schedule Portal

| Detail | Value |
|--------|-------|
| **Schedule URL** | https://www.walleniuswilhelmsen.com/schedules |
| **Search methods** | By voyage, by port, by trade route |
| **Data available** | Vessel names, ports of call, ETD/ETA, trade routes across 15 global routes |

### Other Digital Tools

| Tool | URL | Notes |
|------|-----|-------|
| MyPortal | Referenced on FAQ page | Customer portal -- likely requires account/login. Details unknown |
| Carbon Calculator | Referenced on FAQ page | Environmental impact tool |
| Rate Request | https://www.walleniuswilhelmsen.com/rate-request | Manual rate inquiry form |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Unknown -- not publicly documented |
| **EDI message types** | Unknown |
| **EDI connection method** | Unknown |
| **EDI documentation** | Not available -- contact carrier directly |

> **Note**: Given WW's scale (125+ vessels, 12,000 employees, major OEM automotive customers like BMW, Toyota, Volkswagen), it is highly likely they support EDI for their largest customers. However, no public documentation of EDI capabilities was found.

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Yes | project44 has explicit RoRo visibility support and lists WW as a supported carrier. RoRo shipment lifecycle tracking covers booking through delivery milestones. This is the most promising integration path |
| **FourKites** | Unknown | FourKites covers 85+ ocean carriers. WW coverage not explicitly confirmed but likely given market position |
| **Vizion** | Unknown | Vizion focuses on container tracking. RoRo coverage unclear |
| **INTTRA / E2open** | Unknown | INTTRA primarily serves container carriers. WW as a RoRo carrier may not participate |
| **CargoSmart** | Unknown | CargoSmart focuses on container shipping. RoRo coverage unclear |
| **Portcast** | Yes | Portcast explicitly lists WWL tracking with "real-time and predictive visibility" via web app or API |
| **ShipsGo** | Yes | ShipsGo offers Wallenius Lines tracking API integration |
| **SeaRates** | Yes | SeaRates offers WW container/cargo tracking |
| **GoComet** | Yes | GoComet offers WW tracking by B/L |

> **Aggregator note**: Since WW has no direct API, aggregator integration is the **only viable path** for programmatic data access. project44 is the strongest candidate due to its explicit RoRo visibility product with documented shipment lifecycle tracking. Portcast is a secondary option. These aggregators likely obtain data through direct partnerships with WW rather than scraping.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown -- no API to measure | Unknown |
| **API uptime/reliability** | N/A -- no API | N/A |
| **Historical data depth** | Unknown | Unknown |
| **Timezone handling** | Unknown | Unknown |
| **Character encoding** | Unknown | Unknown |

### Known Issues & Gotchas

- **No API exists**: The most fundamental constraint. WW has no developer portal, no public API, no published API documentation, and no API registration process. All programmatic access must go through third-party aggregators.

- **RoRo vs. container data model mismatch**: WW handles RoRo cargo (vehicles, machinery, breakbulk), not containers. Many of the canonical container-focused fields (ERD, EFC, VGM, empty container events, LCL cutoffs) are fundamentally inapplicable. The SDK adapter would need a RoRo-specific data mapping that translates vehicle/unit milestones to the closest container equivalents.

- **Cargo ID / VIN tracking removed**: WW previously allowed tracking by cargo ID but removed this capability "due to security concerns." This limits tracking to booking number, B/L number, or customer reference only.

- **Legacy technology stack**: The February 2026 Cognizant partnership announcement for technology modernization suggests WW's current digital infrastructure is legacy-based. API capabilities may emerge in the future but are not available today.

- **Dynamic iframe tracking portal**: The Track & Trace interface loads inside a JavaScript iframe, making automated data extraction technically challenging.

### Recently Deprecated or Changed

- Cargo ID search was removed from Track & Trace "due to security concerns" (date of removal unknown).

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | Partial -- only via third-party aggregator (project44 recommended). No direct carrier API exists |
| **Implementation effort** | Very High (no API) -- requires aggregator integration rather than direct carrier integration. If using project44, effort is Medium (project44 API is well-documented) |
| **DCSA base adapter usable?** | No -- WW is not a DCSA member, has no API, and handles RoRo cargo rather than containers. A fully custom approach is needed |

### Recommended Approach

Wallenius Wilhelmsen cannot be integrated directly -- there is no API to integrate with. The recommended approach is to integrate via **project44's RoRo Visibility** product, which explicitly supports WW and provides a documented API with shipment lifecycle tracking.

The adapter architecture should wrap project44's API rather than WW's non-existent API. This means:

1. **project44 as the data source**: Use project44's Ocean RoRo Visibility API to create/track shipments. project44 handles the data acquisition from WW through their direct partnership.

2. **RoRo milestone mapping**: Map project44's RoRo shipment lifecycle events (booking confirmed, cargo received, loaded, in transit, discharged, delivered) to the canonical DCSA-inspired data model. Some container-specific fields will be permanently unavailable for RoRo cargo.

3. **Fallback to Portcast**: If project44 is not available or cost-prohibitive, Portcast offers WWL tracking with a plug-and-play API and could serve as an alternative data source.

This is fundamentally different from a direct carrier adapter -- it is an aggregator-mediated adapter with the aggregator providing the data acquisition layer.

### Recommended Lookup Method

**Booking number** is the recommended primary lookup, as WW's Track & Trace supports it and project44's RoRo visibility typically initiates tracking via booking references.

**Bill of Lading number** as secondary -- supported by WW's Track & Trace and most aggregators.

**Customer reference number** as supplementary -- WW supports this on their portal.

**VIN / Cargo ID** -- no longer supported directly by WW due to security concerns. May be available through project44.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Dependent on aggregator (project44) rate limits and SLA. RoRo transit times are typically longer than container shipping (weeks to months for vehicle logistics), so every 6-12 hours is likely sufficient |
| **Incremental filter** | Dependent on aggregator API capabilities. project44 supports event-based updates |
| **Batch tracking** | Dependent on aggregator. project44 supports batch operations |

### Auth Implementation Notes

Authentication would be against the **aggregator's API** (project44 or Portcast), not against WW directly. project44 uses OAuth2 with client credentials. No WW-specific auth implementation is needed.

### Edge Cases to Handle

- **RoRo-specific cargo types**: Vehicles are tracked by VIN, heavy machinery by unit ID. These don't map to container numbers. The adapter needs to handle non-container identifier types.

- **Longer transit cycles**: RoRo shipments often have longer transit times and fewer port calls than container services. Polling frequency should reflect this.

- **Multi-unit shipments**: A single booking may contain many individual vehicles. The adapter may need to handle unit-level tracking within a booking.

- **Transshipment rarity**: RoRo services typically run direct routes with fewer transshipment points than container services. Transshipment-related fields may rarely be populated.

- **Container-field inapplicability**: Fields like ERD, EFC, VGM cutoff, empty container return, and LCL cutoff are structurally inapplicable to RoRo cargo. The adapter should explicitly mark these as "not applicable" rather than "unknown."

### Mapping Complexity

**Medium-High complexity (aggregator-mediated).** The primary mapping challenge is not field-level translation (the aggregator handles that) but rather the conceptual gap between RoRo cargo milestones and the container-centric canonical data model:

1. **RoRo milestone translation**: RoRo cargo goes through receive -> load -> transit -> discharge -> release, which roughly maps to GTIN -> LOAD -> transport events -> DISC -> GTOT, but the semantics differ (no container, no empty/laden distinction).

2. **Inapplicable fields**: Roughly 40% of the canonical fields (container-specific cutoffs, empty container events, VGM) are structurally inapplicable to RoRo. The adapter must handle this gracefully.

3. **Aggregator response normalization**: The project44 RoRo response format differs from their container format. A dedicated RoRo normalizer layer is needed.

---

## Open Questions

- [ ] Does SSL have a project44 account or relationship? -- Required for the recommended integration path
- [ ] What is the cost of project44 RoRo Visibility for SSL's expected volume?
- [ ] Does project44's RoRo visibility provide cutoff data for WW shipments?
- [ ] Does WW support EDI for partners? -- Could provide an alternative data channel for larger-volume integrations
- [ ] Does WW's MyPortal (referenced on FAQ page) offer any API or data export capabilities?
- [ ] Is WW planning to release a public API as part of their Cognizant technology modernization initiative?
- [ ] What tracking granularity does project44 provide for WW RoRo shipments? -- Need to confirm which milestones are covered
- [ ] Does Portcast's WWL tracking API provide equivalent coverage to project44?
- [ ] Should the SDK support RoRo-specific identifiers (VIN, unit ID) as first-class lookup types?

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | https://www.walleniuswilhelmsen.com |
| Track & Trace Portal | https://www.walleniuswilhelmsen.com/track-trace |
| Schedule Portal | https://www.walleniuswilhelmsen.com/schedules |
| Rate Request | https://www.walleniuswilhelmsen.com/rate-request |
| SCAC Code FAQ | https://www.walleniuswilhelmsen.com/ocean-support/faq/what-is-wallenius-wilhelmsen-oceans-scac-code |
| Tracking FAQ | https://www.walleniuswilhelmsen.com/ocean-support/faq/how-can-i-track-my-shipment |
| Cognizant Partnership (2026) | https://www.prnewswire.com/news-releases/cognizant-to-provide-strategic-technology-services-for-wallenius-wilhelmsen-302688704.html |
| project44 RoRo Visibility | https://developers.project44.com/guides/shippers/visibility/ocean/roro-visibility |
| project44 RoRo Shipment Lifecycle | https://developers.project44.com/guides/shippers/visibility/ocean/roro/shipment-lifecycle |
| Portcast WWL Tracking | https://www.portcast.io/carrier-coverage/wwl-wallenius-wilhelmsen-logistics-container-tracking |
| ShipsGo WW Tracking | https://shipsgo.com/ocean/carriers/wallenius/container-tracking |
| SeaRates WW Tracking | https://www.searates.com/sealine/wallenius_wilhelmsen/container-tracking |
| GoComet WW Tracking | https://www.gocomet.com/online-container-tracking/carriers/wallenius-wilhelmsen-logistics |
| Fluent Cargo WW Schedules | https://www.fluentcargo.com/carriers/scac/WLWH |
| DCSA Members | https://dcsa.org/about-us-our-work-and-what-we-do-dcsa/members/ |
