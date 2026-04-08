# Tropical Shipping -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing
> **Researched by**: Agent
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | Tropical Shipping (commonly "Tropical Shipping"; legal entity Tropical Shipping & Construction Co., Ltd.) |
| **SCAC Code** | TSCW |
| **Parent Company** | Saltchuk Resources (acquired 2014 for ~$220M). Saltchuk Marine group also owns TOTE Maritime and Foss Maritime |
| **Alliance** | Independent |
| **Primary Services** | Container shipping (FCL, LCL), consolidation, break bulk, refrigerated, project cargo, vehicle transport, air freight (Trop Air), small package (TropBox) |
| **Market Position** | Regional Caribbean specialist -- dominant carrier for US-Caribbean and US-Bahamas trade lanes since 1965 |
| **Headquarters** | Riviera Beach (West Palm Beach area), Florida, USA |
| **Website** | https://www.tropical.com |

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | No |
| **Developer portal URL** | N/A |
| **API documentation URL(s)** | N/A -- no public API documentation found |
| **Documentation quality** | None -- no API docs exist |
| **OpenAPI/Swagger spec available?** | No |
| **Sandbox/test environment?** | No |
| **Developer registration** | N/A |
| **Developer support channels** | General customer service only: 800-638-TROP (8767) / 561-881-3999, customersupport@shiptropical.com |
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
| **Known DCSA deviations** | N/A -- Tropical Shipping does not implement DCSA APIs |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Unknown | No EDI capabilities publicly documented. Given small carrier size, likely limited or through INTTRA if at all |
| **INTTRA integration** | Unknown | Tropical Shipping not found in available INTTRA partner lists |
| **BIC (Bureau International des Containers)** | Yes | Standard container prefix TSCW used for container identification |
| **UN/LOCODE** | Unknown | Schedule data on website uses port names, not confirmed whether UN/LOCODE is used internally |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | N/A -- no API available |
| **Auth documentation** | N/A |
| **Registration process** | N/A -- no API registration exists. Customer portal (eServices) requires account with Tropical Shipping as a business customer |
| **Registration URL** | N/A |
| **Partner program required?** | N/A |
| **Partner program URL** | N/A |
| **Credential type** | N/A |
| **Token refresh supported?** | N/A |
| **Token lifetime** | N/A |
| **Access tiers** | N/A |
| **IP whitelisting required?** | N/A |

### Access Requirements Summary for SSL

