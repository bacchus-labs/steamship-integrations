# Independent Container Line (ICL) -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing
> **Researched by**: Agent
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | Independent Container Line Ltd (commonly "ICL") |
| **SCAC Code** | IILU |
| **Parent Company** | Privately held (German-owned); not a subsidiary of a larger shipping group |
| **Alliance** | Independent |
| **Primary Services** | Container shipping (FCL, LCL), warehousing & distribution, cargo insurance, documentation & customs clearance |
| **Market Position** | Niche trans-Atlantic specialist operating a fixed weekly schedule between US East Coast and Northern Europe. Four-vessel fleet (~3,100 TEU each). Known for award-winning delivery reliability and personalized service |
| **Headquarters** | Glen Allen, Virginia, USA (EU office: Antwerp, Belgium; UK office: Liverpool, England) |
| **Website** | https://www.icl-ltd.com |

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | No |
| **Developer portal URL** | N/A |
| **API documentation URL(s)** | N/A -- ICL does not publish a public API |
| **Documentation quality** | None (for APIs) |
| **OpenAPI/Swagger spec available?** | No |
| **Sandbox/test environment?** | No |
| **Developer registration** | N/A |
| **Developer support channels** | General: info@icl-ltd.com; Documentation Supervisor (EU): Leanne.Sumner@icl-ltd.com, +44 151 363 3060 |
| **Community/third-party libraries** | None found for direct ICL integration. Third-party aggregators (Terminal49, Shipsgo, Portcast) provide ICL tracking via their own APIs |
| **API changelog / release notes** | N/A |

### eServices Portal

ICL operates a customer-facing eServices portal at `eservices.icl-ltd.com` (login required). This portal provides:
- FCL and LCL tracking
- Container inquiry and location lookup
- Rate quoting (FCL and LCL)
- Shipping instructions submission
- Verified Gross Mass (VGM) submission
- Booking/shipment requests
- Environmental data reporting
- Tare weight database
- Claims filing

This is a web application for registered customers, not a programmatic API.

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
| **Known DCSA deviations** | N/A -- ICL does not implement DCSA APIs |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Yes | Cross-platform EDI capabilities for shipping instructions. EDI/eServices guide available from ICL |
| **INTTRA integration** | Unknown | ICL documentation references EDI capabilities broadly; explicit INTTRA partnership not confirmed |
| **BIC (Bureau International des Containers)** | Yes | Standard container ID format used |
| **UN/LOCODE** | Yes | Standard port codes for their five ports of call (USCHI, USILM, BEANR, GBSOU, IECOK) |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | N/A -- no public API |
| **Auth documentation** | N/A |
| **Registration process** | N/A for API. eServices portal requires customer account |
| **Registration URL** | https://eservices.icl-ltd.com/Account/Login (customer portal) |
| **Partner program required?** | N/A |
| **Partner program URL** | N/A |
| **Credential type** | N/A |
| **Token refresh supported?** | N/A |
| **Token lifetime** | N/A |
| **Access tiers** | N/A |
| **IP whitelisting required?** | N/A |

### Access Requirements Summary for SSL

ICL does not offer a public API or developer portal. There is no programmatic access to ICL's systems beyond EDI. SSL has two paths to obtain ICL tracking data:

1. **EDI**: ICL supports cross-platform EDI for shipping instructions and cargo tracking. SSL would need to establish an EDI connection, likely via an EDI VAN or direct connection, and negotiate message types with ICL directly.

