# Linea Peninsular -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing
> **Researched by**: Agent
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | Linea Peninsular Inc (commonly "Linea Peninsular") |
| **SCAC Code** | LPUS |
| **Parent Company** | Independent |
| **Alliance** | None / Independent |
| **Primary Services** | Container shipping (breakbulk, RoRo, project cargo), warehouse consolidation/deconsolidation, inland trucking, customs brokerage |
| **Market Position** | Regional niche carrier specializing in U.S. Gulf Coast -- Yucatan Peninsula trade. Serves 100% of the Yucatan Peninsula's maquiladora factories. Over 40 years of operation |
| **Headquarters** | Panama City, FL (USA); Merida, Yucatan (Mexico) |
| **Website** | https://www.lineaships.com |

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
| **Developer support channels** | General email: rates@lineaships.com; U.S. office phone: 850.522.4500 |
| **Community/third-party libraries** | None found |
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
| **Known DCSA deviations** | N/A -- Linea Peninsular does not implement DCSA APIs |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Unknown | No public documentation of EDI capability found. Given the carrier's small size, EDI is unlikely |
| **INTTRA integration** | Unknown | Not listed among INTTRA carrier partners in public materials |
| **BIC (Bureau International des Containers)** | Unknown | Standard container ID format likely used but not confirmed |
| **UN/LOCODE** | Unknown | Ports served (Progreso, Tampa, Panama City, Houston) have standard UN/LOCODEs but carrier's use of them is unconfirmed |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | N/A (no public API) |
| **Auth documentation** | N/A |
| **Registration process** | Customer portal only: contact Brenda Pomes (brenda@lineaships.com) to register. Must be a current Linea Peninsular customer |
| **Registration URL** | https://www.lineaships.com/en/online-access/ |
| **Partner program required?** | Yes -- must be an existing customer to access the web portal |
| **Partner program URL** | N/A |
| **Credential type** | Web portal login (username/password) |
| **Token refresh supported?** | N/A |
| **Token lifetime** | N/A |
| **Access tiers** | Single tier -- customer portal access |
| **IP whitelisting required?** | N/A |

### Access Requirements Summary for SSL

Linea Peninsular does not offer any public API or developer portal. Their only digital access method is a customer-only web portal (WebISIS) at `webisis.lineaships.com/isis/webisis.dll` that requires manual registration through a named contact (Brenda Pomes). SSL would need an existing business relationship with Linea Peninsular to access even the web portal.

To obtain any programmatic access, SSL would likely need to either: (1) establish a shipping customer relationship and then explore whether the web portal can be scraped, (2) contact Linea Peninsular directly to inquire about any private API or EDI capabilities not documented publicly, or (3) use a third-party aggregator if one covers this carrier.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field has a row.
> Availability legend: check = Available | x = Not available | warning = Partial / limited | question = Unknown

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ❌ | N/A (no API) | N/A | N/A | Schedule data available only on website HTML tables at lineaships.com/en/schedules/. Not programmatically accessible |
| 1.2 | Point-to-Point Route Options | ❌ | N/A (no API) | N/A | N/A | Limited routes (Panama City/Tampa/Houston to Progreso) visible on website only |
| 1.3 | Booking Lifecycle | ❌ | N/A (no API) | N/A | N/A | Booking details viewable in customer portal (WebISIS) but no API |
| 1.4 | Shipping Instructions | ❌ | N/A (no API) | N/A | N/A | No programmatic SI capability found |
| 1.5 | Rates | ❌ | N/A (no API) | N/A | N/A | Rate quotes via email (rates@lineaships.com) or website contact form only |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❌ | N/A | N/A | `ECP` | No API access |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❌ | N/A | N/A | `EFC` | No API access |
| 2.3 | Documentation Cutoff | DCO | ❌ | N/A | N/A | `DCO` | No API access |
| 2.4 | VGM Cutoff | VCO | ❌ | N/A | N/A | `VCO` | No API access |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ❌ | N/A | N/A | `FCO` | No API access |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❌ | N/A | N/A | `LCO` | No API access |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ❌ | N/A | N/A | Inferred from first EquipmentEvent | No API access |
| 3.2 | Empty Container Gate-Out (Pickup) | ❌ | N/A | N/A | `GTOT` + `EMPTY` | No API access. Portal may show some container status |
| 3.3 | Full Container Gate-In | ❌ | N/A | N/A | `GTIN` + `LADEN` | No API access |
| 3.4 | Container Loaded on Vessel | ❌ | N/A | N/A | `LOAD` + `LADEN` | No API access |
| 3.5 | Container Discharged at Transshipment | ❌ | N/A | N/A | `DISC` + `LADEN` + transshipment | No API; carrier operates direct routes with minimal transshipment |
| 3.6 | Container Loaded at Transshipment | ❌ | N/A | N/A | `LOAD` + `LADEN` + transshipment | No API; carrier operates direct routes with minimal transshipment |
| 3.7 | Container Discharged at Destination | ❌ | N/A | N/A | `DISC` + `LADEN` | No API access |
| 3.8 | Full Container Gate-Out (Delivery) | ❌ | N/A | N/A | `GTOT` + `LADEN` | No API access |
| 3.9 | Empty Container Returned | ❌ | N/A | N/A | `GTIN` + `EMPTY` | No API access |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ❌ | N/A | N/A | `DEPA` + classifier | Schedule page shows ETD on website HTML only |
| 4.2 | Estimated Time of Arrival | ETA | ❌ | N/A | N/A | `ARRI` + classifier | Schedule page shows ETA on website HTML only |
| 4.3 | Vessel Arrival at Transshipment | -- | ❌ | N/A | N/A | `ARRI` at intermediate | Carrier operates direct routes; transshipment unlikely |
| 4.4 | Vessel Departure from Transshipment | -- | ❌ | N/A | N/A | `DEPA` at intermediate | Carrier operates direct routes; transshipment unlikely |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❌ | No API or webhook system |
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

