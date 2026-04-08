# Great White Fleet -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing
> **Researched by**: Agent
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | Great White Fleet Ltd. (commonly "Great White Fleet" or "GWF") |
| **SCAC Code** | UBCU |
| **Parent Company** | Chiquita Brands International |
| **Alliance** | Independent (space charter agreement with MSC since 2014) |
| **Primary Services** | Refrigerated (reefer) container shipping, dry cargo, project cargo, automotive cargo |
| **Market Position** | Niche/regional specialist -- Central America to U.S. East/Gulf Coast and Europe. Ranked ~53rd globally. Premier refrigerated goods carrier connecting Central America, U.S., and Europe |
| **Headquarters** | Fort Lauderdale, FL, USA (Chiquita HQ); operational offices in Dania Beach, FL and Panama |
| **Website** | https://greatwhitefleet.com |

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
| **Developer support channels** | General contact only: gwf@greatwhitefleet.com, 1-888-724-5493 |
| **Community/third-party libraries** | None found. Third-party aggregator tracking sites (e-tracking.net, MyContainerTracking.com) offer GWF container tracking by scraping or data feeds |
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
| **Known DCSA deviations** | N/A -- GWF does not implement any DCSA APIs |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Unknown | No published information on EDI capabilities. Possible via MSC space charter partner or INTTRA, but not confirmed |
| **INTTRA integration** | Unknown | No confirmed INTTRA partnership found in research |
| **BIC (Bureau International des Containers)** | Yes | Standard container ID format used (tracking by container number supported) |
| **UN/LOCODE** | Unknown | Port codes used in their SolverMinds e-commerce platform, but UN/LOCODE compliance not confirmed |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | N/A (no public API) |
| **Auth documentation** | N/A |
| **Registration process** | N/A -- GWF customer portal (gwfonline.solverminds.net) requires account registration, but this is a web portal, not an API |
| **Registration URL** | https://gwfonline.solverminds.net/ecomonline/ (web portal only) |
| **Partner program required?** | N/A |
| **Partner program URL** | N/A |
| **Credential type** | N/A |
| **Token refresh supported?** | N/A |
| **Token lifetime** | N/A |
| **Access tiers** | N/A |
| **IP whitelisting required?** | N/A |

### Access Requirements Summary for SSL

Great White Fleet does not offer any public API or developer portal. Programmatic access to GWF data is not available through direct integration. The carrier operates a web-based customer portal powered by SolverMinds (gwfonline.solverminds.net) that provides schedule search, container tracking, and rate inquiries -- but only via a browser-based interface requiring login credentials and CAPTCHA verification.