2. **Third-party aggregators**: Several aggregators (Terminal49, Shipsgo, Portcast) already provide ICL tracking data through their APIs. This is the most practical path for programmatic access to ICL shipment data.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field has a row.
> Availability legend: check = Available | x = Not available | warning = Partial / limited | question = Unknown
>
> **Note**: Since ICL has no public API, coverage is assessed based on what is available through the eServices portal, EDI, and third-party aggregators (primarily Terminal49, which provides the most detailed data documentation for ICL).

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ⚠️ | N/A (web portal only) | Fixed weekly schedule published on website | N/A | ICL publishes schedules on icl-ltd.com. No API. Aggregators (Routescanner, Fluent Cargo) index ICL schedules |
| 1.2 | Point-to-Point Route Options | ❌ | N/A | N/A | N/A | ICL operates a single trans-Atlantic loop with five ports. Route options are effectively fixed |
| 1.3 | Booking Lifecycle | ⚠️ | eServices portal; EDI | Booking request via portal or EDI | N/A | Bookings submitted via eServices portal or EDI. No API for booking lifecycle management |
| 1.4 | Shipping Instructions | ⚠️ | eServices portal; EDI | SI submission via portal or EDI | N/A | EDI and eServices support SI submission. Documentation cutoffs published per-port |
| 1.5 | Rates | ⚠️ | eServices portal (rate quote tool) | FCL/LCL rate quotes | N/A | Rate quotes available via eServices portal login. No programmatic access |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❓ | Unknown | Unknown | `ECP` | Not documented on ICL website or aggregator sources |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❓ | Unknown | Unknown | `EFC` | Not documented on ICL website or aggregator sources |
| 2.3 | Documentation Cutoff | DCO | ✅ | ICL website (published per-port schedule) | Fixed per-port cutoff times | `DCO` | Published on icl-ltd.com/documentation. Antwerp: Mon 14:00; Southampton: Wed 12:00-16:00; Cork: Thu 12:00-16:00; Chester: Mon 14:00; Wilmington: Wed 14:00 |
| 2.4 | VGM Cutoff | VCO | ⚠️ | eServices portal (VGM submission) | VGM submission tool available | `VCO` | ICL eServices portal supports VGM submission. Specific cutoff times for VGM not separately published; likely aligned with cargo cutoffs |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ⚠️ | ICL website (cargo cutoff times) | Cargo cutoff timestamps | `FCO` | ICL publishes cargo cutoff times on their website. DG declarations due earlier (e.g., Chester: Fri 16:00 for Wed sailing) |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ⚠️ | ICL website | LCL-specific cutoffs noted for some ports | `LCO` | Antwerp LCL/specialty cargo: Fri 12:00 (vs. FCL Mon 14:00). Other ports not explicitly separated |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ❓ | Unknown | Unknown | Inferred from first EquipmentEvent | Not documented. May be available via EDI or eServices portal |
| 3.2 | Empty Container Gate-Out (Pickup) | ✅ | Terminal49 aggregator | "Empty Out" milestone | `GTOT` + `EMPTY` | Terminal49 confirms "Empty Out" milestone available for ICL via their API |
| 3.3 | Full Container Gate-In | ✅ | Terminal49 aggregator | "Full In" milestone | `GTIN` + `LADEN` | Terminal49 confirms "Full In" milestone available for ICL |
| 3.4 | Container Loaded on Vessel | ✅ | Terminal49 aggregator | Vessel loading/departure milestone | `LOAD` + `LADEN` | Terminal49 confirms vessel loading milestone available |
| 3.5 | Container Discharged at Transshipment | ❌ | N/A | N/A | `DISC` + `LADEN` + transshipment | ICL operates a direct service with no transshipment. Not applicable for standard ICL routings |
| 3.6 | Container Loaded at Transshipment | ❌ | N/A | N/A | `LOAD` + `LADEN` + transshipment | ICL operates a direct service with no transshipment. Not applicable for standard ICL routings |
| 3.7 | Container Discharged at Destination | ✅ | Terminal49 aggregator | Vessel arrival + vessel discharge milestones | `DISC` + `LADEN` | Terminal49 confirms vessel arrival and discharge milestones available |
| 3.8 | Full Container Gate-Out (Delivery) | ✅ | Terminal49 aggregator | "Full Out" milestone | `GTOT` + `LADEN` | Terminal49 confirms "Full Out" milestone available |
| 3.9 | Empty Container Returned | ✅ | Terminal49 aggregator | "Empty Returned" milestone | `GTIN` + `EMPTY` | Terminal49 confirms "Empty Returned" milestone available |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ✅ | Terminal49 aggregator; ICL website (schedule) | Estimated and actual departure times at POL | `DEPA` + classifier | Terminal49 confirms estimated and actual departure times available |
| 4.2 | Estimated Time of Arrival | ETA | ✅ | Terminal49 aggregator; ICL website (schedule) | Estimated and actual arrival times at POD | `ARRI` + classifier | Terminal49 confirms estimated and actual arrival times available |
| 4.3 | Vessel Arrival at Transshipment | -- | ❌ | N/A | N/A | `ARRI` at intermediate | Not applicable -- ICL operates direct services without transshipment |
| 4.4 | Vessel Departure from Transshipment | -- | ❌ | N/A | N/A | `DEPA` at intermediate | Not applicable -- ICL operates direct services without transshipment |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❌ | ICL does not offer webhooks. Terminal49 and Shipsgo provide webhook-like notifications on top of ICL data |
| Event Polling with timestamp filter | ❌ | No direct API to poll. Third-party aggregators support polling for ICL shipments |
| Event Classifier Progression (PLN->EST->ACT) | ⚠️ | Terminal49 provides estimated vs actual timestamps for departure/arrival, enabling progression tracking. Not available directly from ICL |
| Retracted Events | ❌ | No mechanism documented |
| Change Remarks | ❌ | No mechanism documented |
| Delay Reason Codes | ❌ | No mechanism documented |

