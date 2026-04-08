# Pasha Hawaii Transport Lines -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing
> **Researched by**: Agent
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | Pasha Hawaii Transport Lines (commonly "Pasha Hawaii") |
| **SCAC Code** | PSHI |
| **Parent Company** | The Pasha Group |
| **Alliance** | Independent (Jones Act carrier -- US-flag domestic trade) |
| **Primary Services** | Container shipping, RoRo/ConRo (vehicles), oversize/heavy cargo, household goods -- US Mainland to Hawaii |
| **Market Position** | Jones Act carrier specializing in US mainland-to-Hawaii domestic trade. One of three major carriers on this lane alongside Matson and defunct Horizon Lines (acquired by Pasha in 2015) |
| **Headquarters** | Honolulu, Hawaii, USA (parent Pasha Group in San Rafael, CA) |
| **Website** | https://www.pashahawaii.com |

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | No |
| **Developer portal URL** | N/A |
| **API documentation URL(s)** | N/A -- no public API documentation exists |
| **Documentation quality** | None |
| **OpenAPI/Swagger spec available?** | No |
| **Sandbox/test environment?** | No |
| **Developer registration** | N/A |
| **Developer support channels** | EDI integration inquiries: Integrations@pashanet.com, (415) 927-6378 |
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
| **Known DCSA deviations** | N/A -- Pasha Hawaii does not implement DCSA APIs |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Yes | Supports UN/EDIFACT standard transportation and logistics messages |
| **ANSI X12 (EDI)** | Yes | Supports many ANSI X12 standard transportation and logistics messages including Booking, Shipping Instructions, Container Status, Freight Invoices, Vessel Schedules, 322 Terminal Operations |
| **INTTRA integration** | Unknown | No evidence of INTTRA partnership found |
| **BIC (Bureau International des Containers)** | Unknown | Standard container ID format likely used but not confirmed |
| **UN/LOCODE** | Unknown | Not confirmed |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | N/A -- no public API |
| **Auth documentation** | N/A |
| **Registration process** | N/A for API. For EDI: contact Integrations@pashanet.com |
| **Registration URL** | N/A |
| **Partner program required?** | N/A for API. EDI integration requires direct engagement with Pasha's integration team |
| **Partner program URL** | N/A |
| **Credential type** | N/A |
| **Token refresh supported?** | N/A |
| **Token lifetime** | N/A |
| **Access tiers** | N/A |
| **IP whitelisting required?** | N/A |

### Access Requirements Summary for SSL

Pasha Hawaii does not offer a public REST/SOAP API for tracking, booking, or schedules. There is no developer portal and no documented API endpoints. The carrier's digital integration capability is limited to EDI (ANSI X12 and UN/EDIFACT) and proprietary XML/flat file formats, with connectivity via FTP, Secure FTP, Web Services, Value Added Networks, and email.

Pasha Hawaii's EDI page states they "can support APIs of all standard communication protocols (SOAP and REST)" but this appears to refer to custom bilateral integrations arranged through their integration team (Integrations@pashanet.com) rather than a publicly available API. SSL would need to contact Pasha Hawaii directly to negotiate a custom EDI or API integration, which would likely require a business relationship and bilateral agreement.

