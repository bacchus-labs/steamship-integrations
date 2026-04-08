# Maruba -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing
> **Researched by**: Agent
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | Maruba S.C.A. (commonly "Maruba") |
| **SCAC Code** | MRUB |
| **Parent Company** | Independent (private Argentine company) |
| **Alliance** | Independent |
| **Primary Services** | Container (Patagonian feeder), bulk cargo, tanker, tug boats, car carrier, river transport, logistics |
| **Market Position** | Largest maritime company in Argentina; regional specialist focused on Argentine cabotage, Patagonian feeder services, and South American trades |
| **Headquarters** | Buenos Aires, Argentina |
| **Website** | https://www.maruba.com.ar |

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | No |
| **Developer portal URL** | N/A |
| **API documentation URL(s)** | N/A |
| **Documentation quality** | None |
| **OpenAPI/Swagger spec available?** | No |
| **Sandbox/test environment?** | No |
| **Developer registration** | N/A |
| **Developer support channels** | General contact: info@maruba.com.ar, agency@maruba.com.ar, phone +54 11 5279 5555 |
| **Community/third-party libraries** | None found |
| **API changelog / release notes** | Not published |

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
| **Known DCSA deviations** | N/A -- Maruba does not implement any DCSA APIs |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Unknown | No evidence of EDI capability found in public materials |
| **INTTRA integration** | Unknown | No evidence of INTTRA partnership found |
| **BIC (Bureau International des Containers)** | Unknown | Container prefixes JOL, NEX, SAR identified; BIC compliance not confirmed |
| **UN/LOCODE** | Unknown | No documentation available |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | N/A |
| **Auth documentation** | N/A |
| **Registration process** | N/A -- no public API exists |
| **Registration URL** | N/A |
| **Partner program required?** | N/A |
| **Partner program URL** | N/A |
| **Credential type** | N/A |
| **Token refresh supported?** | N/A |
| **Token lifetime** | N/A |
| **Access tiers** | N/A |
| **IP whitelisting required?** | N/A |

### Access Requirements Summary for SSL

Maruba does not offer any public API, developer portal, or programmatic access to tracking, scheduling, or booking data. The company's website provides general corporate and service information but no online tracking tool, no booking platform, and no digital integration capabilities. An ecommerce subdomain (ecom.maruba.com.ar) exists but has an expired SSL certificate and appears to be a customer login portal with unknown capabilities.