### Coverage Summary

| Category | Fields Available | Fields Partial | Fields Unavailable | Fields Unknown | Coverage % |
|----------|-----------------|---------------|-------------------|----------------|-----------|
| API Domains (1.x) | 0/5 | 4/5 | 1/5 | 0/5 | 0% confirmed (4 partial via portal/EDI) |
| Cutoffs (2.x) | 1/6 | 3/6 | 0/6 | 2/6 | 17% (+ 3 partial) |
| Container Milestones (3.x) | 6/9 | 0/9 | 2/9 | 1/9 | 67% (via aggregator) |
| Transport Events (4.x) | 2/4 | 0/4 | 2/4 | 0/4 | 50% (2 N/A due to no transshipment) |
| Change Detection (5.x) | 0/6 | 1/6 | 5/6 | 0/6 | 0% (+ 1 partial via aggregator) |
| **Total** | **9/30** | **8/30** | **10/30** | **3/30** | **30% confirmed (27% partial, 10% unknown)** |

> **Notes on Coverage:**
> - ICL has no public API, so "available" fields are only those accessible via third-party aggregators (Terminal49, Shipsgo, Portcast) or published on ICL's website.
> - Container milestone coverage via Terminal49 is strong (6 of 9 milestones confirmed), making aggregator integration the clear path for tracking data.
> - Transshipment events (3.5, 3.6, 4.3, 4.4) are marked unavailable because ICL operates a direct trans-Atlantic loop without transshipment. These are structurally not applicable rather than a data gap.
> - Cutoff data is partially available: DCO is published per-port on the ICL website (static schedule), but programmatic access to dynamic cutoffs requires EDI or the eServices portal.
> - Change detection is essentially unavailable from ICL directly. Aggregators provide some event progression tracking.

---

## Endpoint Reference

ICL does not expose any public API endpoints. All programmatic access to ICL data must go through third-party aggregators or EDI.

### Lookup Methods Summary (via Third-Party Aggregators)

| Identifier Type | Supported? | Which Aggregators? | Notes |
|----------------|-----------|-------------------|-------|
| **Bill of Lading (B/L) number** | ✅ | Terminal49, Shipsgo, Portcast, GoComet | Primary lookup method. Terminal49 confirms B/L tracking for IILU |
| **Booking reference** | ❌ (Terminal49) / ✅ (others) | Portcast, Shipsgo | Terminal49 reports booking number lookup as unsupported for IILU. Portcast and Shipsgo claim support |
| **Container number** | ❌ (Terminal49) / ✅ (others) | Shipsgo, Portcast | Terminal49 reports container number lookup as unsupported for IILU. Shipsgo and Portcast claim support |
| **Carrier booking number** | ❓ | Unknown | May be same as booking reference |
| **Vessel IMO / voyage** | ❌ | N/A | Not supported as a tracking lookup |

---

## Rate Limits & Quotas

N/A -- ICL does not offer a public API. Rate limits would be governed by whichever third-party aggregator is used for integration.

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | https://eservices.icl-ltd.com (login required); also via aggregators without login |
| **Login required?** | Yes (eServices portal requires customer account) |
| **Data available on portal but NOT in API** | All tracking data is portal-only from ICL's side: container status, location, ETAs, cutoffs, booking details, rate quotes, VGM submission, shipping instructions |
| **Scraping feasibility** | Not assessed -- login-gated portal. Aggregator integration preferred |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Yes |
| **EDI message types** | Shipping instructions (likely IFTMIN), cargo tracking/status (likely IFTSTA). ICL references "cross-platform EDI capabilities" with an EDI/eServices guide available |
| **EDI connection method** | Unknown -- EDI guide available from ICL upon request |
| **EDI documentation** | EDI/eServices guide downloadable from icl-ltd.com/documentation; contact Leanne.Sumner@icl-ltd.com |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Unknown | Not explicitly confirmed for ICL. project44 covers 85+ ocean carriers but ICL is a niche carrier |
| **FourKites** | Unknown | No explicit confirmation found |
| **Vizion** | Unknown | Vizion claims 99%+ ocean freight coverage; ICL may be included but not explicitly confirmed |
| **INTTRA / E2open** | Unknown | ICL has EDI capabilities but explicit INTTRA partnership not confirmed |
| **CargoSmart** | Unknown | No explicit confirmation found |
| **Terminal49** | Yes | Confirmed. IILU listed with B/L tracking, POL/POD data, container milestones (Empty Out, Full In, Load, Discharge, Full Out, Empty Returned), ETD/ETA |
| **Shipsgo** | Yes | Confirmed. ICL tracking via container, booking, or B/L number with real-time updates and ETAs |
| **Portcast** | Yes | Confirmed. Real-time and predictive tracking for ICL with AI-powered ETA predictions. API available |
| **GoComet** | Yes | Confirmed. ICL container tracking by B/L number |
| **OpenTrack** | Yes | Confirmed. ICL tracking support documented in their help center |

