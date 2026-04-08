# SeaLead Shipping -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing
> **Researched by**: Agent
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | SeaLead Shipping Pte Ltd (commonly "SeaLead") |
| **SCAC Code** | SJHH (Sea Lead Shipping Pte Ltd); also SQQY (SeaLead Shipping DMCC, Dubai entity) |
| **Parent Company** | Privately held; no public parent company |
| **Alliance** | Independent (not a member of any shipping alliance) |
| **Primary Services** | Container shipping and liner services; feeder and long-haul routes |
| **Market Position** | 13th-largest container carrier globally (Alphaliner, 2024); fast-growing independent focused on emerging markets and secondary ports |
| **Headquarters** | Singapore (new HQ opened 2024; additional offices in Seoul, Dubai, Gandhidham) |
| **Website** | https://www.sea-lead.com/ |

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | No |
| **Developer portal URL** | N/A |
| **API documentation URL(s)** | N/A -- no public API documentation found |
| **Documentation quality** | None -- no developer-facing documentation exists |
| **OpenAPI/Swagger spec available?** | No |
| **Sandbox/test environment?** | No / Unknown |
| **Developer registration** | N/A -- no API access program exists |
| **Developer support channels** | General customer support via website contact forms and email |
| **Community/third-party libraries** | None found. Third-party aggregators (ShipsGo, Portcast, Terminal49, GoComet) provide tracking APIs that cover SeaLead |
| **API changelog / release notes** | N/A |

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | No -- SeaLead is not a DCSA member. DCSA members are the 10 largest carriers (MSC, Maersk, CMA CGM, Hapag-Lloyd, ONE, Evergreen, Yang Ming, HMM, ZIM, and COSCO as of 2025) |
| **DCSA APIs implemented** | None |
| **DCSA TNT version** | N/A |
| **DCSA Booking version** | N/A |
| **DCSA Schedules version** | N/A |
| **Known DCSA deviations** | N/A -- SeaLead does not implement DCSA APIs |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Unknown | No public information about EDI capabilities found. Given their size (13th globally), some EDI support is likely but unconfirmed |
| **INTTRA integration** | Unknown | No evidence of INTTRA/E2open partnership found |
| **BIC (Bureau International des Containers)** | Yes | Standard BIC container ID format used in tracking (inferred from B/L prefix SLKB/SLS format) |
| **UN/LOCODE** | Unknown | Port codes used in their route search and schedule tools; format not confirmed |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | N/A -- no public API |
| **Auth documentation** | N/A |
| **Registration process** | N/A -- no API access program; customer portal registration available at customer.sea-lead.com |
| **Registration URL** | https://customer.sea-lead.com (customer portal, not API access) |
| **Partner program required?** | N/A |
| **Partner program URL** | N/A |
| **Credential type** | N/A |
| **Token refresh supported?** | N/A |
| **Token lifetime** | N/A |
| **Access tiers** | N/A |
| **IP whitelisting required?** | N/A |

### Access Requirements Summary for SSL

SeaLead does not offer a public API or developer portal. There is no documented way to programmatically access tracking, scheduling, or booking data directly from SeaLead. The company provides a customer portal (customer.sea-lead.com) and a web-based tracking page (sea-lead.com/track-shipment/) that accepts B/L numbers (prefix SLKB or SLS followed by 8-12 alphanumeric characters), booking reference numbers, and container numbers. However, these are web interfaces without published API endpoints.

