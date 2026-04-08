# PT. Andalan Pacific Samudra -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing
> **Researched by**: Agent
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | PT. Andalan Pacific Samudra (commonly "APS") |
| **SCAC Code** | Unknown -- not published; company is a freight forwarder, not a vessel-operating common carrier |
| **Parent Company** | Independent |
| **Alliance** | Independent -- not a member of any shipping alliance |
| **Primary Services** | Freight forwarding (ocean and air freight), door-to-door delivery, inland trucking, warehousing, customs brokerage, distribution/packing |
| **Market Position** | Regional freight forwarder based in Indonesia with branch offices at major Indonesian ports. Not a vessel-operating shipping line |
| **Headquarters** | Surabaya, East Java, Indonesia |
| **Website** | http://www.andalan-pacific.com/ |

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
| **Developer support channels** | General contact: info@andalan-pacific.com, phone: +62 31 3293 898 |
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
| **Known DCSA deviations** | N/A -- no APIs exist |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Unknown | No EDI capability documented. As a small regional forwarder, EDI is unlikely |
| **INTTRA integration** | Unknown | No INTTRA integration documented |
| **BIC (Bureau International des Containers)** | Unknown | No information available |
| **UN/LOCODE** | Unknown | No information available |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | N/A -- no API exists |
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

PT. Andalan Pacific Samudra does not operate any APIs, developer portals, or digital integration tools. The company is a regional Indonesian freight forwarder (not a vessel-operating shipping line) with a basic informational website. There is no programmatic access method available.

SSL cannot integrate with this company via API. Any data exchange would need to occur through manual communication (email/phone) or through the actual vessel-operating carriers that APS books cargo with on behalf of its clients.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field has a row.
> Availability legend: check = Available | x = Not available | warning = Partial / limited | question = Unknown

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | N/A | N/A | N/A | N/A | No API exists. APS is a freight forwarder, not a shipping line |
| 1.2 | Point-to-Point Route Options | N/A | N/A | N/A | N/A | No API exists |
| 1.3 | Booking Lifecycle | N/A | N/A | N/A | N/A | No API exists |
| 1.4 | Shipping Instructions | N/A | N/A | N/A | N/A | No API exists |
| 1.5 | Rates | N/A | N/A | N/A | N/A | No API exists |

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
> PT. Andalan Pacific Samudra is a regional Indonesian freight forwarder, not a vessel-operating shipping line. The company does not operate any APIs, tracking portals, or digital integration tools. All 30 fields are marked N/A (counted as unavailable) because no programmatic data source exists. Tracking of shipments booked through APS would need to be done through the underlying vessel-operating carriers (e.g., the actual shipping lines APS books with).

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | None -- the website (http://www.andalan-pacific.com/) is informational only with no tracking functionality |
| **Login required?** | N/A |
| **Data available on portal but NOT in API** | N/A -- no portal or API exists |
| **Scraping feasibility** | Not applicable -- no tracking portal to scrape |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | No -- no evidence of EDI capability |
| **EDI message types** | N/A |
| **EDI connection method** | N/A |
| **EDI documentation** | N/A |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | No | APS is not a vessel-operating carrier; not listed on project44 |
| **FourKites** | No | APS is not a vessel-operating carrier; not listed on FourKites |
| **Vizion** | No | APS is not a vessel-operating carrier; not listed on Vizion |
| **INTTRA / E2open** | No | No evidence of INTTRA/E2open integration |
| **CargoSmart** | No | No evidence of CargoSmart integration |

> **Aggregator note:** Third-party tracking aggregators cover vessel-operating shipping lines, not freight forwarders like APS. Shipments booked through APS would be trackable through the aggregators only via the underlying vessel-operating carrier's B/L or container number.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | N/A -- no API | N/A |
| **API uptime/reliability** | N/A -- no API | N/A |
| **Historical data depth** | N/A -- no API | N/A |
| **Timezone handling** | N/A -- no API | N/A |
| **Character encoding** | N/A -- no API | N/A |

### Known Issues & Gotchas

- **Not a shipping line**: PT. Andalan Pacific Samudra is a freight forwarder, not a vessel-operating common carrier. It does not operate vessels, publish schedules, or issue ocean Bills of Lading under its own authority. The company books cargo on behalf of its clients with actual vessel-operating shipping lines.

- **No digital infrastructure**: The company website is a basic informational page with no tracking, booking, or API capabilities. There is no evidence of any digital integration tools, EDI connections, or third-party platform participation.

- **Panjiva trade data**: Panjiva records show 395 US-bound shipment records (2007-present) primarily involving handicrafts, furniture, plastics, and wood products. This suggests APS acts as a shipper/exporter or booking agent rather than a carrier.

- **May be confused with other "Samudra" companies**: Indonesia has several shipping/logistics companies with "Samudra" in their name, including PT. Samudera Indonesia Tbk (a major shipping line with SCAC code SAMU), PT. Andalan Samudera Mandiri, and PT. Benua Andalan Samudera. These are separate entities.

### Recently Deprecated or Changed

- N/A -- no API has ever existed for this company.

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | No -- APS does not operate any APIs, tracking systems, or digital integration points. The company is a freight forwarder, not a shipping line |
| **Implementation effort** | N/A -- no adapter possible |
| **DCSA base adapter usable?** | N/A |

### Recommended Approach

No adapter can or should be built for PT. Andalan Pacific Samudra. The company is a regional Indonesian freight forwarder that arranges shipments through vessel-operating shipping lines but does not itself operate vessels, APIs, or tracking systems.

If SSL needs to track shipments that were booked through APS, the correct approach is to identify the underlying vessel-operating carrier (the shipping line whose vessel actually carries the cargo) and use that carrier's API or a third-party aggregator. The carrier can be identified from the ocean Bill of Lading, which will show the vessel-operating carrier's name and SCAC code, not APS's.

APS should be reclassified in the carrier index as a freight forwarder rather than a shipping line, or removed from the integration target list entirely.

### Recommended Lookup Method

N/A -- no API exists. For shipments booked through APS, look up tracking through the underlying vessel-operating carrier using the ocean B/L number or container number.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | N/A |
| **Incremental filter** | N/A |
| **Batch tracking** | N/A |

### Auth Implementation Notes

N/A -- no API exists.

### Edge Cases to Handle

- N/A -- no adapter to build.

### Mapping Complexity

N/A -- no data to map.

---

## Open Questions

- [ ] Why is PT. Andalan Pacific Samudra listed as a carrier in the steamship lines index? It appears to be a freight forwarder, not a vessel-operating shipping line. Should it be reclassified or removed?
- [ ] Does SSL have a business relationship with APS? If so, what is the nature of the relationship (APS as a booking agent, sub-contractor, etc.)?
- [ ] If APS is used as a booking agent, which vessel-operating carriers does APS typically book with? Those carriers' APIs would be the actual integration targets.

---

## Source Links

| Resource | URL |
|----------|-----|
| Company Website | http://www.andalan-pacific.com/ |
| Panjiva Trade Profile | https://panjiva.com/PT-Andalan-Pacific-Samudra/1764696 |
| InfoPelaut Company Profile | https://infopelaut.com/daftar-perusahaan-pelayaran/andalan-pacific-samudra-pt/ |
| Maritime Union Listing | https://maritime-union.com/company/pt-andalan-pacific-samudra |
