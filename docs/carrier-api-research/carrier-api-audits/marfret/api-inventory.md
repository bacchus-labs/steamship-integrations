# Marfret Compagnie Maritime -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing
> **Researched by**: Agent
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | Compagnie Maritime Marfret SAS (commonly "Marfret") |
| **SCAC Code** | MFTU |
| **Parent Company** | Independent (family-owned French company) |
| **Alliance** | None / Independent |
| **Primary Services** | Container, Reefer, RoRo, Multipurpose/Breakbulk, Inland (river/intermodal) |
| **Market Position** | Regional specialist -- French Caribbean, Central America, South America, Mediterranean, North Atlantic. ~45,000 TEUs/year, 80+ ports of call |
| **Headquarters** | Marseille, France |
| **Website** | https://www.marfret.com |

### Key Routes

- **NASP** -- North Atlantic / Southern Pacific
- **MEDCAR** -- Mediterranean / Caribbean
- **Guiana Amazonia** -- Europe / French Guiana / North Brazil
- **North Europe -- French West Indies** -- Europe / Guadeloupe / Martinique
- **INTRACAR** -- Intra-Caribbean feeder
- **Maghreb** -- Marseille / Algeria / Tunisia
- **MPV Service** -- Northern Europe / Caribbean / Guyana (multipurpose/breakbulk)
- **Ireland** -- Le Havre / Waterford
- **Round the World** -- Global service

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
| **Developer support channels** | General contact only: https://www.marfret.com/en/contact-us/ |
| **Community/third-party libraries** | None found |
| **API changelog / release notes** | Not published |

### Digital Tools Available

Marfret provides the following digital tools for customers, none of which are programmatic APIs:

- **Marius** -- Proprietary internal data system for real-time coordination of operations
- **Customer Portal** -- `marfret.locussoftware.com/customer-portal` (Locus Software-based portal for booking and account management)
- **Track & Trace** -- Web-based container tracking at https://www.marfret.com/en/container-tracking/
- **INTTRA Booking** -- Booking requests can be placed via the INTTRA platform
- **Eco-Calculator** -- Carbon footprint assessment tool

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | No -- Marfret is not a DCSA member. DCSA members are: MSC, Maersk, CMA CGM, Hapag-Lloyd, ONE, Evergreen, Yang Ming, HMM, ZIM, and PIL |
| **DCSA APIs implemented** | None |
| **DCSA TNT version** | N/A |
| **DCSA Booking version** | N/A |
| **DCSA Schedules version** | N/A |
| **Known DCSA deviations** | N/A -- Marfret does not implement DCSA APIs |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Yes (via INTTRA) | Booking via INTTRA platform confirmed. Likely supports IFTMIN (Shipping Instructions), COPARN, IFTSTA via INTTRA |
| **INTTRA integration** | Yes | Confirmed -- customers can make booking requests on Marfret vessels via INTTRA login. Source: Marfret website |
| **BIC (Bureau International des Containers)** | Yes | Standard container ID format used (prefix MFTU visible on tracking page) |
| **UN/LOCODE** | Unknown | Not confirmed from available documentation |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | N/A -- no public API |
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

Marfret does not offer any public API or developer portal. There is no known way to obtain programmatic access to Marfret's systems directly. The only electronic integration point is via INTTRA (e2open) for booking operations.

For tracking data, SSL would need to use a third-party aggregator such as project44 or Vizion, both of which confirm Marfret support. Alternatively, web scraping of the Track & Trace portal could be explored but is not recommended as a primary approach.