To obtain shipment data from Maruba, SSL would need to establish a direct business relationship and inquire about data exchange options (likely manual -- email, phone, or possibly EDI if available). Given Maruba's regional focus and lack of digital infrastructure, programmatic integration is not currently feasible without a custom arrangement.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field has a row.
> Availability legend: check = Available | x = Not available | warning = Partial / limited | question = Unknown

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | N/A | N/A | N/A | N/A | No API exists. Schedule information available only via direct contact |
| 1.2 | Point-to-Point Route Options | N/A | N/A | N/A | N/A | No API exists |
| 1.3 | Booking Lifecycle | N/A | N/A | N/A | N/A | No API exists. Booking likely handled via email/phone |
| 1.4 | Shipping Instructions | N/A | N/A | N/A | N/A | No API exists |
| 1.5 | Rates | N/A | N/A | N/A | N/A | No API exists. Rates likely provided via direct quotation |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | N/A | N/A | N/A | `ECP` | No API exists |
| 2.2 | Earliest Full-Container Delivery Date | EFC | N/A | N/A | N/A | `EFC` | No API exists |
| 2.3 | Documentation Cutoff | DCO | N/A | N/A | N/A | `DCO` | No API exists |
| 2.4 | VGM Cutoff | VCO | N/A | N/A | N/A | `VCO` | No API exists |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | N/A | N/A | N/A | `FCO` | No API exists |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | N/A | N/A | N/A | `LCO` | No API exists |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | N/A | N/A | N/A | Inferred from first EquipmentEvent | No API exists |
| 3.2 | Empty Container Gate-Out (Pickup) | N/A | N/A | N/A | `GTOT` + `EMPTY` | No API exists |
| 3.3 | Full Container Gate-In | N/A | N/A | N/A | `GTIN` + `LADEN` | No API exists |
| 3.4 | Container Loaded on Vessel | N/A | N/A | N/A | `LOAD` + `LADEN` | No API exists |
| 3.5 | Container Discharged at Transshipment | N/A | N/A | N/A | `DISC` + `LADEN` + transshipment | No API exists |
| 3.6 | Container Loaded at Transshipment | N/A | N/A | N/A | `LOAD` + `LADEN` + transshipment | No API exists |
| 3.7 | Container Discharged at Destination | N/A | N/A | N/A | `DISC` + `LADEN` | No API exists |
| 3.8 | Full Container Gate-Out (Delivery) | N/A | N/A | N/A | `GTOT` + `LADEN` | No API exists |
| 3.9 | Empty Container Returned | N/A | N/A | N/A | `GTIN` + `EMPTY` | No API exists |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | N/A | N/A | N/A | `DEPA` + classifier | No API exists |
| 4.2 | Estimated Time of Arrival | ETA | N/A | N/A | N/A | `ARRI` + classifier | No API exists |
| 4.3 | Vessel Arrival at Transshipment | -- | N/A | N/A | N/A | `ARRI` at intermediate | No API exists |
| 4.4 | Vessel Departure from Transshipment | -- | N/A | N/A | N/A | `DEPA` at intermediate | No API exists |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | N/A | No API exists |
| Event Polling with timestamp filter | N/A | No API exists |
| Event Classifier Progression (PLN->EST->ACT) | N/A | No API exists |
| Retracted Events | N/A | No API exists |
| Change Remarks | N/A | No API exists |
| Delay Reason Codes | N/A | No API exists |

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
> Maruba does not offer any public API. All 30 fields are marked as unavailable because there is no programmatic access method. The carrier operates primarily through traditional channels (phone, email, in-person) and does not appear to have invested in digital/API infrastructure for external integrations.

---

## Endpoint Reference

No API endpoints exist. Maruba does not expose any REST, SOAP, or other web service APIs for tracking, scheduling, booking, or any other purpose.

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | None found. The main website (maruba.com.ar) has no public tracking tool. An ecommerce portal exists at ecom.maruba.com.ar but has an expired SSL certificate and requires login |
| **Login required?** | Yes (ecom.maruba.com.ar requires authentication; capabilities unknown) |
| **Data available on portal but NOT in API** | N/A -- no API exists for comparison |
| **Scraping feasibility** | Not assessed -- no public tracking page found to scrape. The ecom portal (if functional) would require credentials |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Unknown |
| **EDI message types** | Unknown |
| **EDI connection method** | Unknown |
| **EDI documentation** | Unknown -- would need to inquire directly with Maruba |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Unknown | Not listed in project44's publicly available carrier lists |
| **FourKites** | Unknown | No evidence of coverage found |
| **Vizion** | Unknown | No evidence of coverage found |
| **INTTRA / E2open** | Unknown | No evidence of partnership found |
| **CargoSmart** | Unknown | No evidence of coverage found |
| **Terminal49** | No | Confirmed not listed in Terminal49's supported shipping lines |
| **Shipsgo** | Unknown | Not found in carrier-specific tracking pages |
| **shipping-data.com** | Yes | Maruba listed on shipping-data.com with container prefixes JOL, NEX, SAR; tracking link points to maruba.com.ar (which has no public tracking tool) |

> **Aggregator note:** Maruba does not appear to be covered by any major visibility aggregator. Given the carrier's small regional footprint and lack of API infrastructure, aggregator coverage is unlikely. Any tracking integration would need to be arranged through direct business relationship with Maruba or through manual data exchange.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown -- no API or tracking system found | Unknown |
| **API uptime/reliability** | N/A -- no API exists | N/A |
| **Historical data depth** | Unknown | Unknown |
| **Timezone handling** | Unknown (Argentina uses ART, UTC-3) | Estimated |
| **Character encoding** | Unknown | Unknown |

