# T.S. Lines -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing
> **Researched by**: Agent
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | T.S. Lines Ltd (commonly "TS Lines") |
| **SCAC Code** | TSTU (also referenced as TXZJ on some platforms) |
| **Parent Company** | Independent -- founded by Mr. T.S. Chen |
| **Alliance** | Independent (no major alliance membership) |
| **Primary Services** | Container shipping (intra-Asia specialist, expanding to long-haul) |
| **Market Position** | Regional intra-Asia specialist; one of the largest independent Asian carriers. 46 services covering 22 countries/regions as of Dec 2025. ~24,700 total shipments, ~67,900 TEUs total volume. Fleet of sub-2,000 TEU vessels (avg age 3.5 years). Listed on Hong Kong Stock Exchange in Nov 2024 |
| **Headquarters** | Taipei, Taiwan (established July 2001; Hong Kong listing) |
| **Website** | https://www.tslines.com |

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | No |
| **Developer portal URL** | N/A |
| **API documentation URL(s)** | N/A -- no public API documentation found |
| **Documentation quality** | None -- no API documentation exists |
| **OpenAPI/Swagger spec available?** | No |
| **Sandbox/test environment?** | No |
| **Developer registration** | N/A |
| **Developer support channels** | General contact via tslines.com |
| **Community/third-party libraries** | None found for direct T.S. Lines integration. Third-party aggregator APIs (Shipsgo, Terminal49, Vizion, Portcast) provide tracking data |
| **API changelog / release notes** | N/A |

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | No -- T.S. Lines is not a DCSA member. DCSA members are MSC, Maersk, CMA CGM, Hapag-Lloyd, ONE, Evergreen, Yang Ming, HMM, and ZIM |
| **DCSA APIs implemented** | None |
| **DCSA TNT version** | N/A |
| **DCSA Booking version** | N/A |
| **DCSA Schedules version** | N/A |
| **Known DCSA deviations** | N/A -- T.S. Lines does not implement DCSA APIs |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Unknown | No specific EDI support information found for T.S. Lines |
| **INTTRA integration** | Unknown | No confirmed INTTRA/e2open partnership found |
| **BIC (Bureau International des Containers)** | Yes | Standard container ID format used; container prefixes: TSSU, TXGU, TIIU, MAGU |
| **UN/LOCODE** | Unknown | Web tracking portal uses port names; UN/LOCODE usage not confirmed |

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

T.S. Lines does not offer any public API or developer portal. There is no documented way to programmatically access tracking, booking, or schedule data directly from T.S. Lines. The only direct access is via their web portal at https://www.tslines.com/en/tracking, which provides manual container tracking by B/L number.