If deeper integration is needed, SSL would need to contact Marfret directly (via their Marseille headquarters or local agency) to inquire about any private API or EDI capabilities beyond what is publicly documented.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field has a row.
> Availability legend: check = Available | x = Not available | warning = Partial / limited | question = Unknown
>
> **Note**: Marfret has no public API. All assessments below are based on what is visible through the web portal Track & Trace, INTTRA integration, and third-party aggregator capabilities.

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ❌ | N/A | N/A | N/A | No API. Schedules visible on website but not programmatically accessible. Available via aggregators (project44) |
| 1.2 | Point-to-Point Route Options | ❌ | N/A | N/A | N/A | No API. Route finder available on website only |
| 1.3 | Booking Lifecycle | ⚠️ | INTTRA platform | INTTRA EDI (IFTMIN) | N/A | Booking via INTTRA only. No direct REST API for booking |
| 1.4 | Shipping Instructions | ⚠️ | INTTRA platform | INTTRA EDI (IFTMIN) | N/A | Likely available via INTTRA EDI. Not confirmed for REST/API access |
| 1.5 | Rates | ❌ | N/A | N/A | N/A | No rate API. Rates likely handled via direct sales/contracts |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❓ | N/A | Unknown | `ECP` | No API. May be communicated via booking confirmation or INTTRA |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❓ | N/A | Unknown | `EFC` | No API. May be communicated via booking confirmation or INTTRA |
| 2.3 | Documentation Cutoff | DCO | ❓ | N/A | Unknown | `DCO` | No API. Likely communicated in booking confirmation documents |
| 2.4 | VGM Cutoff | VCO | ❓ | N/A | Unknown | `VCO` | No API. SOLAS-mandated, so must be communicated somehow |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ❓ | N/A | Unknown | `FCO` | No API. Likely in booking confirmation or schedule documents |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❓ | N/A | Unknown | `LCO` | No API. Conditional on LCL shipments |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ❓ | N/A | Unknown | Inferred from first EquipmentEvent | No API. Unknown if visible on web portal |
| 3.2 | Empty Container Gate-Out (Pickup) | ❓ | N/A | Unknown | `GTOT` + `EMPTY` | No API. May be available via aggregators (Vizion, project44) |
| 3.3 | Full Container Gate-In | ❓ | N/A | Unknown | `GTIN` + `LADEN` | No API. May be available via aggregators |
| 3.4 | Container Loaded on Vessel | ⚠️ | Web portal Track & Trace | Unknown | `LOAD` + `LADEN` | Likely visible on web portal tracking. Available via aggregators |
| 3.5 | Container Discharged at Transshipment | ❓ | N/A | Unknown | `DISC` + `LADEN` + transshipment | No API. Transshipment visibility unknown |
| 3.6 | Container Loaded at Transshipment | ❓ | N/A | Unknown | `LOAD` + `LADEN` + transshipment | No API. Transshipment visibility unknown |
| 3.7 | Container Discharged at Destination | ⚠️ | Web portal Track & Trace | Unknown | `DISC` + `LADEN` | Likely visible on web portal tracking. Available via aggregators |
| 3.8 | Full Container Gate-Out (Delivery) | ❓ | N/A | Unknown | `GTOT` + `LADEN` | No API. May be available via aggregators |
| 3.9 | Empty Container Returned | ❓ | N/A | Unknown | `GTIN` + `EMPTY` | No API. May be available via aggregators |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ⚠️ | Web portal Track & Trace | Unknown | `DEPA` + classifier | Likely visible on web portal. Available via aggregators |
| 4.2 | Estimated Time of Arrival | ETA | ⚠️ | Web portal Track & Trace | Unknown | `ARRI` + classifier | Likely visible on web portal. Available via aggregators |
| 4.3 | Vessel Arrival at Transshipment | -- | ❓ | N/A | Unknown | `ARRI` at intermediate | No API. Transshipment detail unknown |
| 4.4 | Vessel Departure from Transshipment | -- | ❓ | N/A | Unknown | `DEPA` at intermediate | No API. Transshipment detail unknown |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❌ | No API, no webhook capability |
| Event Polling with timestamp filter | ❌ | No API to poll |
| Event Classifier Progression (PLN->EST->ACT) | ❌ | No API, no classifier system |
| Retracted Events | ❌ | No API |
| Change Remarks | ❌ | No API |
| Delay Reason Codes | ❌ | No API |

