# Orient Overseas Container Line (OOCL) -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing. Research based on OOCL's public website, My OOCL Center documentation, EDI service pages, DCSA membership records, COSCO COP platform documentation, third-party aggregator listings, and community resources. No API credentials were obtained or used because OOCL does not offer a public API.
> **Researched by**: Agent (carrier API audit workflow)
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | Orient Overseas Container Line (OOCL) |
| **SCAC Code** | OOLU |
| **Parent Company** | COSCO Group (Orient Overseas (International) Limited / OOIL, acquired by COSCO Shipping Holdings in 2018 for $6.3B) |
| **Alliance** | Ocean Alliance (with CMA CGM, COSCO, Evergreen) |
| **Primary Services** | Container shipping (fully containerized) |
| **Market Position** | 7th-8th largest container carrier globally. Operates under COSCO Group's "dual brand" strategy alongside COSCO Shipping Lines. Revenue US$10.7B in 2024 |
| **Headquarters** | Hong Kong |
| **Website** | [https://www.oocl.com](https://www.oocl.com) |

### OOCL Digital Ecosystem

| Entity | Role | URL |
|--------|------|-----|
| **OOCL Website** | Corporate site and public tracking | [oocl.com](https://www.oocl.com) |
| **My OOCL Center (MOC)** | Customer portal for booking, tracking, documentation, reports | [moc.oocl.com](https://moc.oocl.com) |
| **CargoSmart** | Technology platform powering OOCL EDI and MOC | [cargosmart.com](https://www.cargosmart.com/) |
| **IQAX** | Electronic Bill of Lading platform (blockchain/GSBN) | [iqax.com](https://www.iqax.com) |
| **GSBN** | Global Shipping Business Network -- blockchain trade platform | [gsbn.trade](https://gsbn.trade) |

> **Note on CargoSmart**: CargoSmart is an independently-operated company with OOCL investing in its development, introduced in October 2000. It powers OOCL's EDI services and the My OOCL Center portal. CargoSmart is not a third-party aggregator in this context -- it is OOCL's own technology affiliate.

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | **No** |
| **Developer portal URL** | N/A |
| **API documentation URL(s)** | N/A -- no public API documentation exists |
| **Documentation quality** | **None** -- no API documentation available. Web portal and EDI service pages exist but do not describe REST/SOAP APIs |
| **OpenAPI/Swagger spec available?** | No |
| **Sandbox/test environment?** | No (for API). COSCO's COP platform has a test endpoint but does not cover OOCL |
| **Developer registration** | N/A -- no developer registration process exists |
| **Developer support channels** | General customer service only. No developer-specific support |
| **Community/third-party libraries** | None found -- no GitHub repos, npm packages, or PyPI packages for OOCL API integration |
| **API changelog / release notes** | N/A |

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | **No** -- OOCL is not among the nine DCSA member carriers (MSC, Maersk, CMA CGM, Hapag-Lloyd, ONE, Evergreen, Yang Ming, HMM, ZIM) |
| **DCSA APIs implemented** | **None** (for Track & Trace, Booking, or Commercial Schedules) |
| **DCSA TNT version** | N/A |
| **DCSA Booking version** | N/A |
| **DCSA Schedules version** | N/A |
| **Known DCSA deviations** | N/A |

> **Exception**: OOCL's IQAX eBL platform implements **DCSA eBL API v3.0** on the GSBN blockchain platform (live since June 2025). This is limited to electronic Bill of Lading functionality and does not extend to tracking, booking, or schedules. Source: [IQAX DCSA eBL v3.0 announcement](https://gsbn.trade/iqax-becomes-first-ebl-solution-globally-to-go-live-with-dcsa-ebl-api-v3-0-on-gsbn/)

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | **Yes** | Powered by CargoSmart. Supports UN/EDIFACT and ANSI X.12 for booking, shipping instructions, shipment status, B/L details. Source: [OOCL EDI page](https://www.oocl.com/eng/ourservices/eservices/edi) |
| **XML (EDI-style)** | **Yes** | XML message format supported alongside EDIFACT/X.12 for system-to-system integration |
| **INTTRA integration** | **No** | OOCL is not listed on INTTRA/E2open's ocean carrier network. Confirmed absent from their carrier list. Source: [INTTRA Ocean Carrier Network](https://www.inttra.com/ocean-carrier-network/) |
| **BIC (Bureau International des Containers)** | Yes | Container IDs follow BIC ISO 6346 format (OOLU prefix) |
| **UN/LOCODE** | Unknown | Likely used in EDI messages but not confirmed from public documentation |
| **GSBN** | **Yes** | Participant in Global Shipping Business Network blockchain platform |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | N/A -- no public API |
| **Auth documentation** | N/A |
| **Registration process** | N/A for API. MOC portal requires OOCL customer account. EDI requires CargoSmart registration |
| **Registration URL** | MOC: [moc.oocl.com](https://moc.oocl.com) |
| **Partner program required?** | N/A for API. EDI integration requires business relationship with OOCL |
| **Partner program URL** | N/A |
| **Credential type** | MOC: Username/Password. EDI: CargoSmart credentials + SFTP/AS2 setup |
| **Token refresh supported?** | N/A |
| **Token lifetime** | N/A |
| **Access tiers** | N/A |
| **IP whitelisting required?** | Unknown for EDI |

### Access Requirements Summary for SSL

OOCL does not offer a public REST/SOAP API. To access OOCL data programmatically, SSL has three options:

1. **EDI integration** -- Register with OOCL's CargoSmart-powered EDI service. Requires a business relationship with OOCL. Supports EDIFACT/X.12/XML over SFTP or AS2. This provides booking, shipping instructions, shipment status (IFTSTA), and B/L data but requires traditional EDI infrastructure rather than REST API calls.

2. **Third-party aggregator** -- Use Vizion (confirmed OOCL coverage) or project44 (likely coverage given 98%+ ocean freight coverage). This provides container tracking via a modern REST API without direct OOCL integration. Requires commercial agreement with the aggregator.

3. **Web portal scraping** -- OOCL's public cargo tracking page does not require login and provides milestone data. However, this approach is fragile, may violate OOCL's Terms of Service, and is not recommended for production use.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field must have a row.
> ✅ = Available | ❌ = Not available | ⚠️ = Partial / limited | ❓ = Unknown
>
> **Important context**: OOCL has no public API. The assessments below reflect availability through EDI and the web portal. Fields marked with ⚠️ may be available via EDI (IFTSTA/IFTMIN) or visible on the web portal but cannot be accessed via a REST API.

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ⚠️ | Web: [Sailing Schedule](https://www.oocl.com/eng/ourservices/eservices/sailingschedule) | N/A | N/A | Available on web portal and MOC. No API endpoint. Scraping possible but not recommended |
| 1.2 | Point-to-Point Route Options | ⚠️ | Web: Sailing Schedule search by origin/destination | N/A | N/A | Available via web portal search. No API endpoint |
| 1.3 | Booking Lifecycle | ⚠️ | MOC Portal + EDI | EDI: IFTMIN (booking), IFTSTA (status) | N/A | Available through MOC portal (login required) and EDI. No REST API |
| 1.4 | Shipping Instructions | ⚠️ | MOC Portal + EDI | EDI messages for SI submission | N/A | Available through MOC portal and EDI. IQAX eBL platform for electronic B/L (DCSA eBL API v3.0 on GSBN) |
| 1.5 | Rates | ❌ | Web: [Rate Inquiry](https://www.oocl.com/eng/contactus/rateinquiry/Pages/rateinquiry.aspx) | N/A | N/A | Rate inquiry via web form only. No API or EDI for rates |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❓ | Unknown | Unknown | `ECP` | May be available in EDI booking confirmation or MOC. Not confirmed from public documentation |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❓ | Unknown | Unknown | `EFC` | May be available in EDI booking confirmation or MOC. Not confirmed |
| 2.3 | Documentation Cutoff | DCO | ⚠️ | MOC Portal, possibly EDI | Unknown | `DCO` | Visible on web portal for confirmed bookings. May be in EDI messages. No API access |
| 2.4 | VGM Cutoff | VCO | ⚠️ | MOC Portal, possibly EDI | Unknown | `VCO` | VGM submission available via MOC. Cutoff timestamp likely shown. No API access |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ⚠️ | MOC Portal, web tracking | Unknown | `FCO` | Web portal shows cutoff info for confirmed bookings. No API access |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❓ | Unknown | Unknown | `LCO` | Not confirmed from public documentation |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ❓ | Unknown | Unknown | Inferred from first EquipmentEvent | Not confirmed. May be visible in MOC or EDI |
| 3.2 | Empty Container Gate-Out (Pickup) | ⚠️ | Web tracking, EDI (IFTSTA) | "Empty Container Pick-Up" milestone on web portal | `GTOT` + `EMPTY` | Confirmed visible on web portal tracking. Available via EDI IFTSTA. No API |
| 3.3 | Full Container Gate-In | ⚠️ | Web tracking, EDI (IFTSTA) | Gate-in milestone on web portal | `GTIN` + `LADEN` | Visible on web portal tracking. Available via EDI. No API |
| 3.4 | Container Loaded on Vessel | ⚠️ | Web tracking, EDI (IFTSTA) | "Loaded on Vessel" milestone | `LOAD` + `LADEN` | Confirmed visible on web portal. Available via EDI. No API |
| 3.5 | Container Discharged at Transshipment | ⚠️ | Web tracking, EDI (IFTSTA) | Discharge event at intermediate port | `DISC` + `LADEN` + transshipment | Visible on web portal for transshipment shipments. No API |
| 3.6 | Container Loaded at Transshipment | ⚠️ | Web tracking, EDI (IFTSTA) | Load event at transshipment port | `LOAD` + `LADEN` + transshipment | Visible on web portal for transshipment shipments. No API |
| 3.7 | Container Discharged at Destination | ⚠️ | Web tracking, EDI (IFTSTA) | "Discharged from Vessel" milestone | `DISC` + `LADEN` | Confirmed visible on web portal. Available via EDI. No API |
| 3.8 | Full Container Gate-Out (Delivery) | ⚠️ | Web tracking, EDI (IFTSTA) | Gate-out milestone on web portal | `GTOT` + `LADEN` | Visible on web portal. Available via EDI. No API |
| 3.9 | Empty Container Returned | ⚠️ | Web tracking, EDI (IFTSTA) | Empty return milestone on web portal | `GTIN` + `EMPTY` | Visible on web portal. Available via EDI. No API |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ⚠️ | Web tracking, Sailing Schedule, EDI | ETD shown in tracking and schedule pages | `DEPA` + classifier | Available on web portal and in EDI. Web portal shows ETA adjustments. No API |
| 4.2 | Estimated Time of Arrival | ETA | ⚠️ | Web tracking, Sailing Schedule, EDI | ETA shown in tracking and schedule pages | `ARRI` + classifier | Available on web portal and in EDI. Web portal shows ETA adjustments. No API |
| 4.3 | Vessel Arrival at Transshipment | -- | ⚠️ | Web tracking, EDI | Vessel arrival at intermediate port | `ARRI` at intermediate | Visible on web portal for multi-leg shipments. No API |
| 4.4 | Vessel Departure from Transshipment | -- | ⚠️ | Web tracking, EDI | Vessel departure from intermediate port | `DEPA` at intermediate | Visible on web portal for multi-leg shipments. No API |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❌ | No webhook/push API available. No event subscription mechanism |
| Event Polling with timestamp filter | ❌ | No API to poll. EDI IFTSTA messages provide status updates but on a push/schedule basis, not on-demand polling |
| Event Classifier Progression (PLN->EST->ACT) | ❌ | No API-level event classifier progression. Web portal shows ETA updates but not in a structured PLN->EST->ACT format |
| Retracted Events | ❌ | No API mechanism for retracted events |
| Change Remarks | ❌ | No API mechanism for change remarks |
| Delay Reason Codes | ❌ | No API mechanism for delay reason codes |

### Coverage Summary

| Category | Fields Available | Fields Unavailable | Fields Unknown | Coverage % |
|----------|-----------------|-------------------|----------------|-----------|
| API Domains (1.x) | 0/5 | 1/5 | 0/5 | 0% (4 partial via web/EDI) |
| Cutoffs (2.x) | 0/6 | 0/6 | 3/6 | 0% (3 partial via web/EDI, 3 unknown) |
| Container Milestones (3.x) | 0/9 | 0/9 | 1/9 | 0% (8 partial via web/EDI, 1 unknown) |
| Transport Events (4.x) | 0/4 | 0/4 | 0/4 | 0% (4 partial via web/EDI) |
| Change Detection (5.x) | 0/6 | 6/6 | 0/6 | 0% |
| **Total** | **0/30** | **7/30** | **4/30** | **0% via API (63% partial via web/EDI, 13% unknown)** |

> **Coverage note**: OOCL has **zero fields available via a REST/SOAP API**. However, 19 of 30 fields (63%) have partial availability through EDI (IFTSTA/IFTMIN messages) or the web portal. The remaining 7 fields are unavailable (all 6 Change Detection mechanisms + Rates), and 4 fields are unknown (ERD, EFC, LCO cutoffs and Container Assigned to Booking). For SDK integration, the most viable path is through a third-party aggregator like Vizion, which provides REST API access to OOCL tracking data.

---

## Endpoint Reference

OOCL has no public REST/SOAP API endpoints. This section is not applicable.

### Lookup Methods Summary

| Identifier Type | Supported? | Which Endpoints? | Notes |
|----------------|-----------|-----------------|-------|
| **Bill of Lading (B/L) number** | Web portal + EDI | Web tracking, MOC, EDI | Format: OOLU + 8-12 alphanumeric characters |
| **Booking reference** | Web portal + EDI | Web tracking, MOC, EDI | Available as a tracking identifier |
| **Container number** | Web portal + EDI | Web tracking, MOC, EDI | Standard BIC format |
| **Carrier booking number** | Web portal + EDI | MOC, EDI | Same as booking reference |
| **Vessel IMO / voyage** | Web portal only | Vessel tracking page, sailing schedule | [Vessel & Rail Tracking](https://www.oocl.com/eng/ourservices/eservices/trackandtrace) |

---

## Rate Limits & Quotas

N/A -- OOCL has no public API. No rate limits apply.

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | [https://www.oocl.com/eng/ourservices/eservices/cargotracking](https://www.oocl.com/eng/ourservices/eservices/cargotracking/Pages/cargotracking.aspx) |
| **Login required?** | No (public cargo tracking). MOC portal requires login for advanced features |
| **Data available on portal but NOT in API** | All tracking data is portal-only since there is no API. Includes: milestone events, vessel details, ETD/ETA, event timestamps, map view, customs clearance status |
| **Scraping feasibility** | Not assessed in detail. Portal appears to be a standard web application. Anti-bot measures unknown. ToS review required before attempting. Not recommended for production use |

### Additional Web Services

OOCL's website and MOC portal provide:
- **Booking** -- online booking submission via MOC
- **Sailing Schedule** -- search by port, vessel, or route
- **Shipping Instructions** -- submit via MOC
- **VGM Submission** -- submit Verified Gross Mass via MOC
- **eBL** -- electronic Bill of Lading via IQAX platform
- **Shipment Details** -- detailed shipment information via MOC
- **Rate Inquiry** -- web form for rate requests (not automated)

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | **Yes** |
| **EDI message types** | UN/EDIFACT, ANSI X.12, and XML for: booking, shipping instructions, shipment status, B/L details. Specific EDIFACT message types (IFTMIN, COPARN, IFTSTA, etc.) not enumerated on public pages |
| **EDI connection method** | **SFTP** (with SSH protocol) and **AS2** protocol |
| **EDI documentation** | Behind registration wall. Source: [OOCL EDI page](https://www.oocl.com/eng/ourservices/eservices/edi) |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Likely yes | project44 claims 98%+ global ocean freight coverage, 55+ shipping lines. OOCL is a top-10 carrier. Not individually confirmed but highly probable. Source: [project44 Ocean Visibility](https://www.project44.com/platform/visibility/ocean/) |
| **FourKites** | Unknown | FourKites covers 85+ carriers. OOCL not specifically confirmed. Source: [FourKites Ocean](https://www.fourkites.com/platform/ocean-freight-visibility/) |
| **Vizion** | **Yes** | Explicitly listed. Provides container tracking API for OOCL. Source: [Vizion OOCL tracking](https://www.vizionapi.com/carrier-tracking/oocl) |
| **INTTRA / E2open** | **No** | OOCL is NOT listed on INTTRA's ocean carrier network. Confirmed absent. Source: [INTTRA carrier network](https://www.inttra.com/ocean-carrier-network/) |
| **CargoSmart** | **Yes (affiliated)** | CargoSmart is OOCL's own technology affiliate. Powers EDI and MOC portal. Source: [CargoSmart](https://www.cargosmart.com/) |
| **Portcast** | **Yes** | Listed for predictive container tracking. Source: [Portcast OOCL](https://www.portcast.io/carrier-coverage/orient-overseas-container-line-oocl-tracking) |

> **Aggregator note**: Since OOCL has no public API, a third-party aggregator is the most practical path to REST API access for OOCL tracking data. Vizion is the only confirmed aggregator with explicit OOCL support. project44 is highly likely given their coverage claims. The aggregator approach adds cost and a dependency but provides a standardized REST API without EDI infrastructure.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown -- no published data on event delay | Unknown |
| **API uptime/reliability** | N/A -- no API | N/A |
| **Historical data depth** | Unknown | Unknown |
| **Timezone handling** | Unknown -- web portal appears to show local port times | Estimated |
| **Character encoding** | Unknown | Unknown |

### Known Issues & Gotchas

- **No public API**: The most significant finding. OOCL is a top-10 global carrier that does not offer a public REST/SOAP API for tracking or any other function. This is unusual for a carrier of this size
- **Not a DCSA member**: Despite parent company COSCO being in the Ocean Alliance with DCSA members (CMA CGM, Evergreen), OOCL has not joined DCSA
- **Not on INTTRA**: Also unusual for a major carrier. May limit EDI integration options for partners using INTTRA as their primary ocean platform
- **Separate from COSCO COP**: Despite being owned by COSCO, OOCL is not available on COSCO's Open API Platform. The "dual brand" strategy means separate digital infrastructure
- **CargoSmart dependency**: All programmatic integration goes through CargoSmart-powered EDI. This is a single point of dependency
- **IQAX eBL is not a tracking API**: OOCL's one DCSA-compliant offering (eBL API v3.0) is only for electronic Bills of Lading, not for tracking or shipment visibility

### Recently Deprecated or Changed

- No known deprecations (no API to deprecate)
- IQAX eBL launched DCSA eBL API v3.0 on GSBN in June 2025 -- this is OOCL's newest digital service

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | **Partial** -- only through a third-party aggregator (Vizion recommended) or EDI. No direct API integration is possible |
| **Implementation effort** | **Very High** (no API) -- requires either aggregator integration (medium effort but adds dependency) or EDI infrastructure (high effort, specialized) |
| **DCSA base adapter usable?** | **No** -- OOCL does not implement DCSA APIs (except eBL which is not relevant for tracking) |

### Recommended Approach

The recommended approach for OOCL integration is a **two-tier strategy**:

**Primary: Aggregator integration via Vizion** -- Vizion explicitly supports OOCL container tracking through their REST API. This provides the fastest path to integration with modern API tooling (REST, JSON, webhooks). The SDK adapter would talk to Vizion's API, not OOCL directly. The trade-off is an aggregator dependency and per-track pricing.

**Secondary: EDI integration (if cost/volume justifies it)** -- For high-volume scenarios where aggregator costs are prohibitive, SSL could establish a direct EDI connection with OOCL via CargoSmart. This requires SFTP/AS2 infrastructure and EDIFACT/X.12 parsing capability. EDI provides richer data (booking, SI, B/L, status) but at significantly higher implementation cost.

A direct REST API adapter for OOCL is not possible given current offerings. SSL should monitor whether OOCL develops an API in the future -- the COSCO Group's digital transformation strategy and the general industry trend toward DCSA adoption suggest this may happen eventually.

### Recommended Lookup Method

**Container number** is the recommended primary lookup method when using an aggregator like Vizion, as aggregator APIs typically normalize on container-level tracking. B/L number is a secondary option. For EDI, booking reference provides the broadest data access across the shipment lifecycle.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Depends on aggregator. Vizion supports webhooks (push) which is preferred. For polling, every 4-6 hours is typical for aggregator APIs |
| **Incremental filter** | Aggregator-dependent. Vizion uses webhook-based push notifications for new events |
| **Batch tracking** | Aggregator-dependent. Vizion supports subscribing to individual containers |

### Auth Implementation Notes

For aggregator-based integration (Vizion):
- Vizion uses API key authentication
- Standard REST API patterns apply
- No OOCL-specific auth required -- all auth is with the aggregator

For EDI integration:
- SFTP credentials (username/password or SSH key) or AS2 certificates
- CargoSmart-managed registration process
- Not a REST/OAuth pattern

### Edge Cases to Handle

- **Aggregator data lag**: Data from aggregators may have a delay compared to what's visible on OOCL's web portal. Freshness depends on the aggregator's data pipeline
- **Limited change detection**: Without direct API access, change detection (schedule changes, ETA updates) is limited to what the aggregator provides. No PLN->EST->ACT progression available through aggregators
- **No webhook/push from OOCL directly**: All push notifications must come from the aggregator layer
- **B/L prefix**: OOCL B/L numbers typically start with "OOLU". Aggregator APIs may or may not require this prefix
- **Transshipment visibility**: Depends on aggregator data depth. May be less detailed than what OOCL's web portal shows

### Mapping Complexity

**Low complexity for aggregator path** -- the aggregator normalizes OOCL's data into their standard format. Mapping from Vizion's API to the canonical model is straightforward.

**High complexity for EDI path** -- requires EDIFACT/X.12 parsing, message type mapping (IFTSTA events to canonical milestones), and handling carrier-specific EDI implementations.

---

## Open Questions

- [ ] Does SSL have an existing business relationship with OOCL that would facilitate EDI integration?
- [ ] Is the aggregator cost model (Vizion or project44) acceptable for OOCL tracking volume?
- [ ] Does OOCL have any plans to launch a public REST API? (Worth asking OOCL directly or monitoring COSCO Group announcements)
- [ ] What specific EDIFACT message types does OOCL support? (Requires EDI registration to access documentation)
- [ ] Is OOCL available on project44? (Highly likely but not individually confirmed -- worth verifying with project44 sales)
- [ ] Would OOCL's web portal tracking be sufficient for low-volume use cases where an aggregator is not justified?
- [ ] Are cutoff dates (ERD, EFC, LCO) available in OOCL's EDI booking confirmation messages?
- [ ] Does CargoSmart offer any API access beyond EDI that could be leveraged?

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | [https://www.oocl.com](https://www.oocl.com) |
| My OOCL Center (MOC) | [https://moc.oocl.com](https://moc.oocl.com) |
| Public Cargo Tracking | [https://www.oocl.com/eng/ourservices/eservices/cargotracking](https://www.oocl.com/eng/ourservices/eservices/cargotracking/Pages/cargotracking.aspx) |
| Sailing Schedule | [https://www.oocl.com/eng/ourservices/eservices/sailingschedule](https://www.oocl.com/eng/ourservices/eservices/sailingschedule) |
| Vessel & Rail Tracking | [https://www.oocl.com/eng/ourservices/eservices/trackandtrace](https://www.oocl.com/eng/ourservices/eservices/trackandtrace) |
| EDI Services | [https://www.oocl.com/eng/ourservices/eservices/edi](https://www.oocl.com/eng/ourservices/eservices/edi) |
| MOC User Guide (PDF) | [https://www.oocl.com/SiteCollectionDocuments/MOC%20User%20Guide.pdf](https://www.oocl.com/SiteCollectionDocuments/MOC%20User%20Guide.pdf) |
| eBL Service (IQAX) | [https://www.oocl.com/eng/ourservices/eservices/eBL](https://www.oocl.com/eng/ourservices/eservices/eBL) |
| IQAX eBL FAQ | [https://www.oocl.com/eng/ourservices/eservices/eBL/faq](https://www.oocl.com/eng/ourservices/eservices/eBL/faq/Pages/default.aspx) |
| IQAX DCSA eBL v3.0 on GSBN | [https://gsbn.trade/iqax-becomes-first-ebl-solution-globally-to-go-live-with-dcsa-ebl-api-v3-0-on-gsbn/](https://gsbn.trade/iqax-becomes-first-ebl-solution-globally-to-go-live-with-dcsa-ebl-api-v3-0-on-gsbn/) |
| COSCO COP Platform | [https://cop.lines.coscoshipping.com/](https://cop.lines.coscoshipping.com/) |
| COSCO COP GitHub | [https://github.com/cop-cos/COP](https://github.com/cop-cos/COP) |
| INTTRA Carrier Network | [https://www.inttra.com/ocean-carrier-network/](https://www.inttra.com/ocean-carrier-network/) |
| DCSA Members | [https://dcsa.org/about-us/](https://dcsa.org/about-us/) |
| Vizion OOCL Tracking | [https://www.vizionapi.com/carrier-tracking/oocl](https://www.vizionapi.com/carrier-tracking/oocl) |
| Portcast OOCL Tracking | [https://www.portcast.io/carrier-coverage/orient-overseas-container-line-oocl-tracking](https://www.portcast.io/carrier-coverage/orient-overseas-container-line-oocl-tracking) |
| CargoSmart | [https://www.cargosmart.com/](https://www.cargosmart.com/) |
| project44 Ocean Visibility | [https://www.project44.com/platform/visibility/ocean/](https://www.project44.com/platform/visibility/ocean/) |
| OOCL Mobile App | [https://www.oocl.com/eng/ourservices/eservices/mobilesolution](https://www.oocl.com/eng/ourservices/eservices/mobilesolution) |
| Rate Inquiry | [https://www.oocl.com/eng/contactus/rateinquiry](https://www.oocl.com/eng/contactus/rateinquiry/Pages/rateinquiry.aspx) |