To obtain programmatic tracking data for T.S. Lines shipments, SSL would need to use a third-party aggregator such as Vizion (confirmed support, SCAC TSTU), Terminal49 (SCAC TXZJ, B/L tracking only), Shipsgo (SCAC TSTU), or Portcast. Alternatively, SSL could contact T.S. Lines directly to inquire about any private/partner API access that is not publicly documented.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field has a row.
> Availability legend: check = Available | x = Not available | warning = Partial / limited | question = Unknown
>
> **Note:** Since T.S. Lines has no public API, all assessments below are based on data available through their web tracking portal and third-party aggregator capabilities.

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ❌ | N/A | N/A | N/A | No API. Schedules available on web portal only. Third-party aggregators (Routescanner, Fluent Cargo) index TS Lines schedules |
| 1.2 | Point-to-Point Route Options | ❌ | N/A | N/A | N/A | No API. Schedule search available on web portal |
| 1.3 | Booking Lifecycle | ❌ | N/A | N/A | N/A | No API. Booking managed via direct carrier contact or freight forwarder channels |
| 1.4 | Shipping Instructions | ❌ | N/A | N/A | N/A | No API. Manual process |
| 1.5 | Rates | ❌ | N/A | N/A | N/A | No API. Rates obtained via direct negotiation |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❌ | N/A | N/A | `ECP` | No API |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❌ | N/A | N/A | `EFC` | No API |
| 2.3 | Documentation Cutoff | DCO | ❌ | N/A | N/A | `DCO` | No API |
| 2.4 | VGM Cutoff | VCO | ❌ | N/A | N/A | `VCO` | No API |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ❌ | N/A | N/A | `FCO` | No API |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❌ | N/A | N/A | `LCO` | No API |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ❌ | N/A | N/A | Inferred from first EquipmentEvent | No API |
| 3.2 | Empty Container Gate-Out (Pickup) | ❌ | N/A | N/A | `GTOT` + `EMPTY` | No direct API. Terminal49 aggregator reports "Empty out" milestone available via their platform |
| 3.3 | Full Container Gate-In | ❌ | N/A | N/A | `GTIN` + `LADEN` | No direct API. Terminal49 reports "Full in" milestone available |
| 3.4 | Container Loaded on Vessel | ❌ | N/A | N/A | `LOAD` + `LADEN` | No direct API. Terminal49 reports "Vessel loading" available |
| 3.5 | Container Discharged at Transshipment | ❌ | N/A | N/A | `DISC` + `LADEN` + transshipment | No direct API. Terminal49 reports transshipment operations available |
| 3.6 | Container Loaded at Transshipment | ❌ | N/A | N/A | `LOAD` + `LADEN` + transshipment | No direct API. Terminal49 reports transshipment operations available |
| 3.7 | Container Discharged at Destination | ❌ | N/A | N/A | `DISC` + `LADEN` | No direct API. Terminal49 reports vessel discharge available |
| 3.8 | Full Container Gate-Out (Delivery) | ❌ | N/A | N/A | `GTOT` + `LADEN` | No direct API. Terminal49 reports "Full container out" available. Terminal49 notes final destination/delivery data NOT available |
| 3.9 | Empty Container Returned | ❌ | N/A | N/A | `GTIN` + `EMPTY` | No direct API |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ❌ | N/A | N/A | `DEPA` + classifier | No direct API. Terminal49 reports port of lading departure data available |
| 4.2 | Estimated Time of Arrival | ETA | ❌ | N/A | N/A | `ARRI` + classifier | No direct API. Terminal49 reports port of discharge arrival data available. Portcast offers predictive ETA |
| 4.3 | Vessel Arrival at Transshipment | -- | ❌ | N/A | N/A | `ARRI` at intermediate | No direct API |
| 4.4 | Vessel Departure from Transshipment | -- | ❌ | N/A | N/A | `DEPA` at intermediate | No direct API |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❌ | No API, no webhook capability |
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
> - T.S. Lines has no public API. All 30 fields are marked as unavailable via direct carrier integration.
> - However, third-party aggregators (particularly Terminal49 and Vizion) provide tracking data for T.S. Lines shipments. Through aggregators, container milestones (gate-out, gate-in, load, discharge), ETD/ETA, and vessel information are available. Terminal49 reports B/L tracking with port departure/arrival data, vessel details (IMO, name, voyage), and key container milestones.
> - If SSL uses an aggregator adapter, the effective coverage would be significantly higher -- estimated 40-60% for tracking milestones and transport events, though cutoffs, booking, schedules, and rates would remain unavailable.
> - Terminal49 specifically notes that final destination data, feeder/rail operations, and delivery confirmations are NOT available for T.S. Lines.

---

## Endpoint Reference

T.S. Lines does not provide any public API endpoints. This section is intentionally omitted.

---

## Rate Limits & Quotas

N/A -- T.S. Lines has no public API.

---

## Webhook / Push Support

T.S. Lines does not support webhooks or push notifications.

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | https://www.tslines.com/en/tracking |
| **Login required?** | No -- basic tracking available without login |
| **Data available on portal but NOT in API** | All tracking data is portal-only since there is no API. Portal provides B/L-based container tracking with vessel/voyage details and milestone events |
| **Scraping feasibility** | Not assessed. The portal appears to be a JavaScript-rendered single-page application (Bootstrap/Vue or similar), which may complicate scraping. ToS review required before considering scraping |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Unknown |
| **EDI message types** | Unknown |
| **EDI connection method** | Unknown |
| **EDI documentation** | Unknown -- contact T.S. Lines directly |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Unknown | Not explicitly confirmed. project44 covers 55+ shipping lines; T.S. Lines coverage not verified |
| **FourKites** | Unknown | Not explicitly confirmed |
| **Vizion** | Yes | Confirmed support. SCAC code TSTU. B/L tracking supported; booking tracking not supported. Source: https://docs.vizionapi.com/docs/supported-carriers |
| **INTTRA / E2open** | Unknown | No confirmed partnership found |
| **CargoSmart** | Unknown | Not confirmed |
| **Terminal49** | Yes | Confirmed support. SCAC code TXZJ. B/L tracking supported; booking and container number tracking not supported. Provides port of lading/discharge data, vessel details (IMO, name, voyage), key container milestones. Does NOT support final destination, feeder/rail, or delivery data. Source: https://terminal49.com/shipping-lines/txzj-t-s-lines-container-tracking |
| **Shipsgo** | Yes | Confirmed support. SCAC code TSTU. Tracking by container, booking, or B/L. Provides ETA predictions (96% claimed accuracy), live map, gate-in/out info. Offers free tracking API with unlimited calls. Source: https://shipsgo.com/ocean/carriers/tslines/container-tracking |
| **Portcast** | Yes | Confirmed support. Tracking by container, booking, B/L, or vessel. FCL and LCL coverage. Predictive ETA with AI. API available. Source: https://www.portcast.io/carrier-coverage/ts-lines-container-tracking |