For programmatic access to SeaLead tracking data, SSL would need to use third-party aggregators such as Terminal49 (which lists SeaLead under SCAC code SQQY), Portcast, ShipsGo, or GoComet. Alternatively, SSL could approach SeaLead directly about potential API partnerships, though given the carrier's relatively young age (founded 2017) and focus on rapid growth, a formal API program may not yet be a priority.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field has a row.
> Availability legend: check = Available | x = Not available | warning = Partial / limited | question = Unknown

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ❌ | N/A (no API) | N/A | N/A | SeaLead offers a web-based route search tool but no programmatic schedule API. Schedule data available via RouteScanner partnership |
| 1.2 | Point-to-Point Route Options | ❌ | N/A (no API) | N/A | N/A | Web-based route search available on sea-lead.com but no API |
| 1.3 | Booking Lifecycle | ❌ | N/A (no API) | N/A | N/A | Booking available through customer portal (customer.sea-lead.com) and "Request a Quote" web form; no API |
| 1.4 | Shipping Instructions | ❌ | N/A (no API) | N/A | N/A | Likely handled through customer portal or email; no API |
| 1.5 | Rates | ❌ | N/A (no API) | N/A | N/A | Quote requests via web form; no programmatic rate access |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❌ | N/A | N/A | `ECP` | No API; cutoff data not programmatically accessible |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❌ | N/A | N/A | `EFC` | No API |
| 2.3 | Documentation Cutoff | DCO | ❌ | N/A | N/A | `DCO` | No API |
| 2.4 | VGM Cutoff | VCO | ❌ | N/A | N/A | `VCO` | No API |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ❌ | N/A | N/A | `FCO` | No API |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❌ | N/A | N/A | `LCO` | No API |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ❌ | N/A | N/A | Inferred from first EquipmentEvent | No API |
| 3.2 | Empty Container Gate-Out (Pickup) | ❌ | N/A | N/A | `GTOT` + `EMPTY` | No direct API. Terminal49 reports "empty out" milestone available via aggregator |
| 3.3 | Full Container Gate-In | ❌ | N/A | N/A | `GTIN` + `LADEN` | No direct API. Terminal49 reports "full in" milestone available via aggregator |
| 3.4 | Container Loaded on Vessel | ❌ | N/A | N/A | `LOAD` + `LADEN` | No direct API. Terminal49 reports vessel loading milestone available via aggregator |
| 3.5 | Container Discharged at Transshipment | ❌ | N/A | N/A | `DISC` + `LADEN` + transshipment | No direct API. Terminal49 reports transshipment events available via aggregator |
| 3.6 | Container Loaded at Transshipment | ❌ | N/A | N/A | `LOAD` + `LADEN` + transshipment | No direct API. Terminal49 reports transshipment events available via aggregator |
| 3.7 | Container Discharged at Destination | ❌ | N/A | N/A | `DISC` + `LADEN` | No direct API. Terminal49 reports vessel discharge milestone available via aggregator |
| 3.8 | Full Container Gate-Out (Delivery) | ❌ | N/A | N/A | `GTOT` + `LADEN` | No direct API. Terminal49 reports "full out" milestone available via aggregator |
| 3.9 | Empty Container Returned | ❌ | N/A | N/A | `GTIN` + `EMPTY` | No direct API |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ❌ | N/A | N/A | `DEPA` + classifier | No direct API. Available via aggregators (Terminal49, Portcast) |
| 4.2 | Estimated Time of Arrival | ETA | ❌ | N/A | N/A | `ARRI` + classifier | No direct API. Available via aggregators (Terminal49, Portcast with predictive AI ETA) |
| 4.3 | Vessel Arrival at Transshipment | -- | ❌ | N/A | N/A | `ARRI` at intermediate | No direct API |
| 4.4 | Vessel Departure from Transshipment | -- | ❌ | N/A | N/A | `DEPA` at intermediate | No direct API |

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
| Container Milestones (3.x) | 0/9 | 9/9 | 0/9 | 0% |
| Transport Events (4.x) | 0/4 | 4/4 | 0/4 | 0% |
| Change Detection (5.x) | 0/6 | 6/6 | 0/6 | 0% |
| **Total** | **0/30** | **30/30** | **0/30** | **0%** |

> **Notes on Coverage:**
> - SeaLead has zero direct API coverage. The carrier does not expose any public APIs for tracking, scheduling, booking, or any other domain.
> - However, several third-party aggregators (Terminal49, Portcast, ShipsGo, GoComet) provide tracking data for SeaLead shipments. Terminal49 specifically reports availability of: empty out, full in, vessel load/discharge, transshipment events, full out milestones, plus ETD/ETA data.
> - Through aggregators, effective tracking coverage is significantly higher than 0%, but this is not direct carrier API access.
> - SeaLead's web tracking portal (sea-lead.com/track-shipment/) provides container status, routes, and delivery timelines, indicating the underlying data exists -- it is simply not exposed via API.

---

## Endpoint Reference

SeaLead does not offer any public API endpoints. This section is not applicable.

### Lookup Methods Summary

| Identifier Type | Supported? | Which Endpoints? | Notes |
|----------------|-----------|-----------------|-------|
| **Bill of Lading (B/L) number** | Web only | sea-lead.com/track-shipment/ | B/L prefix: SLKB or SLS + 8-12 alphanumeric characters |
| **Booking reference** | Web only | sea-lead.com/track-shipment/ | Available on web tracking portal |
| **Container number** | Web only | sea-lead.com/track-shipment/ | Available on web tracking portal |
| **Carrier booking number** | Unknown | N/A | |
| **Vessel IMO / voyage** | Unknown | N/A | |

---

## Rate Limits & Quotas

N/A -- SeaLead does not offer a public API.

---

## Webhook / Push Support

SeaLead does not support webhooks or push notifications. Customers can opt in for email notifications on shipment status through the tracking portal.

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | https://www.sea-lead.com/track-shipment/ |
| **Login required?** | No -- basic tracking available without login |
| **Data available on portal but NOT in API** | All data is portal-only since there is no API. Portal shows container status, routes, delivery timelines, and milestone events |
| **Scraping feasibility** | Not assessed. Portal is WordPress/Elementor-based. ToS should be reviewed before considering scraping. Aggregator integration strongly preferred |