For tracking data specifically, the most practical path may be through third-party aggregators (ShipsGo, Portcast) or web portal scraping, rather than a direct API integration.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field has a row.
> Availability legend: check = Available | x = Not available | warning = Partial / limited | question = Unknown

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ❌ | N/A (no API) | N/A | N/A | Vessel schedules available on web portal only. EDI vessel schedule messages (ANSI X12) supported for EDI partners |
| 1.2 | Point-to-Point Route Options | ❌ | N/A (no API) | N/A | N/A | Fixed trade lane (US Mainland to Hawaii) with limited routing. Schedule info on web portal only |
| 1.3 | Booking Lifecycle | ❌ | N/A (no API) | N/A | N/A | Booking via web portal, phone, or EDI (Booking Request/Confirmation/Cancellation messages). No REST API |
| 1.4 | Shipping Instructions | ❌ | N/A (no API) | N/A | N/A | Shipping Instructions available via EDI only (ANSI X12 / UN/EDIFACT) |
| 1.5 | Rates | ❌ | N/A (no API) | N/A | N/A | Rates available via web portal tariff tool and quote request form. No rate API |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❌ | N/A | N/A | `ECP` | No API access. May be communicated via EDI or portal |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❌ | N/A | N/A | `EFC` | No API access |
| 2.3 | Documentation Cutoff | DCO | ❌ | N/A | N/A | `DCO` | No API access. Likely communicated in booking confirmation |
| 2.4 | VGM Cutoff | VCO | ❌ | N/A | N/A | `VCO` | No API access. SOLAS VGM requirement applies |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ❌ | N/A | N/A | `FCO` | No API access. Cutoffs communicated via booking confirmation and EDI |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❌ | N/A | N/A | `LCO` | No API access |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ❌ | N/A | N/A | Inferred from first EquipmentEvent | No API. Web portal tracking may show assignment |
| 3.2 | Empty Container Gate-Out (Pickup) | ❌ | N/A | N/A | `GTOT` + `EMPTY` | No API. EDI Container Shipment Status messages may include this milestone |
| 3.3 | Full Container Gate-In | ❌ | N/A | N/A | `GTIN` + `LADEN` | No API. EDI status messages may include gate-in events |
| 3.4 | Container Loaded on Vessel | ❌ | N/A | N/A | `LOAD` + `LADEN` | No API. Web portal tracking shows loading status |
| 3.5 | Container Discharged at Transshipment | ❌ | N/A | N/A | `DISC` + `LADEN` + transshipment | N/A -- Pasha Hawaii operates direct services (no transshipment) on the US-Hawaii lane |
| 3.6 | Container Loaded at Transshipment | ❌ | N/A | N/A | `LOAD` + `LADEN` + transshipment | N/A -- no transshipment in Pasha Hawaii's service model |
| 3.7 | Container Discharged at Destination | ❌ | N/A | N/A | `DISC` + `LADEN` | No API. Web portal tracking shows discharge |
| 3.8 | Full Container Gate-Out (Delivery) | ❌ | N/A | N/A | `GTOT` + `LADEN` | No API. Web portal shows delivery status |
| 3.9 | Empty Container Returned | ❌ | N/A | N/A | `GTIN` + `EMPTY` | No API. EDI status messages may include empty return |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ❌ | N/A | N/A | `DEPA` + classifier | No API. Vessel schedules available on web portal and via EDI |
| 4.2 | Estimated Time of Arrival | ETA | ❌ | N/A | N/A | `ARRI` + classifier | No API. Available on web portal and via EDI |
| 4.3 | Vessel Arrival at Transshipment | -- | ❌ | N/A | N/A | `ARRI` at intermediate | N/A -- no transshipment on US-Hawaii route |
| 4.4 | Vessel Departure from Transshipment | -- | ❌ | N/A | N/A | `DEPA` at intermediate | N/A -- no transshipment on US-Hawaii route |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❌ | No webhook or push notification system |
| Event Polling with timestamp filter | ❌ | No API to poll |
| Event Classifier Progression (PLN->EST->ACT) | ❌ | No event classifier system |
| Retracted Events | ❌ | No event system |
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
> - Pasha Hawaii has no public REST or SOAP API. All 30 fields are unavailable via API.
> - The carrier does support EDI (ANSI X12 and UN/EDIFACT) which can provide booking, shipping instructions, container status, vessel schedules, and freight invoices to integrated partners. However, EDI requires bilateral setup and is not a web API.
> - The web portal at pashahawaii.com provides tracking (container, vehicle, household goods, oversize cargo), booking, scheduling, and tariff information -- but this is a browser-based interface, not a programmatic API.
> - Pasha Hawaii's EDI page mentions ability to "support APIs of all standard communication protocols (SOAP and REST)" suggesting a custom API could potentially be negotiated, but nothing is publicly available or documented.
> - Third-party aggregators (ShipsGo, Portcast, SeaRates) offer Pasha Hawaii tracking, likely via scraping or EDI data feeds.

---

## Endpoint Reference