> **Aggregator note:** Since T.S. Lines has no direct API, aggregator integration is the only programmatic path to tracking data. Vizion and Terminal49 are the most relevant for SSL's use case -- both offer API access to T.S. Lines tracking data with normalized event formats. Shipsgo and Portcast also offer APIs. The aggregator approach would provide container milestones (load/discharge/gate events), ETD/ETA, and vessel information, but would not cover booking, rates, cutoffs, or shipping instructions. SSL should evaluate aggregator pricing and data quality for T.S. Lines specifically before committing.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown -- no direct API. Aggregator freshness depends on aggregator's data collection method | Unknown |
| **API uptime/reliability** | N/A -- no API | N/A |
| **Historical data depth** | Unknown | Unknown |
| **Timezone handling** | Unknown | Unknown |
| **Character encoding** | Unknown | Unknown |

### Known Issues & Gotchas

- **No direct API**: T.S. Lines is one of the carriers with no public API whatsoever. All programmatic access must go through third-party aggregators.

- **Dual SCAC codes**: T.S. Lines appears under two different SCAC codes depending on the platform -- TSTU (used by Vizion, Shipsgo, Fluent Cargo) and TXZJ (used by Terminal49, Panjiva). The adapter must handle both codes or determine which is canonical.

- **Regional carrier limitations**: As an intra-Asia specialist with a relatively small fleet (sub-2,000 TEU vessels), T.S. Lines' tracking data granularity and reliability via aggregators may be less comprehensive than for major global carriers.

- **Limited aggregator feature coverage**: Terminal49 explicitly notes that final destination data, feeder/rail operations, and delivery confirmations are NOT available for T.S. Lines. Booking number and container number tracking are also not supported on Terminal49.

- **Web portal is JavaScript-rendered**: The tslines.com tracking portal appears to use a client-side JavaScript framework, making web scraping more complex than for server-rendered pages.

### Recently Deprecated or Changed

- No deprecation notices found. T.S. Lines completed its Hong Kong IPO in November 2024 and is actively expanding services, so digital capabilities may evolve.

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | Partial -- only via third-party aggregator. No direct carrier API exists. An adapter would wrap an aggregator API (Vizion, Terminal49, or Shipsgo) to provide tracking milestones and ETD/ETA data |
| **Implementation effort** | Medium (aggregator passthrough) -- the adapter would call an aggregator API rather than the carrier directly. Aggregator APIs are typically well-documented with standard auth (API key or OAuth2) |
| **DCSA base adapter usable?** | No -- T.S. Lines does not implement DCSA. The aggregator adapter would use the aggregator's data model, not DCSA |

### Recommended Approach

The only viable approach for T.S. Lines integration is through a third-party aggregator. SSL should select one aggregator that covers T.S. Lines (and ideally other non-API carriers) and build an aggregator adapter that normalizes the aggregator's response format to SSL's canonical data model.

Vizion is the strongest candidate for this purpose. It is an API-first container tracking platform with confirmed T.S. Lines support (SCAC TSTU), offers B/L tracking, and pushes standardized container events. Vizion's event-driven model (webhooks + polling) aligns well with SSL's change detection requirements. Terminal49 is a viable alternative with B/L tracking and milestone data.

If SSL already uses or plans to use an aggregator for other non-API carriers, the same aggregator adapter can serve T.S. Lines with no additional carrier-specific work -- just adding the SCAC code to the supported list.

### Recommended Lookup Method