### Coverage Summary

| Category | Fields Available | Fields Partial | Fields Unavailable | Fields Unknown | Coverage % |
|----------|-----------------|---------------|-------------------|----------------|-----------|
| API Domains (1.x) | 0/5 | 2/5 | 3/5 | 0/5 | 0% (2 partial via INTTRA) |
| Cutoffs (2.x) | 0/6 | 0/6 | 0/6 | 6/6 | 0% (all unknown) |
| Container Milestones (3.x) | 0/9 | 2/9 | 0/9 | 7/9 | 0% (2 partial via portal) |
| Transport Events (4.x) | 0/4 | 2/4 | 0/4 | 2/4 | 0% (2 partial via portal) |
| Change Detection (5.x) | 0/6 | 0/6 | 6/6 | 0/6 | 0% |
| **Total** | **0/30** | **6/30** | **9/30** | **15/30** | **0% confirmed (20% partial, 50% unknown)** |

> **Notes on Coverage:**
> - Marfret has no public API whatsoever. Zero fields are available via direct programmatic access.
> - The 6 "partial" fields reflect data that is likely visible on the web portal or available through INTTRA EDI, but not via a REST API.
> - The 15 "unknown" fields reflect data that Marfret likely communicates to customers through booking confirmations, shipping documents, or the web portal, but cannot be confirmed from desk research.
> - Third-party aggregators (project44, Vizion) can provide tracking data for Marfret containers, effectively raising the practical coverage for tracking and transport events. Via aggregators, container milestones and ETD/ETA data would likely reach 50-70% coverage.
> - For booking and cutoff data, INTTRA EDI is the only electronic channel confirmed.

---

## Endpoint Reference

Marfret does not expose any public REST API endpoints. This section is intentionally empty.

### Lookup Methods Summary

| Identifier Type | Supported? | Which Endpoints? | Notes |
|----------------|-----------|-----------------|-------|
| **Bill of Lading (B/L) number** | N/A (no API) | Web portal only | Available on Track & Trace web page and via aggregators |
| **Booking reference** | N/A (no API) | INTTRA EDI only | Booking via INTTRA platform |
| **Container number** | N/A (no API) | Web portal only | Track & Trace page accepts container numbers (e.g., MFTU1234567) |
| **Carrier booking number** | N/A (no API) | Unknown | |
| **Vessel IMO / voyage** | N/A (no API) | N/A | |

---

## Rate Limits & Quotas

N/A -- Marfret has no public API.

---

## Webhook / Push Support

Marfret does not offer webhooks or push notifications.

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | https://www.marfret.com/en/container-tracking/ |
| **Login required?** | No -- basic tracking appears available without login |
| **Data available on portal but NOT in API** | All tracking data is portal-only since there is no API. Container location, vessel, voyage, ETD/ETA, and milestone statuses likely visible |
| **Scraping feasibility** | Not assessed -- web portal is a simple form-based interface. Terms of service should be reviewed before considering scraping |

### Customer Portal