> **Aggregator note:** Since ICL has no public API, aggregator integration is the only practical path for programmatic tracking. Terminal49 provides the most detailed milestone data for ICL, including Empty Out, Full In, vessel loading/departure, vessel arrival/discharge, Full Out, and Empty Returned. Portcast adds predictive ETA capabilities. The aggregator approach also normalizes ICL data alongside other carriers, reducing adapter complexity.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown from ICL directly. Terminal49 claims "refreshed within minutes" for carrier and terminal events | Terminal49 website |
| **API uptime/reliability** | N/A -- no direct API. Aggregator reliability depends on the chosen platform | N/A |
| **Historical data depth** | Unknown | Unknown |
| **Timezone handling** | Unknown from ICL. Documentation cutoffs published in local port time. Terminal49 provides timezone data per port | ICL website, Terminal49 |
| **Character encoding** | N/A -- no direct API | N/A |

### Known Issues & Gotchas

- **No public API**: ICL is entirely portal/EDI/aggregator-dependent. Any direct integration requires EDI setup or aggregator subscription.

- **Single trade lane**: ICL operates only the trans-Atlantic route (Antwerp - Southampton - Cork - Chester PA - Wilmington NC). Transshipment milestones are not applicable.

- **Four-vessel fleet**: With only four vessels (~3,100 TEU each) on a single weekly rotation, tracking volume is inherently limited compared to major carriers.

- **Aggregator lookup inconsistencies**: Terminal49 reports that booking number and container number lookups are unsupported for IILU, while Shipsgo and Portcast claim support for these identifiers. B/L lookup is consistently supported across aggregators.

- **Static cutoff schedule**: Documentation and cargo cutoffs are published as a fixed per-port schedule on the ICL website, not as dynamic per-sailing values. Actual cutoffs may vary and would need to be confirmed per booking.

- **World Shipping Council / CTPAT certified**: ICL is a World Shipping Council member and CTPAT-certified, indicating compliance with trade security standards.

### Recently Deprecated or Changed

- No deprecation notices found. ICL's digital ecosystem has remained stable with the eServices portal as the primary customer interface.

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | Partial -- via aggregator only. ICL has no public API, so a direct adapter is not possible. An aggregator-mediated adapter (Terminal49, Portcast, or Shipsgo) can provide tracking milestones, ETD/ETA, and container status |
| **Implementation effort** | Low (aggregator passthrough) -- if using an aggregator like Terminal49 that already normalizes ICL data. Medium if using EDI |
| **DCSA base adapter usable?** | No -- ICL has no DCSA implementation. The aggregator adapter pattern would be used instead |

### Recommended Approach

The ICL adapter should be implemented as an **aggregator-mediated adapter** rather than a direct carrier integration, since ICL has no public API.

1. **Primary data source: Terminal49 or Portcast API**. Terminal49 provides confirmed coverage for ICL (IILU) with B/L tracking, ETD/ETA, and key container milestones (Empty Out, Full In, Load, Arrival, Discharge, Full Out, Empty Returned). Portcast adds predictive ETA capabilities. Choose based on existing aggregator relationships and pricing.

2. **Aggregator adapter pattern**: Build a generic aggregator adapter that handles Terminal49/Portcast/Shipsgo API calls and maps their normalized response format to the canonical DCSA-based data model. This adapter can serve multiple niche carriers that lack direct APIs.

3. **Cutoff data supplementation**: Since aggregators may not provide cutoff data, supplement with ICL's published per-port cutoff schedule (static mapping) or establish an EDI connection for dynamic cutoff data.

### Recommended Lookup Method