---

## Endpoint Reference / Lookup Methods

No API endpoints available. Tracking is limited to the customer portal.

---

## Rate Limits

No API available; rate limits not applicable.

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | https://webisis.lineaships.com/isis/webisis.dll (customer portal; requires login) |
| **Login required?** | Yes -- must be a registered customer. Contact brenda@lineaships.com to register |
| **Data available on portal but NOT in API** | All data is portal-only: Bills of Lading, Accounts Receivable, Trailer Interchange Receipts, Booking details, Invoices, Delivery Receipts, Dock Receipts, U.S. Customs entry status, container tracking |
| **Scraping feasibility** | Difficult -- portal is a DLL-based WebISIS application (likely a legacy Windows-based system). Login-gated access. Anti-bot measures (reCAPTCHA on website). Scraping ToS status unknown |

### Third-Party Tracking (e-tracking.net)

| Detail | Value |
|--------|-------|
| **Available?** | Yes |
| **URL** | https://e-tracking.net/tracking/container-tracking/linea-peninsular |
| **Identifiers** | Container number, Bill of Lading number |
| **Data provided** | Current location, transit history, loading/unloading events, vessel assignments, estimated arrival times |
| **API available?** | Unknown -- e-tracking.net provides web-based tracking but API access unclear |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Unknown |
| **EDI message types** | Unknown |
| **EDI connection method** | Unknown |
| **EDI documentation** | N/A |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Unknown | Not confirmed in public carrier lists |
| **FourKites** | Unknown | Not confirmed in public carrier lists |
| **Vizion** | Unknown | Not confirmed in public carrier lists |
| **INTTRA / E2open** | Unknown | Not found in INTTRA carrier partner lists |
| **CargoSmart** | Unknown | Not confirmed |
| **Terminal49** | No | Not listed among Terminal49's 34 supported carriers |

> **Aggregator note**: Linea Peninsular is a small regional carrier, and major aggregators do not appear to cover it. The third-party site e-tracking.net offers web-based tracking for Linea Peninsular containers, but it is unclear whether they provide API access or how they source the data. If aggregator coverage exists, it would likely be the most viable path to programmatic tracking data.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown -- no API | Unknown |
| **API uptime/reliability** | N/A -- no API | N/A |
| **Historical data depth** | Unknown -- portal data depth not documented | Unknown |
| **Timezone handling** | Unknown | Unknown |
| **Character encoding** | Unknown | Unknown |

### Known Issues & Gotchas

- **No API whatsoever**: Linea Peninsular has zero public API surface. All digital services are behind a customer-only web portal running legacy DLL-based software (WebISIS).

- **Customer-gated access**: Even the web portal requires an existing business relationship and manual registration through a specific contact person.

- **Legacy technology stack**: The WebISIS portal (`webisis.lineaships.com/isis/webisis.dll`) appears to be a legacy Windows/DLL-based application, suggesting limited modern integration capability.

- **Very small fleet**: The carrier operates approximately 3-4 vessels (Progreso, Juan Diego, Campeche Bay) on a handful of routes. The small scale makes API investment by the carrier unlikely in the near term.