| Detail | Value |
|--------|-------|
| **Portal URL** | https://marfret.locussoftware.com/customer-portal |
| **Platform** | Locus Software (third-party logistics portal platform) |
| **Capabilities** | Account management, booking dashboard, document access |
| **Login required?** | Yes |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Yes (via INTTRA / e2open) |
| **EDI message types** | Booking via INTTRA confirmed. Likely supports IFTMIN (Shipping Instructions), COPARN, IFTSTA (Tracking status) -- not all individually confirmed |
| **EDI connection method** | Via INTTRA / e2open platform |
| **EDI documentation** | Contact Marfret agency or INTTRA. No public EDI documentation found |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Yes | Confirmed -- Marfret container tracking available via project44 Movement platform. B/L and container number lookup. Source: https://www.project44.com/tracking/container/marfret/ |
| **FourKites** | Unknown | Not explicitly confirmed for Marfret |
| **Vizion** | Yes | Confirmed -- Marfret (MFTU) listed as supported carrier. Source: https://docs.vizionapi.com/docs/supported-carriers |
| **INTTRA / E2open** | Yes | Confirmed -- Marfret booking available on INTTRA platform. Source: Marfret website |
| **CargoSmart** | Unknown | Not explicitly confirmed for Marfret |
| **Portcast** | Yes | Marfret tracking available via Portcast. Source: https://www.portcast.io/carrier-coverage/marfret-compagnie-maritime-container-tracking |
| **ShipsGo** | Yes | Marfret tracking API available via ShipsGo. Source: https://shipsgo.com/ocean/carriers/marfret/container-tracking |
| **GoComet** | Yes | Marfret tracking available. Source: https://www.gocomet.com/online-container-tracking/carriers/marfret-compagnie-maritime |

> **Aggregator note:** Since Marfret has no direct API, third-party aggregators are the only viable path for programmatic tracking data. project44 and Vizion both confirm Marfret support and would provide normalized, API-accessible tracking data. For booking operations, INTTRA EDI is the only confirmed electronic channel. The SDK architecture for Marfret should be aggregator-first rather than direct integration.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown -- no API to measure. Aggregators (Vizion) claim 6-hour or less latency for their data sources | Estimated |
| **API uptime/reliability** | N/A -- no API | N/A |
| **Historical data depth** | Unknown | Unknown |
| **Timezone handling** | Unknown -- likely CET/CEST given Marseille headquarters | Estimated |
| **Character encoding** | Unknown | Unknown |

### Known Issues & Gotchas

- **No API at all**: Marfret is a small regional carrier (~45,000 TEUs/year) with no public API. All programmatic access must go through third-party aggregators or EDI via INTTRA.

- **Limited digital maturity**: The customer portal is powered by Locus Software (a third-party logistics platform), and the internal system "Marius" is proprietary. This suggests limited in-house technology development capability.

- **Small fleet, niche routes**: Marfret operates primarily on French Caribbean, Central/South American, and Mediterranean routes. Tracking data availability through aggregators may be less complete for niche port calls compared to major carriers.

- **INTTRA dependency for booking**: Electronic booking is only available through INTTRA. Direct API booking is not possible.

- **French-language bias**: As a French company serving primarily French overseas territories, some documentation and communications may be primarily in French.

### Recently Deprecated or Changed

- No deprecation notices found. No API has ever been published.

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | Partial -- tracking only, via aggregator (project44 or Vizion). No direct booking, schedule, or cutoff API |
| **Implementation effort** | Low (aggregator passthrough) for tracking; N/A for other domains |
| **DCSA base adapter usable?** | No -- Marfret is not DCSA-compliant. However, aggregators like Vizion normalize data into a standard format that could be mapped |

### Recommended Approach

The Marfret adapter should be built as an **aggregator-mediated integration** rather than a direct carrier integration. There are two recommended paths:

1. **Primary -- Vizion API**: Use Vizion's container tracking API with carrier code "MFTU". Vizion normalizes tracking events into a standard format and supports webhook-based push notifications. This provides the best data coverage for container milestones and transport events without needing to interact with Marfret's systems directly.

2. **Alternative -- project44**: Use project44's Movement platform for Marfret container tracking. project44 also supports B/L and container number lookups with normalized data.

For booking operations, the only electronic channel is INTTRA EDI. If SSL needs booking capability for Marfret, an INTTRA/e2open integration would be required separately from the tracking adapter.

There is no path to direct rate, schedule, or cutoff API access. These would need to be handled through manual processes or by checking if aggregators provide derived schedule data.

### Recommended Lookup Method

**Container number** is the recommended primary lookup when using aggregators, as it is the most universal identifier supported across all aggregator platforms.