**Bill of Lading (B/L) number** is the recommended lookup method. It is the only identifier consistently supported across all aggregators for ICL (IILU). Terminal49 explicitly notes that booking number and container number lookups are not supported for IILU.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Every 4-6 hours for in-transit shipments. ICL's weekly sailing schedule means events change slowly. Governed by aggregator rate limits |
| **Incremental filter** | Depends on aggregator API capabilities. Terminal49 supports webhook notifications for milestone changes, reducing polling needs |
| **Batch tracking** | Depends on aggregator. Terminal49 supports bulk tracking via CSV upload and API. One aggregator API call per shipment for real-time queries |

### Auth Implementation Notes

Authentication depends entirely on the chosen aggregator:
- **Terminal49**: API key authentication
- **Portcast**: API key authentication (requires scheduling a consultation call for access)
- **Shipsgo**: API key authentication

No ICL-specific authentication is needed since there is no direct API.

### Edge Cases to Handle

- **No transshipment**: ICL operates direct services. The adapter should handle the absence of transshipment events (3.5, 3.6, 4.3, 4.4) gracefully rather than flagging them as missing data.

- **Lookup method restrictions**: If using Terminal49, only B/L lookup is supported for ICL. The adapter must reject or translate booking/container number lookups for this carrier.

- **Static vs dynamic cutoffs**: ICL's published cutoff times are a fixed schedule (e.g., "Monday 14:00 for Wednesday sailing"). These need to be computed relative to the specific sailing date, not fetched dynamically from an API.

- **Small fleet identification**: ICL has only four vessels (Independent Primero, Independent Future, Independent Horizon, Independent Quest) all with IMO numbers. Vessel identification should be straightforward.

### Mapping Complexity

**Low complexity (via aggregator).** Since the adapter would consume pre-normalized data from an aggregator like Terminal49 rather than raw ICL data, the mapping effort is minimal:

1. **Aggregator-to-canonical mapping**: Terminal49 and similar platforms already normalize carrier data. The mapping is from the aggregator's format to SSL's canonical model, which is a one-time effort that benefits all carriers covered by that aggregator.

2. **Milestone mapping**: Terminal49's milestone names ("Empty Out", "Full In", etc.) map directly to DCSA event codes (GTOT+EMPTY, GTIN+LADEN, etc.).

3. **No event code discovery needed**: Unlike direct API integrations where proprietary event codes must be reverse-engineered, aggregator data is already classified.

4. **Cutoff mapping is the only manual effort**: ICL's published cutoff schedule needs to be encoded as a static configuration and updated when ICL changes their cutoff times.

---

## Open Questions

- [ ] Does SSL have an existing relationship with any aggregator (Terminal49, Portcast, Shipsgo) that covers ICL?
- [ ] Does ICL provide tracking data via EDI (IFTSTA messages)? If so, what events are included?
- [ ] Can ICL's eServices portal be accessed programmatically (e.g., does it have an underlying API that could be used)?
- [ ] Does ICL plan to develop a public API in the future?
- [ ] Are dynamic per-sailing cutoff times available via EDI, or are the published per-port schedules the only cutoff data?
- [ ] Does project44 or Vizion cover ICL (IILU)? These are the largest aggregators but explicit ICL coverage was not confirmed
- [ ] What is the actual data freshness for ICL events via aggregators? How quickly do physical events appear?

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | https://www.icl-ltd.com |
| About ICL | https://www.icl-ltd.com/about-icl |
| ICL Ports of Call | https://www.icl-ltd.com/our-ports |
| ICL Vessels | https://www.icl-ltd.com/our-vessels |
| ICL Documentation & Cutoffs | https://www.icl-ltd.com/documentation |
| ICL Fixed Weekly Schedule | https://www.icl-ltd.com/fixed-weekly-schedule |
| eServices Portal (login required) | https://eservices.icl-ltd.com |
| Terminal49 ICL Tracking | https://terminal49.com/shipping-lines/iilu-independent-container-line-container-tracking |
| Shipsgo ICL Tracking | https://shipsgo.com/ocean/carriers/icl/container-tracking |
| Portcast ICL Tracking | https://www.portcast.io/carrier-coverage/icl-independent-container-line-tracking |
| Fluent Cargo ICL Schedules (SCAC: IILU) | https://www.fluentcargo.com/carriers/scac/IILU |
| Routescanner ICL Schedules | https://www.routescanner.com/partners/ICL |
| OpenTrack ICL Tracking | https://support.opentrack.co/en/articles/9661894-tracking-independent-container-lines-icl |
| SeaRates ICL Tracking | https://www.searates.com/sealine/icl |
| GoComet ICL Tracking | https://www.gocomet.com/online-container-tracking/carriers/independent-container-line |