Pasha Hawaii does not expose any public API endpoints. This section is intentionally omitted.

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | https://www.pashahawaii.com/tracking (main); https://www.pashahawaiishipping.com/public/track.htm (legacy) |
| **Login required?** | Yes -- container tracking requires login at https://www.pashahawaiishipping.com/cgi-pas/login.pgm |
| **Data available on portal but NOT in API** | All tracking data is portal-only: container status, location, vessel/voyage, ETD/ETA, milestone events. No API exists |
| **Scraping feasibility** | Difficult -- login-gated portal with legacy CGI-based system. Tracking alerts can be configured through the portal |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Yes |
| **EDI message types** | Vessel Schedules, Booking Request/Confirmation/Cancellation, Shipping Instructions, Container Shipment Status Details (Ocean and Trucking), Freight Invoices, Functional Acknowledgements, 322 Terminal Operations Update Messages. Supports ANSI X12 and UN/EDIFACT standards plus proprietary XML and Flat File formats |
| **EDI connection method** | FTP, Secure FTP, Web Services, Value Added Networks, Email |
| **EDI documentation** | Contact Integrations@pashanet.com or (415) 927-6378 |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Unknown | Pasha Hawaii not found in project44's publicly listed ocean carriers. Likely not covered given niche domestic trade focus |
| **FourKites** | Unknown | No evidence of Pasha Hawaii coverage found |
| **Vizion** | Unknown | No explicit confirmation of Pasha Hawaii coverage. Vizion claims broad coverage but Pasha Hawaii is a niche domestic carrier |
| **INTTRA / E2open** | Unknown | No evidence of INTTRA partnership found |
| **CargoSmart** | Unknown | No evidence of CargoSmart integration found |
| **Portcast** | Yes | Portcast lists Pasha Hawaii container tracking coverage (by B/L, container number, or booking number) |
| **ShipsGo** | Yes | ShipsGo offers Pasha Hawaii container tracking API integration |
| **SeaRates** | Yes | SeaRates provides Pasha Hawaii container tracking |

> **Aggregator note:** Given that Pasha Hawaii has no public API, third-party aggregators (particularly ShipsGo and Portcast) are the most viable path for programmatic tracking data. These aggregators likely obtain data via web scraping of Pasha Hawaii's portal or EDI data feeds. The major enterprise aggregators (project44, Vizion, FourKites) do not appear to cover Pasha Hawaii, likely because it is a niche Jones Act domestic carrier rather than a global ocean carrier.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown -- no API to measure | Unknown |
| **API uptime/reliability** | N/A -- no API | N/A |
| **Historical data depth** | Unknown | Unknown |
| **Timezone handling** | Unknown -- likely US Pacific or Hawaii time given trade lane | Estimated |
| **Character encoding** | Unknown | Unknown |

### Known Issues & Gotchas

- **No public API exists**: This is the primary constraint. Pasha Hawaii is a traditional shipping line with web portal and EDI capabilities but no modern REST/SOAP API for external developers.

- **Login-gated tracking portal**: Container tracking on the web portal requires authentication, making even scraping more complex than carriers with public tracking pages.

- **Legacy CGI-based systems**: The tracking system uses legacy CGI scripts (pashahawaiishipping.com/cgi-pas/), suggesting older technology infrastructure that may not be easily API-enabled.

- **Jones Act / domestic trade focus**: As a purely domestic US carrier (mainland-to-Hawaii), Pasha Hawaii has less incentive to adopt international standards like DCSA or build developer APIs compared to global carriers.

- **Limited trade lane**: Pasha Hawaii operates only on the US Mainland to Hawaii route (Long Beach, Oakland to Hawaiian ports). No international routes, no transshipment operations.

- **EDI "API support" claim**: The EDI services page states support for "APIs of all standard communication protocols (SOAP and REST)" but there is no evidence of any publicly available or documented API. This likely refers to custom bilateral integrations arranged on a case-by-case basis.

### Recently Deprecated or Changed

- No deprecation notices found. Pasha Hawaii acquired Horizon Lines' Hawaii business in 2015, consolidating the trade lane.

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | No -- no public API exists. Possible via third-party aggregator (ShipsGo, Portcast) or custom EDI integration, but not direct API |
| **Implementation effort** | Very High (no API) -- would require EDI integration (bilateral negotiation + FTP/SFTP setup) or aggregator integration |
| **DCSA base adapter usable?** | No -- Pasha Hawaii has no DCSA implementation and no API of any kind |

### Recommended Approach

Pasha Hawaii cannot be integrated via direct API since none exists. There are three possible approaches, listed in order of practicality:

1. **Third-party aggregator**: Use ShipsGo or Portcast APIs to obtain Pasha Hawaii tracking data. This is the fastest path to production but depends on the aggregator's data quality and coverage for this carrier. This approach provides tracking only -- no booking, rates, or schedules.