### Known Issues & Gotchas

- **No digital infrastructure**: Maruba has no public API, no documented tracking portal, and no developer resources. This is a traditional, offline-first shipping operation.

- **Expired SSL certificate on ecom portal**: The ecommerce subdomain (ecom.maruba.com.ar) has an expired SSL certificate, suggesting limited investment in digital infrastructure maintenance.

- **Regional/niche operator**: Maruba primarily operates Patagonian feeder services (Buenos Aires to Ushuaia), river transport on the Parana-Paraguay waterway, and tanker/bulk/car carrier services. Its container operations are limited compared to global carriers.

- **Container prefixes**: JOL, NEX, SAR -- these are non-standard prefixes that may complicate container identification in multi-carrier scenarios.

- **Language barrier**: Maruba's website and operations are primarily Spanish-language. English documentation is minimal.

### Recently Deprecated or Changed

- No information available. The company's digital presence appears to have been static for an extended period.

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | No -- Maruba has no API, no documented web tracking, and no aggregator coverage. There is nothing to integrate with programmatically |
| **Implementation effort** | Very High (no API) -- would require a custom arrangement with the carrier or web scraping (if a portal exists behind authentication) |
| **DCSA base adapter usable?** | No -- not applicable. No API of any kind exists |

### Recommended Approach

Direct API integration with Maruba is not feasible. The carrier has no public API, no developer portal, no documented EDI connectivity, and no aggregator coverage. Any data from Maruba shipments would need to come through:

1. **Manual data entry**: SSL staff manually entering tracking updates based on email/phone communications from Maruba.
2. **Custom arrangement**: Negotiating a data exchange mechanism directly with Maruba (potentially email-based status reports, shared spreadsheets, or a future EDI connection).
3. **Future reassessment**: If Maruba develops an ecommerce portal with tracking capabilities (the ecom.maruba.com.ar domain suggests intent), reassess for web scraping or API possibilities.

Given the carrier's regional focus and the likely small volume of SSL shipments on Maruba routes, manual tracking may be the most pragmatic approach.

### Recommended Lookup Method

N/A -- no programmatic lookup is available.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | N/A -- no API to poll |
| **Incremental filter** | N/A |
| **Batch tracking** | N/A |

### Auth Implementation Notes

N/A -- no authentication required as no API exists.

### Edge Cases to Handle

- **No data source**: The primary edge case is the complete absence of a data source. Any adapter for Maruba would need to handle the "no data available" state gracefully.
- **Manual data integration**: If SSL manually enters Maruba tracking data, the adapter would need to accept manually-sourced data alongside API-sourced data from other carriers.

### Mapping Complexity

N/A -- there are no carrier-specific fields to map since no API or data feed exists. If Maruba eventually provides data through any mechanism, mapping complexity would depend entirely on the format they choose.

---

## Open Questions

- [ ] Does Maruba's ecom.maruba.com.ar portal provide container tracking capabilities behind authentication?
- [ ] Does SSL have an existing business relationship with Maruba?
- [ ] Does Maruba support EDI (EDIFACT) for any data exchange with customers or partners?
- [ ] Is Maruba connected to any regional aggregator platforms serving South American carriers?
- [ ] Does Maruba plan to develop public API or digital tracking capabilities?
- [ ] What is the typical volume of SSL shipments on Maruba routes? (Determines whether manual tracking is viable)

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | https://www.maruba.com.ar |
| Carrier Website (English) | https://www.maruba.com.ar/en/ |
| Services Page | https://www.maruba.com.ar/en/services/ |
| Ecommerce Portal (expired cert) | https://ecom.maruba.com.ar/ |
| LinkedIn | https://www.linkedin.com/company/maruba |
| shipping-data.com Profile | https://shipping-data.com/tracktrace/container/maruba |
| SCAC Code Reference | https://www.safround.com/en/ocean-carrier-scac-code-list |
| Anchor Shipping Agency Profile | https://anchorshipping.com/aboutus/maruba.shtml |