- **Limited route network**: Service is concentrated on U.S. Gulf Coast (Panama City FL, Tampa FL, Houston TX) to Progreso, Mexico. Worldwide coverage is achieved through partnerships with other carriers, not their own fleet.

### Recently Deprecated or Changed

- No changes documented. The carrier's web presence and technology appear to have been stable for an extended period.

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | No -- no API exists. Portal scraping is technically possible but unreliable and legally uncertain |
| **Implementation effort** | Very High (no API) -- would require web scraping of a legacy DLL-based portal or reliance on an aggregator (if one covers this carrier) |
| **DCSA base adapter usable?** | No -- no API of any kind, let alone DCSA-compliant |

### Recommended Approach

Linea Peninsular has no API, no developer portal, no published EDI capability, and no DCSA compliance. The only digital access method is a customer-gated web portal running legacy WebISIS software. Building a direct SDK adapter is not feasible.

The recommended approach, in priority order:

1. **Investigate aggregator coverage**: Contact project44, Vizion, and FourKites to determine whether any aggregator covers Linea Peninsular. Given the carrier's small size, coverage is unlikely but worth confirming. The third-party tracking site e-tracking.net appears to have some data source for Linea Peninsular -- investigating their data sourcing method could be informative.

2. **Contact Linea Peninsular directly**: Inquire whether they offer any private API, EDI, or data feed capabilities not documented publicly. Small carriers sometimes have unpublished integration options available to business partners.

3. **Portal scraping (last resort)**: If SSL has a business relationship with Linea Peninsular and obtains portal access, scraping the WebISIS portal could theoretically extract tracking data. However, the DLL-based architecture makes this technically challenging, and the approach is fragile and potentially ToS-violating.

4. **Deprioritize**: Given Linea Peninsular's extremely narrow geographic scope (Gulf Coast USA to Yucatan, Mexico only) and small fleet, this carrier may not warrant significant integration effort unless SSL has specific business requirements for this trade lane.

### Recommended Lookup Method

If tracking data becomes available through any method, **Bill of Lading number** would be the primary identifier, as the portal and third-party tracking sites support B/L lookup. **Container number** as secondary.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | N/A -- no API to poll |
| **Incremental filter** | N/A |
| **Batch tracking** | N/A |

### Auth Implementation Notes

No API exists. If portal scraping were attempted, it would require session-based web authentication against the WebISIS DLL application.

### Edge Cases to Handle

- **Direct routes only**: Linea Peninsular operates direct point-to-point services with 2-3 day transit times. Transshipment events (milestones 3.5, 3.6, 4.3, 4.4) are largely irrelevant for this carrier.

- **Worldwide coverage via partnerships**: Linea Peninsular offers worldwide shipping through carrier agreements with major shipping companies. These movements would be tracked under the partner carrier's system, not Linea Peninsular's.

### Mapping Complexity

N/A -- no API data to map. If data were obtained through scraping or an aggregator, the mapping complexity would depend entirely on the data format provided by that source.

---

## Open Questions

- [ ] Does Linea Peninsular offer any private/unpublished API or EDI capabilities to business partners?
- [ ] Does SSL have an existing business relationship with Linea Peninsular?
- [ ] Is Linea Peninsular covered by any third-party aggregator (project44, Vizion, FourKites)?
- [ ] How does e-tracking.net source its Linea Peninsular tracking data? Could SSL use the same data source?
- [ ] Would Linea Peninsular consider developing API capabilities if requested by a partner?
- [ ] What data is actually visible in the WebISIS customer portal? The public website lists document types but not the granularity of tracking events.
- [ ] Does Linea Peninsular have plans to modernize their digital platform?

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | https://www.lineaships.com |
| Company Overview | https://www.lineaships.com/en/linea-peninsular/ |
| Online Access / Portal | https://www.lineaships.com/en/online-access/ |
| Schedules | https://www.lineaships.com/en/schedules/ |
| Contact Page | https://www.lineaships.com/en/contact/ |
| Shipping Guidelines | https://www.lineaships.com/en/shipping-guidelines/ |
| SCAC Profile (Panjiva) | https://panjiva.com/scac_profiles/profile/LPUS |
| E-tracking Container Tracking | https://e-tracking.net/tracking/container-tracking/linea-peninsular |
| E-tracking B/L Tracking | https://e-tracking.net/tracking/bl-tracking/linea-peninsular |
| PayCargo Payment | https://paycargo.com/vendors/linea-peninsular/ |