Tropical Shipping does not offer any public API. All digital interaction is through their eServices web portal (https://login.tropical.com/ and https://eservices.tropical.com/), which is a customer-facing portal for booking, payment, document upload, and cargo tracking. The portal uses Okta authentication (introduced in eServices 2.0, February 2023). There is no developer access, no API documentation, and no indication that programmatic integration is available.

SSL would need to explore alternative access methods: (1) contact Tropical Shipping directly to inquire about any unpublished API or EDI capabilities, (2) use third-party aggregators like Portcast that claim Tropical Shipping tracking coverage, or (3) assess web portal scraping feasibility as a last resort.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field has a row.
> Availability legend: check = Available | x = Not available | warning = Partial / limited | question = Unknown

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ❌ | N/A (web portal only) | N/A | N/A | Schedule data visible on tropical.com/schedules/ (280 routes) but no API. Web-only interactive lookup by departure/arrival port |
| 1.2 | Point-to-Point Route Options | ❌ | N/A | N/A | N/A | Route options viewable on website schedule tool only |
| 1.3 | Booking Lifecycle | ❌ | N/A (eServices portal only) | N/A | N/A | Booking available through eServices web portal (login.tropical.com). No API |
| 1.4 | Shipping Instructions | ❌ | N/A | N/A | N/A | Document upload available through eServices portal (bonds, vehicle titles, MSPO) but no API |
| 1.5 | Rates | ❌ | N/A | N/A | N/A | No rate API. Rates likely communicated via email/portal |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❌ | N/A | N/A | `ECP` | No API to retrieve cutoff data |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❌ | N/A | N/A | `EFC` | No API to retrieve cutoff data |
| 2.3 | Documentation Cutoff | DCO | ❌ | N/A | N/A | `DCO` | No API to retrieve cutoff data |
| 2.4 | VGM Cutoff | VCO | ❌ | N/A | N/A | `VCO` | No API to retrieve cutoff data |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ❌ | N/A | N/A | `FCO` | No API to retrieve cutoff data |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❌ | N/A | N/A | `LCO` | No API to retrieve cutoff data |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ❌ | N/A | N/A | Inferred from first EquipmentEvent | No API |
| 3.2 | Empty Container Gate-Out (Pickup) | ❌ | N/A | N/A | `GTOT` + `EMPTY` | No API. eServices portal shows event type, date/time, and details for tracking but no programmatic access |
| 3.3 | Full Container Gate-In | ❌ | N/A | N/A | `GTIN` + `LADEN` | No API |
| 3.4 | Container Loaded on Vessel | ❌ | N/A | N/A | `LOAD` + `LADEN` | No API |
| 3.5 | Container Discharged at Transshipment | ❌ | N/A | N/A | `DISC` + `LADEN` + transshipment | No API |
| 3.6 | Container Loaded at Transshipment | ❌ | N/A | N/A | `LOAD` + `LADEN` + transshipment | No API |
| 3.7 | Container Discharged at Destination | ❌ | N/A | N/A | `DISC` + `LADEN` | No API |
| 3.8 | Full Container Gate-Out (Delivery) | ❌ | N/A | N/A | `GTOT` + `LADEN` | No API |
| 3.9 | Empty Container Returned | ❌ | N/A | N/A | `GTIN` + `EMPTY` | No API |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ❌ | N/A | N/A | `DEPA` + classifier | No API. Schedule data viewable on website only |
| 4.2 | Estimated Time of Arrival | ETA | ❌ | N/A | N/A | `ARRI` + classifier | No API |
| 4.3 | Vessel Arrival at Transshipment | -- | ❌ | N/A | N/A | `ARRI` at intermediate | No API |
| 4.4 | Vessel Departure from Transshipment | -- | ❌ | N/A | N/A | `DEPA` at intermediate | No API |

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
> - Tropical Shipping has zero API coverage because no public API exists.
> - The eServices portal (eservices.tropical.com) provides tracking data including event type, date/time, details, equipment number, size, type, seals, and vessel information -- but exclusively through a web portal with Okta authentication. No programmatic access is available.
> - The web portal distinguishes between FCL, LCL, and Break Bulk shipments for tracking purposes.
> - Third-party aggregators (Portcast) claim tracking coverage for Tropical Shipping containers, suggesting that tracking data does flow through AIS/terminal data sources even if Tropical Shipping itself does not expose an API.

---

## Endpoint Reference

No API endpoints available. Tracking is limited to the eServices portal.

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | https://login.tropical.com/ (eServices portal); formerly tracked from tropical.com homepage (disabled October 2023) |
| **Login required?** | Yes -- Okta-authenticated eServices account required (since eServices 2.0, February 2023) |
| **Data available on portal but NOT in API** | All data is portal-only: tracking events (event type, date/time, details), equipment details (number, size, type, seals), vessel information, booking status, cargo status for FCL/LCL/BB shipments |
| **Scraping feasibility** | Difficult -- Okta authentication adds complexity. Portal is modern web application (eServices 2.0 launched 2023). ToS likely prohibits scraping. Not recommended |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Unknown |
| **EDI message types** | Unknown |
| **EDI connection method** | Unknown |
| **EDI documentation** | Unknown -- contact Tropical Shipping directly to inquire |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Unknown | TSGL/TSCW not confirmed in available project44 carrier lists. Would need to check directly |
| **FourKites** | Unknown | Not confirmed |
| **Vizion** | Unknown | Not found in Vizion's supported carrier page. May be covered through terminal data |
| **INTTRA / E2open** | Unknown | Not confirmed as an INTTRA partner |
| **CargoSmart** | Unknown | Not confirmed |
| **Portcast** | Yes | Portcast explicitly lists Tropical Shipping tracking coverage. Offers container tracking by container number, booking number, and B/L number. Provides real-time ETAs, delay reasons, port congestion data |
| **Terminal49** | No | Not listed among Terminal49's 34+ supported shipping lines |
| **Fluent Cargo** | Yes | Lists Tropical Shipping (SCAC: TSGL) with schedule and tracking data |

> **Aggregator note:** Tropical Shipping has no direct API. The only confirmed programmatic tracking option is through Portcast, which offers container-level visibility including predictive ETAs. Portcast likely derives tracking data from AIS vessel tracking and terminal data sources rather than a direct carrier API feed. For SSL, using an aggregator like Portcast may be the only viable path to automated Tropical Shipping tracking without web scraping.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown -- no API to measure | Unknown |
| **API uptime/reliability** | N/A -- no API exists | N/A |
| **Historical data depth** | Unknown | Unknown |
| **Timezone handling** | Unknown | Unknown |
| **Character encoding** | Unknown | Unknown |

### Known Issues & Gotchas

- **No API exists.** This is the fundamental constraint. All digital functionality is locked behind the eServices web portal with Okta authentication.

- **Homepage tracking was disabled in October 2023.** Tropical Shipping moved all tracking to the authenticated eServices portal, eliminating the previously available unauthenticated tracking lookup on the homepage.

- **eServices 2.0 modernization (February 2023).** The portal was rebuilt with Okta authentication, making any scraping approach significantly more complex than it would have been with the legacy system.

- **Two SCAC codes in use.** Tropical Shipping uses TSCW (Tropical Shipping & Construction Co.) as the primary container prefix and SCAC code, but some third-party sources list TSGL (associated with the Tropical brand more broadly). Aggregator queries may need to try both codes.

- **Regional carrier with limited technology investment.** As a Caribbean-focused regional carrier (compared to global carriers like Maersk or CMA CGM), Tropical Shipping has not invested in developer-facing API infrastructure. This is common among smaller regional carriers.

- **Saltchuk group does not share technology platforms.** Despite being part of Saltchuk (which also owns TOTE Maritime), there is no indication that Tropical Shipping shares any API or technology platform with TOTE or other Saltchuk subsidiaries.

- **Separate Tropical Express brand.** Tropical Express (shiptropical.com) appears to be a related small-package/courier service with its own portals (customers.shiptropical.com, portal.shiptropical.com, track.shiptropical.com). This is distinct from the ocean container shipping service at tropical.com.

### Recently Deprecated or Changed

- October 2023: Homepage cargo tracking disabled; all tracking moved to authenticated eServices portal
- February 2023: eServices 2.0 launched with Okta authentication, enhanced tracking views, integrated payments

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | No -- not with direct carrier integration. No API exists. Possible only through aggregator (Portcast) or web scraping (not recommended) |
| **Implementation effort** | Very High (no API) -- would require either aggregator integration or web scraping |
| **DCSA base adapter usable?** | No -- no API of any kind to adapt |

### Recommended Approach

Tropical Shipping cannot be integrated via a direct carrier adapter because no API exists. There are three potential approaches, listed in order of recommendation:

1. **Aggregator integration (Portcast).** Portcast confirms Tropical Shipping tracking coverage. SSL could use the Portcast API to get container-level visibility including predictive ETAs, delay reasons, and transit events. This would be an aggregator adapter rather than a carrier adapter. The data likely comes from AIS vessel tracking and terminal/port data rather than from Tropical Shipping's own systems, so coverage of detailed container milestones (gate-in, gate-out, loaded, discharged) may be limited compared to carriers with direct API feeds.

2. **Contact Tropical Shipping directly.** As a Saltchuk-owned carrier, there may be unpublished EDI or API capabilities available to business partners that are not publicly advertised. SSL should inquire with Tropical Shipping's IT/operations team about B2B integration options.

3. **Web scraping (not recommended).** The eServices portal contains tracking data, but Okta authentication, modern web application architecture, and likely ToS restrictions make scraping impractical and unreliable.

### Recommended Lookup Method

If using Portcast or a similar aggregator: **Bill of Lading number** as primary, **Container number** as secondary. Both are supported by Portcast for Tropical Shipping tracking.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Dependent on aggregator (Portcast) rate limits and data freshness. Likely every 4-6 hours |
| **Incremental filter** | Dependent on aggregator API capabilities |
| **Batch tracking** | Dependent on aggregator API capabilities |

### Auth Implementation Notes

N/A -- no direct carrier API exists. Auth implementation would be against the aggregator API (Portcast or similar), not against Tropical Shipping directly.

### Edge Cases to Handle

- **Dual SCAC codes**: Tracking queries may need to use both TSCW and TSGL depending on the aggregator's carrier identification system
- **Limited Caribbean routes**: Tropical Shipping operates primarily US-Caribbean routes from Palm Beach, FL. Trade lanes are narrower than global carriers, which may affect aggregator data quality/freshness
- **No transshipment complexity**: Tropical Shipping operates direct Caribbean services with limited transshipment, which simplifies the tracking data model but also means transshipment events (3.5, 3.6, 4.3, 4.4) are rarely relevant

### Mapping Complexity

**Low complexity (if using aggregator)** -- Portcast and similar aggregators return normalized data. The main mapping challenge is converting aggregator-specific event formats to SSL's canonical DCSA model, which is a common pattern across all aggregator-sourced carriers.

**Not applicable (for direct integration)** -- there is no carrier API to map from.

---

## Open Questions

- [ ] Does Tropical Shipping offer any unpublished EDI or API capabilities for business partners?
- [ ] Does SSL have an existing business relationship with Tropical Shipping that could facilitate technology discussions?
- [ ] Does Portcast provide full container milestone coverage (gate-in, loaded, discharged, gate-out) for Tropical Shipping, or only vessel-level AIS data?
- [ ] Is TSCW or TSGL the correct SCAC code to use with various aggregators?
- [ ] Are there other aggregators beyond Portcast that provide Tropical Shipping tracking data?
- [ ] Does Tropical Shipping have any plans to develop a public API? (Given Saltchuk ownership and recent eServices modernization, this is plausible in the medium term)

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | https://www.tropical.com |
| eServices Portal | https://login.tropical.com/ |
| eServices Portal (alt) | https://eservices.tropical.com/ |
| Schedules Page | https://www.tropical.com/schedules/ |
| Locations | https://www.tropical.com/locations/ |
| Contact Page | https://www.tropical.com/contact/ |
| Saltchuk Parent Company | https://www.saltchuk.com/ |
| Saltchuk Acquisition Announcement | https://www.saltchuk.com/saltchuk/saltchuk-announces-acquisition-tropical-shipping |
| Portcast Tropical Tracking | https://www.portcast.io/carrier-coverage/tropical-shipping-container-tracking |
| Fluent Cargo Tropical Schedules | https://www.fluentcargo.com/carriers/scac/TSGL |
| eServices 2.0 Announcement | https://www.tropical.com/news/2023/tropical-eservices-20 |
| Homepage Tracking Disabled | https://www.tropical.com/news/2023/cargo-tracking-on-tropicalcom-homepage-to-be-disabled-effective-october-21-2023 |
| Panjiva TSCW Profile | https://panjiva.com/scac_profiles/profile/TSCW |