**Bill of Lading (B/L) number** as secondary -- supported by both project44 and Vizion.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Dependent on aggregator -- Vizion uses webhook push (event-driven, no polling needed). project44 supports both polling and push. If polling, every 6-12 hours is sufficient for a regional carrier with moderate transit times |
| **Incremental filter** | Aggregator-dependent -- Vizion pushes only new events. project44 supports incremental queries |
| **Batch tracking** | Aggregator-dependent -- both Vizion and project44 support multi-container subscriptions |

### Auth Implementation Notes

No Marfret-specific auth is needed. The adapter authenticates with the chosen aggregator's API:
- **Vizion**: API key-based authentication
- **project44**: OAuth2 / API key authentication

### Edge Cases to Handle

- **Limited port coverage**: Marfret serves niche routes (French Caribbean, Guyana, North Brazil). Aggregator data for smaller ports may have longer latency or missing events compared to major trade lanes.

- **Transshipment complexity**: Marfret operates feeder services (INTRACAR) connecting to its mainline routes. Containers may transfer between Marfret vessels, which could create complex tracking chains.

- **Mixed fleet types**: Marfret operates container, RoRo, and multipurpose vessels. The adapter should handle the possibility that tracking data format may differ based on vessel/cargo type.

- **Aggregator data gaps**: Since aggregators scrape or receive data indirectly, some Marfret-specific milestones (especially at smaller Caribbean ports) may be missing or delayed.

### Mapping Complexity

**Low complexity** when using an aggregator. Both Vizion and project44 normalize carrier data into standardized formats. The adapter would map from the aggregator's schema to SSL's canonical data model rather than dealing with Marfret's proprietary data directly.

If INTTRA EDI is used for booking, mapping complexity increases to **medium** due to EDIFACT message parsing requirements.

---

## Open Questions

- [ ] Does Marfret have any private/partner API that is not publicly documented? -- Contact Marfret directly to inquire
- [ ] What specific EDI message types does Marfret support via INTTRA? -- Only booking is confirmed; SI, tracking status, and VGM support need verification
- [ ] Does Marfret's customer portal (Locus Software) expose any API? -- The Locus Software platform may have API capabilities not visible from desk research
- [ ] What tracking events are available through aggregators for Marfret specifically? -- Test with Vizion and project44 using actual Marfret container numbers
- [ ] Does Marfret provide cutoff data electronically via INTTRA or in booking confirmations? -- Critical for DCO/VCO/FCO fields
- [ ] Does SSL have an existing INTTRA/e2open account? -- Required for booking integration
- [ ] What is the data freshness of Marfret tracking data through Vizion/project44? -- Niche carrier data may have higher latency
- [ ] Is Marfret considering any future API development or DCSA adoption? -- Company direction for digital capabilities

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | https://www.marfret.com |
| Container Tracking (Web) | https://www.marfret.com/en/container-tracking/ |
| Customer Portal | https://marfret.locussoftware.com/customer-portal |
| Contact Page | https://www.marfret.com/en/contact-us/ |
| Container Liner Shipping | https://www.marfret.com/en/solutions/container-liner-shipping/ |
| Ships & Fleet | https://www.marfret.com/en/our-company/ships/ |
| INTTRA Platform | https://my.inttra.e2open.com/ |
| project44 Marfret Tracking | https://www.project44.com/tracking/container/marfret/ |
| Vizion Supported Carriers | https://docs.vizionapi.com/docs/supported-carriers |
| Portcast Marfret Coverage | https://www.portcast.io/carrier-coverage/marfret-compagnie-maritime-container-tracking |
| ShipsGo Marfret Tracking | https://shipsgo.com/ocean/carriers/marfret/container-tracking |
| Fluent Cargo (SCAC reference) | https://www.fluentcargo.com/carriers/scac/MFTU |
| Routescanner Marfret Schedules | https://www.routescanner.com/partners/Marfret |