2. **EDI integration**: Negotiate a direct EDI integration with Pasha Hawaii's integration team (Integrations@pashanet.com). This would provide the richest data (booking, status, schedules, invoices) but requires bilateral agreement, FTP/SFTP setup, EDI message parsing (ANSI X12 or UN/EDIFACT), and ongoing maintenance. Implementation timeline would be weeks to months.

3. **Web portal scraping**: Scrape the tracking portal at pashahawaiishipping.com. This is fragile (login-gated, CGI-based, subject to change without notice) and likely violates Pasha Hawaii's terms of service. Not recommended for production use.

Given Pasha Hawaii's niche position (domestic US-Hawaii trade only), the cost-benefit of any integration should be carefully evaluated against the volume of Pasha Hawaii shipments SSL needs to track.

### Recommended Lookup Method

If integrating via a third-party aggregator: **Container number** is the most universally supported lookup method across aggregators like ShipsGo and Portcast. **Bill of Lading number** as secondary.

If integrating via EDI: **Booking reference** for lifecycle tracking from booking through delivery.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Every 4-6 hours via aggregator API. Pasha Hawaii's transit times are short (4 days Long Beach to Honolulu) so more frequent polling near ETD/ETA may be warranted |
| **Incremental filter** | Depends on aggregator capabilities. Full re-fetch likely required |
| **Batch tracking** | Depends on aggregator API. One call per container is typical |

### Auth Implementation Notes

No authentication to implement for Pasha Hawaii directly. Authentication requirements depend on the chosen third-party aggregator (ShipsGo, Portcast, etc.).

### Edge Cases to Handle

- **No transshipment**: Pasha Hawaii operates direct services between the US mainland and Hawaii. Transshipment events (3.5, 3.6, 4.3, 4.4) will never occur and can be excluded from tracking logic.

- **Short transit times**: The 4-day transit from Long Beach to Honolulu means the window for tracking updates is compressed compared to international voyages. Polling frequency should account for this.

- **Multiple cargo types**: Pasha Hawaii handles containers, vehicles, household goods, and oversize cargo. The tracking system differentiates between these. The adapter should filter for container shipments only unless other cargo types are in scope.

- **Domestic trade regulations**: As a Jones Act carrier, Pasha Hawaii operates under different regulatory requirements than international carriers. VGM/SOLAS still applies but customs/manifest requirements differ from international trade.

### Mapping Complexity

**Low mapping complexity (if via aggregator)**: Third-party aggregators like ShipsGo and Portcast provide normalized tracking data that can be mapped to the canonical model. The main simplification is no transshipment events.

**High mapping complexity (if via EDI)**: ANSI X12 EDI messages require parsing fixed-format or delimited records and mapping X12 transaction set fields to the canonical DCSA-based model. EDI message types like IFTSTA (container status) would need field-by-field mapping.

---

## Open Questions

- [ ] Does SSL have significant shipment volume with Pasha Hawaii? -- Determines whether integration is worth the effort
- [ ] Would Pasha Hawaii be willing to set up a custom API/EDI integration for SSL? -- Contact Integrations@pashanet.com to explore
- [ ] What specific tracking data does the Pasha Hawaii web portal display? -- Login-gated so could not be fully assessed during desk research
- [ ] Do ShipsGo or Portcast provide reliable, real-time tracking data for Pasha Hawaii? -- Needs evaluation before committing to aggregator approach
- [ ] What EDI message types does Pasha Hawaii support for Container Shipment Status (X12 315? 304? IFTSTA?) -- Specific transaction sets not documented on website
- [ ] Does the "SOAP and REST" API support mentioned on the EDI page refer to actual available APIs or aspirational capability? -- Clarify with Integrations@pashanet.com

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | https://www.pashahawaii.com |
| Tracking Portal | https://www.pashahawaii.com/tracking |
| Container Tracking | https://www.pashahawaii.com/tracking/container-tracking |
| Legacy Tracking | https://www.pashahawaiishipping.com/public/track.htm |
| EDI Services | https://www.pashahawaii.com/tools/containers/edi-services |
| Container Shipping Overview | https://www.pashahawaii.com/services/containers/container-shipping-overview |
| Pasha Group (Parent) | https://www.pashagroup.com |
| ShipsGo Tracking | https://shipsgo.com/ocean/carriers/pashahawaii/container-tracking |
| Portcast Tracking | https://www.portcast.io/carrier-coverage/pasha-hawaii-container-tracking |
| SeaRates Tracking | https://www.searates.com/sealine/pasha_hawaii |