SSL would need to either (a) negotiate a custom data exchange agreement with GWF directly (likely EDI-based given the carrier's size), (b) use a third-party aggregator that covers GWF, or (c) explore web scraping of the GWF portal (subject to ToS and technical feasibility). Given GWF's niche market position and parent company (Chiquita), a direct partnership approach via Chiquita's logistics team may be the most viable path.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field has a row.
> Availability legend: check = Available | x = Not available | warning = Partial / limited | question = Unknown

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ❌ | N/A (portal only) | Schedule search via web portal | N/A | SolverMinds web portal offers schedule search by origin/destination/date, but no API endpoint |
| 1.2 | Point-to-Point Route Options | ❌ | N/A (portal only) | Route options via web portal | N/A | Web portal supports origin-destination schedule queries, but no API |
| 1.3 | Booking Lifecycle | ❌ | N/A | N/A | N/A | Booking presumably handled via email/phone/portal. "Request a Quote" form on website |
| 1.4 | Shipping Instructions | ❌ | N/A | N/A | N/A | No electronic SI submission capability found |
| 1.5 | Rates | ❌ | N/A (portal only) | Rate inquiry via web portal | N/A | SolverMinds portal allows rate inquiries by equipment type and port pair, but no API |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❌ | N/A | N/A | `ECP` | No API access to cutoff data |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❌ | N/A | N/A | `EFC` | No API access to cutoff data |
| 2.3 | Documentation Cutoff | DCO | ❌ | N/A | N/A | `DCO` | No API access to cutoff data |
| 2.4 | VGM Cutoff | VCO | ❌ | N/A | N/A | `VCO` | No API access to cutoff data |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ❌ | N/A | N/A | `FCO` | No API access to cutoff data |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❌ | N/A | N/A | `LCO` | No API access to cutoff data |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ❌ | N/A | N/A | Inferred from first EquipmentEvent | No API access |
| 3.2 | Empty Container Gate-Out (Pickup) | ❌ | N/A | N/A | `GTOT` + `EMPTY` | No API access. Portal tracking may show this milestone |
| 3.3 | Full Container Gate-In | ❌ | N/A | N/A | `GTIN` + `LADEN` | No API access |
| 3.4 | Container Loaded on Vessel | ❌ | N/A | N/A | `LOAD` + `LADEN` | No API access |
| 3.5 | Container Discharged at Transshipment | ❌ | N/A | N/A | `DISC` + `LADEN` + transshipment | No API access |
| 3.6 | Container Loaded at Transshipment | ❌ | N/A | N/A | `LOAD` + `LADEN` + transshipment | No API access |
| 3.7 | Container Discharged at Destination | ❌ | N/A | N/A | `DISC` + `LADEN` | No API access |
| 3.8 | Full Container Gate-Out (Delivery) | ❌ | N/A | N/A | `GTOT` + `LADEN` | No API access |
| 3.9 | Empty Container Returned | ❌ | N/A | N/A | `GTIN` + `EMPTY` | No API access |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ❌ | N/A | N/A | `DEPA` + classifier | No API access. Portal and third-party sites show schedule ETDs |
| 4.2 | Estimated Time of Arrival | ETA | ❌ | N/A | N/A | `ARRI` + classifier | No API access |
| 4.3 | Vessel Arrival at Transshipment | -- | ❌ | N/A | N/A | `ARRI` at intermediate | No API access |
| 4.4 | Vessel Departure from Transshipment | -- | ❌ | N/A | N/A | `DEPA` at intermediate | No API access |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❌ | No webhook/push capability |
| Event Polling with timestamp filter | ❌ | No API to poll |
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
> - Great White Fleet has zero API-accessible data. All coverage is 0% from a programmatic integration standpoint.
> - The SolverMinds-powered web portal (gwfonline.solverminds.net) does offer schedule search, container tracking, and rate inquiries via browser, suggesting the underlying data exists -- but is not exposed through any API.
> - Third-party tracking aggregator sites (e-tracking.net, MyContainerTracking.com) claim to offer GWF container tracking, which suggests data may be accessible through aggregator partnerships or web scraping.
> - The MSC space charter agreement means some GWF cargo may be trackable through MSC's systems for shipments on MSC-operated vessels.

---

## Endpoint Reference

Great White Fleet does not expose any public API endpoints. This section is intentionally omitted.

---

## Rate Limits & Quotas

| Detail | Value | Source |
|--------|-------|--------|
| **Global rate limit** | N/A | N/A |
| **Per-endpoint limits** | N/A | N/A |
| **Daily/monthly quota** | N/A | N/A |
| **Rate limit response** | N/A | N/A |
| **Rate limit by** | N/A | N/A |
| **Burst allowance** | N/A | N/A |
| **Different tiers** | N/A | N/A |

No API available; rate limits not applicable.

---

## Webhook / Push Support

| Detail | Value |
|--------|-------|
| **Webhooks supported?** | No |
| **Subscription endpoint** | N/A |
| **Subscription management** | N/A |
| **Subscribable event types** | N/A |
| **Callback format** | N/A |
| **Callback authentication** | N/A |
| **Retry policy on failure** | N/A |
| **Documented reliability** | N/A |

No webhook or push notification support available.

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | https://gwfonline.solverminds.net/ecomonline/ (requires login + CAPTCHA) |
| **Login required?** | Yes -- customer account required |
| **Data available on portal but NOT in API** | All data -- schedules, tracking, rates, bills of lading are portal-only. No API exists |
| **Scraping feasibility** | Difficult -- CAPTCHA verification required for tracking; login required for all features. SolverMinds platform may have anti-bot protections. ToS assessment needed |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Unknown |
| **EDI message types** | Unknown |
| **EDI connection method** | Unknown -- may be available through MSC partnership or direct arrangement with Chiquita |
| **EDI documentation** | Contact carrier (gwf@greatwhitefleet.com) |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Unknown | GWF/UBCU not found in project44's published carrier lists. Given GWF's niche size, coverage is unlikely |
| **FourKites** | Unknown | No confirmed coverage found |
| **Vizion** | Unknown | No confirmed coverage found. Vizion claims 99% ocean freight coverage; GWF may or may not be included given its small market share |
| **INTTRA / E2open** | Unknown | No confirmed partnership. INTTRA covers 70+ carriers; GWF status unknown |
| **CargoSmart** | Unknown | No confirmed coverage found |
| **Fluent Cargo** | Yes | Fluent Cargo lists GWF sailing schedules under SCAC UBCU. Likely sourced from public schedule data |
| **e-tracking.net** | Yes | Offers GWF container tracking. Data source unclear -- likely scraping or data feed arrangement |

> **Aggregator note:** No confirmed aggregator coverage was found for Great White Fleet. The carrier's small market size (ranked ~53rd globally) and niche focus (Central America perishables) make aggregator coverage less likely than for top-20 carriers. Third-party tracking sites (e-tracking.net, MyContainerTracking.com) do claim GWF support, but the data source and reliability are unknown. For SSL, the most promising path may be direct negotiation with GWF/Chiquita for EDI access or exploring whether the MSC space charter agreement enables tracking through MSC's APIs.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown -- no API to assess | Unknown |
| **API uptime/reliability** | N/A -- no API | N/A |
| **Historical data depth** | Unknown | Unknown |
| **Timezone handling** | Unknown | Unknown |
| **Character encoding** | Unknown | Unknown |

### Known Issues & Gotchas

- **No API exists**: Great White Fleet has no public API, developer portal, or documented programmatic access method. All integration would require non-standard approaches (EDI negotiation, aggregator, or web scraping).

- **CAPTCHA on tracking portal**: The SolverMinds web portal requires CAPTCHA verification for tracking lookups, making automated scraping technically challenging.

- **Niche carrier with limited digital investment**: As a subsidiary of Chiquita focused on refrigerated cargo for the banana/produce trade, GWF's digital infrastructure is minimal. The SolverMinds portal is a basic commercial off-the-shelf solution.

- **MSC space charter complication**: Since 2014, GWF has a space charter agreement with MSC. Cargo on MSC-operated vessels may have tracking data available through MSC's APIs, but it would be under MSC's tracking system, not GWF's.

- **Chiquita ownership**: GWF is wholly owned by Chiquita Brands International. Any partnership or data exchange agreement would likely need to go through Chiquita's corporate channels.

- **Regional focus**: GWF serves a narrow set of routes (Central America to U.S. East/Gulf Coast, with some European service). The carrier is not relevant for Pacific, Asia, or broader global shipping lanes.

### Recently Deprecated or Changed

- No deprecation notices found. The SolverMinds portal appears to be GWF's current operational platform.

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | No -- GWF has no API. A direct adapter is not feasible without a custom data exchange agreement |
| **Implementation effort** | Very High (no API) -- would require EDI setup, web scraping with CAPTCHA bypass, or aggregator subscription |
| **DCSA base adapter usable?** | No -- GWF has no DCSA compliance and no API of any kind |

### Recommended Approach

Great White Fleet cannot be integrated via a standard API adapter. The recommended approach depends on SSL's business need for GWF data:

1. **If GWF tracking is low priority**: Skip direct integration. For the rare GWF shipment, manual tracking via the web portal (gwfonline.solverminds.net) or the main website (greatwhitefleet.com) is sufficient.

2. **If GWF tracking is needed at moderate volume**: Explore whether the MSC space charter agreement means GWF cargo can be tracked through MSC's DCSA-compliant API. If a shipment moves on an MSC vessel under the space charter, MSC's tracking system may have the data. This would allow using the existing MSC adapter for GWF shipments on shared vessels.

3. **If full GWF integration is required**: Contact GWF/Chiquita directly to negotiate EDI connectivity (likely IFTSTA for status messages). This would require a custom EDI adapter. Alternatively, investigate whether Vizion or project44 can add GWF to their coverage on request.

### Recommended Lookup Method

For the web portal, both **Bill of Lading number** and **Container number** are supported for tracking lookups. If EDI integration were established, B/L number would be the recommended primary identifier.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | N/A -- no API to poll |
| **Incremental filter** | N/A |
| **Batch tracking** | N/A |

### Auth Implementation Notes

N/A -- no API authentication required since no API exists.

### Edge Cases to Handle

- **MSC cross-tracking**: If tracking GWF cargo via MSC's API (for space charter shipments), the B/L or booking reference format may differ between carriers. Mapping between GWF and MSC identifiers would be needed.

- **Portal CAPTCHA**: If web scraping is attempted, the CAPTCHA on the SolverMinds portal would need to be handled, likely through a CAPTCHA-solving service.

- **Limited route coverage**: GWF only serves Central America to U.S./Europe routes. Any integration should validate that a shipment's route matches GWF's service area before attempting a lookup.

### Mapping Complexity

**N/A (no API).** If EDI integration were established, mapping complexity would be **medium** -- standard EDIFACT message types (IFTSTA, IFTMIN) would need to be parsed and mapped to the canonical DCSA model. If web scraping were used, mapping complexity would be **high** due to the need to parse HTML/JavaScript responses from the SolverMinds portal.

---

## Open Questions

- [ ] Does SSL need to track GWF shipments at all? What is the volume of GWF shipments in SSL's portfolio?
- [ ] Can GWF shipments on MSC vessels (via the space charter agreement) be tracked through MSC's API?
- [ ] Does GWF offer EDI connectivity for tracking status messages (IFTSTA)?
- [ ] Would Chiquita's logistics team be willing to establish a data exchange agreement with SSL?
- [ ] Do aggregators like Vizion or project44 cover GWF, or could they add coverage on request?
- [ ] Is the SolverMinds portal (gwfonline.solverminds.net) the same platform used for internal operations, or is it a customer-facing subset?
- [ ] What data does the GWF web portal tracking feature actually expose? (Requires a GWF customer account to investigate)

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | https://greatwhitefleet.com |
| About / Who We Are | https://greatwhitefleet.com/who-we-are |
| Bills of Lading Terms | https://greatwhitefleet.com/bills-of-lading |
| SolverMinds Web Portal | https://gwfonline.solverminds.net/ecomonline/ |
| Fluent Cargo Schedules (UBCU) | https://www.fluentcargo.com/carriers/scac/UBCU |
| MSC Space Charter Agreement | https://www.freightwaves.com/news/msc-and-great-white-fleet-file-space-charter-agreement |
| Chiquita-GWF Reefer Investment | https://news.cision.com/chiquita-brands-international/r/chiquita-s-great-white-fleet-increases-investment-in-carrier-transicold-s-primeline-container-refrig,c3814968 |
| GWF on Port Everglades | https://www.porteverglades.net/listing/great-white-fleet-liner-services-ltd/358/ |
| GWF LinkedIn | https://www.linkedin.com/company/great-white-fleet-ltd- |
| e-tracking.net GWF Tracking | https://e-tracking.net/tracking/container-tracking/great-white-fleet |
| Chiquita Wikipedia | https://en.wikipedia.org/wiki/Chiquita |