### Customer Portal

| Detail | Value |
|--------|-------|
| **Portal URL** | https://customer.sea-lead.com |
| **Capabilities** | Digital shipping management, booking, tracking, documentation |
| **Login required?** | Yes |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Unknown |
| **EDI message types** | Unknown |
| **EDI connection method** | Unknown |
| **EDI documentation** | Unknown -- contact SeaLead directly |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Unknown | No explicit SeaLead confirmation found in search results |
| **FourKites** | Unknown | No explicit SeaLead confirmation found |
| **Vizion** | Unknown | Vizion claims 99% ocean freight coverage; SeaLead likely covered but not explicitly confirmed |
| **INTTRA / E2open** | Unknown | No partnership documentation found |
| **CargoSmart** | Unknown | No partnership documentation found |
| **Terminal49** | Yes | SeaLead tracked under SCAC code SQQY. Supports B/L and container number lookup. Milestones: empty out, full in, vessel load/discharge, transshipment, full out. ETD/ETA available. Booking number lookup NOT supported. Final destination/feeder/delivery not supported |
| **Portcast** | Yes | Provides real-time and predictive visibility for SeaLead. Supports container, booking, and B/L lookup. AI-based predictive ETAs |
| **ShipsGo** | Yes | Offers SeaLead tracking API with unlimited API calls. Container tracking data integration for ERP/CRM/TMS |
| **GoComet** | Yes | SeaLead container tracking and sailing schedule data available |
| **Tradlinx** | Yes | B/L and container tracking for SeaLead |
| **RouteScanner** | Yes | SeaLead listed as a partner; schedule/route data available |

> **Aggregator note:** Since SeaLead has no direct API, aggregator integration is the only viable path for programmatic tracking. Terminal49 offers the most detailed documented coverage with specific milestone data. ShipsGo offers an attractive unlimited-calls API model. Portcast adds predictive ETA capabilities. For SSL's SDK, integrating SeaLead via one of these aggregators (particularly Terminal49 or ShipsGo) is the recommended approach.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown -- dependent on aggregator data pipeline | Unknown |
| **API uptime/reliability** | N/A -- no direct API | N/A |
| **Historical data depth** | Unknown | Unknown |
| **Timezone handling** | Unknown | Unknown |
| **Character encoding** | Unknown | Unknown |

### Known Issues & Gotchas

- **No direct API exists**: This is the primary constraint. All programmatic integration must go through third-party aggregators.

- **Multiple SCAC codes**: SeaLead operates under at least three SCAC codes: SJHH (Sea Lead Shipping Pte Ltd, Singapore), SQQY (SeaLead Shipping DMCC, Dubai), and SEAL is sometimes attributed to SeaLead but is also used by Seaboard Marine (which has SEAL in the carrier index). Different aggregators use different codes (Terminal49 uses SQQY, Panjiva lists both SJHH and SQQY).

- **Young carrier with evolving digital capabilities**: Founded in 2017, SeaLead has been growing rapidly (13th globally by 2024) and investing in digital capabilities (customer portal, "innovative IT solutions"). An API program may emerge in the future, but none exists today.

- **B/L number format**: SeaLead B/L numbers use prefix SLKB or SLS followed by 8-12 alphanumeric characters. This is important for tracking lookups via aggregators.

- **Aggregator data gaps**: Terminal49 notes that booking number lookup, final destination info, feeder/rail operations, and delivery confirmations are not available for SeaLead.

### Recently Deprecated or Changed

- No deprecation notices applicable -- no API has ever been published.

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | Partial -- only via aggregator. No direct carrier integration possible due to absence of API |
| **Implementation effort** | Very High (no API) -- requires aggregator subscription and integration rather than direct carrier API work |
| **DCSA base adapter usable?** | No -- SeaLead does not implement DCSA. If using an aggregator, the aggregator's normalized format would be the integration target |

### Recommended Approach

SeaLead cannot be integrated directly into the SDK because the carrier offers no public API. The recommended approach is to integrate SeaLead tracking through a third-party aggregator:

1. **Primary option -- Terminal49 or ShipsGo**: Both provide documented SeaLead tracking APIs. Terminal49 offers specific milestone data (empty out, full in, vessel load/discharge, transshipment, full out, ETD/ETA). ShipsGo offers unlimited API calls. The adapter would target the aggregator's API rather than a carrier-specific API.

2. **Alternative -- Portcast**: If predictive ETA capabilities are valued, Portcast provides AI-enhanced arrival predictions for SeaLead shipments in addition to real-time tracking.