**Bill of Lading (B/L) number** is the only viable lookup method. Both Vizion and Terminal49 confirm B/L tracking support for T.S. Lines. Booking number and container number tracking are not supported on Terminal49 and booking tracking is not supported on Vizion. Shipsgo and Portcast report support for additional identifier types.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Every 4-6 hours for in-transit shipments. Aggregator rate limits and pricing determine the practical ceiling |
| **Incremental filter** | Depends on aggregator capability. Vizion supports event-driven webhooks (preferred). Terminal49 offers DataSync. If polling, compare against local state to detect changes |
| **Batch tracking** | Depends on aggregator. Vizion and Terminal49 support subscribing to multiple shipments. Not a one-call-per-batch model |

### Auth Implementation Notes

Authentication depends entirely on the chosen aggregator:
- **Vizion**: API key-based auth. Well-documented at https://docs.vizionapi.com
- **Terminal49**: API key-based auth
- **Shipsgo**: API key-based auth
- **Portcast**: API key-based auth; scheduling a consultation call may be required

No carrier-level authentication is needed since there is no direct T.S. Lines API.

### Edge Cases to Handle

- **Dual SCAC code resolution**: T.S. Lines uses both TSTU and TXZJ. The adapter must determine which SCAC the chosen aggregator expects and handle any B/L number prefix stripping (Vizion strips TXZJ prefixes automatically).

- **Limited event coverage via aggregator**: Not all 9 container milestones may be available. Terminal49 confirms gate events, load/discharge, and transshipment, but NOT final destination delivery or feeder/rail data. Expect gaps in the tracking lifecycle.

- **No cutoff data**: Cutoffs (DCO, VCO, FCO, etc.) are not available through any aggregator for T.S. Lines. The adapter must handle missing cutoff data gracefully.

- **No booking or rate data**: The adapter can only provide tracking -- no booking lifecycle, shipping instructions, or rate data. These capabilities must be marked as unsupported in `CarrierCapabilities`.

### Mapping Complexity

**Low complexity** (if using an aggregator). Aggregators like Vizion and Terminal49 already normalize carrier data into their own standardized formats. The mapping task is from aggregator format to SSL's canonical model, not from raw T.S. Lines data. This is a one-time effort per aggregator that benefits all carriers covered by that aggregator.

The main complexity is in handling the gaps -- gracefully reporting which milestones and fields are unavailable for T.S. Lines versus other carriers, and ensuring downstream consumers understand the reduced data coverage.

---

## Open Questions

- [ ] Does SSL have an existing relationship with any aggregator (Vizion, Terminal49, Shipsgo, Portcast) that covers T.S. Lines?
- [ ] Which SCAC code is canonical for T.S. Lines -- TSTU or TXZJ? Different aggregators use different codes
- [ ] Does T.S. Lines offer any private/partner API that is not publicly documented? Worth a direct inquiry
- [ ] Does T.S. Lines support EDI (INTTRA/e2open)? Could be an alternative data channel for booking/SI
- [ ] What is the data freshness and reliability of T.S. Lines tracking data through aggregators?
- [ ] Is T.S. Lines likely to develop a public API following their 2024 Hong Kong IPO and expansion?
- [ ] What is the pricing model for the preferred aggregator for T.S. Lines coverage?

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | https://www.tslines.com |
| Cargo Tracking Portal | https://www.tslines.com/en/tracking |
| About T.S. Lines (Australia) | https://www.tslines.com.au/about-us/ |
| Vizion Supported Carriers | https://docs.vizionapi.com/docs/supported-carriers |
| Terminal49 T.S. Lines Tracking | https://terminal49.com/shipping-lines/txzj-t-s-lines-container-tracking |
| Shipsgo T.S. Lines Tracking | https://shipsgo.com/ocean/carriers/tslines/container-tracking |
| Portcast T.S. Lines Tracking | https://www.portcast.io/carrier-coverage/ts-lines-container-tracking |
| Fluent Cargo (TSTU schedules) | https://www.fluentcargo.com/carriers/scac/TSTU |
| Panjiva (TXZJ profile) | https://panjiva.com/scac_profiles/profile/TXZJ |
| Routescanner T.S. Lines Schedules | https://www.routescanner.com/partners/TS%20Lines |
| TimeToCargo T.S. Lines | https://timetocargo.com/shipping-lines/ts-lines |
| GoComet T.S. Lines | https://www.gocomet.com/online-container-tracking/carriers/ts-line |
| Loadstar: TS Lines 2024 Earnings | https://theloadstar.com/ts-lines-revamps-services-as-it-reports-soaring-2024-earnings/ |
| Loadstar: TS Lines Long-Haul Expansion | https://theloadstar.com/ts-lines-eyes-risky-return-to-long-haul-trade-with-new-ships/ |