3. **Architecture impact**: The SeaLead adapter would be an "aggregator adapter" rather than a "carrier adapter." This implies the SDK architecture should support aggregator-backed adapters as a first-class pattern, since SeaLead is unlikely to be the only carrier without a direct API.

If SSL has enough SeaLead volume to justify direct outreach, contacting SeaLead about potential API partnership could be worthwhile. The carrier's emphasis on "innovative IT solutions" and rapid growth suggests they may be open to API partnerships even if no public program exists yet.

### Recommended Lookup Method

**B/L number** is the primary recommended lookup method, using the SLKB or SLS prefix format. Container number is a secondary option. Booking number lookup is not supported by Terminal49 for SeaLead, so B/L or container is preferred.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Dependent on aggregator rate limits and data freshness. Typical aggregator polling: every 2-4 hours for active shipments |
| **Incremental filter** | Dependent on aggregator capabilities (most support timestamp-based filtering) |
| **Batch tracking** | Dependent on aggregator -- Terminal49 supports batch container tracking; ShipsGo supports bulk tracking |

### Auth Implementation Notes

No carrier-specific auth is needed. Authentication would be against the chosen aggregator's API (typically API key-based for Terminal49, ShipsGo, Portcast, etc.).

### Edge Cases to Handle

- **Multiple SCAC codes**: Ensure the adapter maps SJHH, SQQY, and any other SeaLead SCAC variants to a single carrier identity in the SDK.

- **Aggregator data latency**: Data from SeaLead may have additional latency compared to carriers with direct APIs, as it passes through the aggregator's data pipeline first.

- **Limited milestone coverage**: Some milestones (booking assignment, empty container return, final delivery) may not be available even through aggregators.

- **B/L prefix validation**: Validate that B/L numbers start with SLKB or SLS to ensure they are SeaLead bills before routing to the aggregator.

### Mapping Complexity

**Low complexity (via aggregator).** If integrating through an aggregator like Terminal49 or ShipsGo, the mapping work shifts to the aggregator's normalized data format rather than SeaLead's proprietary format. The aggregator handles the complexity of extracting and normalizing data from SeaLead's web portal or internal systems. The SDK adapter would map from the aggregator's schema to SSL's canonical model, which is a simpler transformation than mapping from a proprietary carrier API.

---

## Open Questions

- [ ] Does SSL have an existing business relationship with SeaLead? -- Could facilitate discussions about direct API access
- [ ] Which aggregator does SSL already use or prefer? -- Terminal49, ShipsGo, Portcast, and others all cover SeaLead
- [ ] Does SeaLead have any unpublished API or partner API program? -- Direct outreach to SeaLead would clarify
- [ ] What is SeaLead's EDI capability? -- May support EDI for larger customers even without a public API
- [ ] Is SeaLead considering DCSA membership or API development? -- Given their rapid growth and digital investment, this may be on their roadmap
- [ ] What is the data freshness and accuracy of aggregator tracking data for SeaLead? -- Varies by aggregator; testing needed
- [ ] Which SCAC code should SSL use as the canonical identifier for SeaLead? -- SJHH (Singapore entity) appears to be the primary code

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | https://www.sea-lead.com/ |
| About Page | https://www.sea-lead.com/about/ |
| Tracking Portal | https://www.sea-lead.com/track-shipment/ |
| Solutions Page | https://www.sea-lead.com/solutions/ |
| Support/FAQ | https://www.sea-lead.com/support/ |
| Customer Portal | https://customer.sea-lead.com |
| Route Services | https://www.sea-lead.com/services/ |
| 2024 Journey / 2025 Vision | https://www.sea-lead.com/2024-journey/ |
| RouteScanner Partnership | https://www.routescanner.com/partners/SeaLead |
| Terminal49 SeaLead Tracking | https://terminal49.com/shipping-lines/sqqy-sealead-container-tracking |
| Portcast SeaLead Tracking | https://www.portcast.io/carrier-coverage/sealead-container-tracking |
| ShipsGo SeaLead Tracking | https://shipsgo.com/ocean/carriers/sealead/container-tracking |
| GoComet SeaLead Tracking | https://www.gocomet.com/online-container-tracking/carriers/sea-lead |
| Panjiva SJHH Profile | https://panjiva.com/scac_profiles/profile/SJHH |
| Panjiva SQQY Profile | https://panjiva.com/scac_profiles/profile/SQQY |
| SeaBayCargo SEAL Entry | https://www.seabaycargo.com/shipping-company/details/SeaLead |
| Beacon SCAC List | https://www.beacon.com/resources/ocean-carrier-scac-codes-list |
| JAXPORT Press Release | https://www.jaxport.com/global-shipping-line-sea-lead-brings-first-u-s-east-coast-container-service-to-jaxport/ |
