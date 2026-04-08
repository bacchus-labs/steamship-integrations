# SM Line Corporation -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing
> **Researched by**: Agent
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | SM Line Corporation (commonly "SM Line" or "Shipping Maestro") |
| **SCAC Code** | SMLM |
| **Parent Company** | Samra Midas (SM) Group |
| **Alliance** | Independent (South Korea-based; slot exchange cooperation with HMM since 2024; formerly participated in 2M cooperation with Maersk/MSC in 2020) |
| **Primary Services** | Container shipping (intra-Asia, transpacific, Middle East) |
| **Market Position** | Mid-tier carrier; successor to Hanjin Shipping assets (acquired Dec 2016); fleet of ~30+ vessels; focuses on Asia-US West Coast and intra-Asia trades |
| **Headquarters** | Seoul, South Korea |
| **Website** | https://smlines.com |

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
| **Developer support channels** | General contact via smlines.com; no developer-specific channels found |
| **Community/third-party libraries** | None found for direct SM Line API. Third-party aggregators (Vizion, Terminal49, ShipsGo) offer SM Line tracking through their own APIs |
| **API changelog / release notes** | Not published |

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | No -- SM Line is not listed as a DCSA member (DCSA was founded by MSC, Maersk, CMA CGM, Hapag-Lloyd, ONE, Evergreen, Yang Ming, HMM, and ZIM) |
| **DCSA APIs implemented** | None |
| **DCSA TNT version** | N/A |
| **DCSA Booking version** | N/A |
| **DCSA Schedules version** | N/A |
| **Known DCSA deviations** | N/A |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Yes | Supports ANSI X.12, UN/EDIFACT, and XML formats. Message types include Booking Request, Booking Confirmation, Shipping Instruction, Bills of Lading (outbound); Arrival Notice, Shipment Status, Vessel Schedule (inbound). Source: https://esvc.smlines.com/smline/CUP_HOM_3050.do |
| **INTTRA integration** | Yes | SM Line joined the INTTRA (now E2open) network. Provides booking and container tracking through INTTRA's multi-carrier platform. Source: https://www.inttra.com/newsroom/press-releases/sm-line-joins-inttra-network/ |
| **BIC (Bureau International des Containers)** | Unknown | |
| **UN/LOCODE** | Yes | Port codes used in web tracking portal and schedule displays |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | N/A -- no public REST/SOAP API exists |
| **Auth documentation** | N/A |
| **Registration process** | N/A (for EDI: contact SM Line's IT/EDI team directly) |
| **Registration URL** | N/A |
| **Partner program required?** | N/A for API; EDI likely requires business relationship |
| **Partner program URL** | N/A |
| **Credential type** | N/A |
| **Token refresh supported?** | N/A |
| **Token lifetime** | N/A |
| **Access tiers** | N/A |
| **IP whitelisting required?** | N/A |

### Access Requirements Summary for SSL

SM Line does not offer a public REST or SOAP API for programmatic access. There is no developer portal, no API documentation, and no self-service registration process. The carrier provides EDI connectivity (ANSI X.12, UN/EDIFACT, XML) for structured data exchange, which would require establishing a direct EDI partnership with SM Line's operations team.

For tracking data, SSL has two practical options: (1) integrate via a third-party aggregator such as Vizion, Terminal49, or INTTRA/E2open, which all support SM Line; or (2) establish an EDI connection for shipment status messages (IFTSTA equivalent). Direct API integration is not possible with SM Line's current digital infrastructure.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field must have a row.
> Availability assessed via: EDI, web portal, and third-party aggregators (not direct API).

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ⚠️ | Web portal: `esvc.smlines.com/smline/CUP_HOM_3005.do`; EDI inbound: Vessel Schedule | Vessel Schedule EDI message | N/A | Available via web portal (no login required for schedule search) and EDI. No REST API |
| 1.2 | Point-to-Point Route Options | ⚠️ | Web portal: `esvc.smlines.com/smline/CUP_HOM_3001.do` | N/A | N/A | Available via web portal only. No programmatic access |
| 1.3 | Booking Lifecycle | ⚠️ | EDI: Booking Request / Booking Confirmation messages; INTTRA booking platform | Booking Request, Booking Confirmation (EDI) | N/A | Available via EDI and INTTRA. No REST API for booking |
| 1.4 | Shipping Instructions | ⚠️ | EDI: Shipping Instruction message | Shipping Instruction (EDI) | N/A | Available via EDI only |
| 1.5 | Rates | ❌ | N/A | N/A | N/A | No programmatic access to rates found |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❓ | Unknown | Unknown | `ECP` | May be included in EDI Booking Confirmation; not confirmed |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❓ | Unknown | Unknown | `EFC` | May be included in EDI Booking Confirmation; not confirmed |
| 2.3 | Documentation Cutoff | DCO | ⚠️ | Web portal: visible in sailing schedule details | Displayed in portal schedule view | `DCO` | Visible on web portal schedule pages; likely in EDI Booking Confirmation |
| 2.4 | VGM Cutoff | VCO | ⚠️ | Web portal | Displayed in portal | `VCO` | Visible on web portal; likely in EDI messages |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ⚠️ | Web portal: visible in sailing schedule details | Displayed in portal schedule view | `FCO` | Visible on web portal schedule pages; likely in EDI Booking Confirmation |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❓ | Unknown | Unknown | `LCO` | SM Line focuses on FCL; LCL cutoff availability unknown |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ❓ | Unknown | Unknown | Inferred from first EquipmentEvent | Not confirmed via any channel |
| 3.2 | Empty Container Gate-Out (Pickup) | ⚠️ | Web portal tracking; EDI Shipment Status | Portal: status event with location | `GTOT` + `EMPTY` | Visible in web portal cargo tracking. Available via EDI Shipment Status message and aggregators |
| 3.3 | Full Container Gate-In | ⚠️ | Web portal tracking; EDI Shipment Status | Portal: status event with location | `GTIN` + `LADEN` | Visible in web portal cargo tracking |
| 3.4 | Container Loaded on Vessel | ⚠️ | Web portal tracking; EDI Shipment Status | Portal: "Loaded" status | `LOAD` + `LADEN` | Visible in web portal cargo tracking |
| 3.5 | Container Discharged at Transshipment | ⚠️ | Web portal tracking; EDI Shipment Status | Portal: "Discharged" at intermediate port | `DISC` + `LADEN` + transshipment | Visible in web portal if transshipment occurs |
| 3.6 | Container Loaded at Transshipment | ⚠️ | Web portal tracking; EDI Shipment Status | Portal: "Loaded" at intermediate port | `LOAD` + `LADEN` + transshipment | Visible in web portal if transshipment occurs |
| 3.7 | Container Discharged at Destination | ⚠️ | Web portal tracking; EDI Shipment Status | Portal: "Discharged" at destination | `DISC` + `LADEN` | Visible in web portal cargo tracking |
| 3.8 | Full Container Gate-Out (Delivery) | ⚠️ | Web portal tracking; EDI Shipment Status | Portal: gate-out status | `GTOT` + `LADEN` | Visible in web portal cargo tracking |
| 3.9 | Empty Container Returned | ⚠️ | Web portal tracking; EDI Shipment Status | Portal: empty return status | `GTIN` + `EMPTY` | Visible in web portal cargo tracking |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ⚠️ | Web portal: schedule and tracking pages; EDI Vessel Schedule | Portal: departure time in schedule/tracking | `DEPA` + classifier | Available on portal (gray = estimated, subject to change). EDI Vessel Schedule inbound message |
| 4.2 | Estimated Time of Arrival | ETA | ⚠️ | Web portal: schedule and tracking pages; EDI Vessel Schedule | Portal: arrival time in schedule/tracking | `ARRI` + classifier | Available on portal. Note: portal distinguishes "coastal" vs "actual" schedules |
| 4.3 | Vessel Arrival at Transshipment | -- | ⚠️ | Web portal tracking | Portal: arrival event at intermediate port | `ARRI` at intermediate | Visible in cargo tracking for multi-leg routes |
| 4.4 | Vessel Departure from Transshipment | -- | ⚠️ | Web portal tracking | Portal: departure event at intermediate port | `DEPA` at intermediate | Visible in cargo tracking for multi-leg routes |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❌ | No webhook or push notification capability found |
| Event Polling with timestamp filter | ❌ | No API endpoint to poll |
| Event Classifier Progression (PLN->EST->ACT) | ⚠️ | Web portal shows estimated (gray) vs actual schedules, but no programmatic access. EDI may carry status progression |
| Retracted Events | ❌ | No evidence of retracted event support |
| Change Remarks | ❌ | No evidence of change remarks in any channel |
| Delay Reason Codes | ❌ | No evidence of delay reason codes |

### Coverage Summary

| Category | Fields Available | Fields Unavailable | Fields Unknown | Coverage % |
|----------|-----------------|-------------------|----------------|-----------|
| API Domains (1.x) | 0/5 | 1/5 | 0/5 | 0% |
| Cutoffs (2.x) | 0/6 | 0/6 | 2/6 | 0% |
| Container Milestones (3.x) | 0/9 | 0/9 | 1/9 | 0% |
| Transport Events (4.x) | 0/4 | 0/4 | 0/4 | 0% |
| Change Detection (5.x) | 0/6 | 4/6 | 0/6 | 0% |
| **Total** | **0/30** | **5/30** | **3/30** | **0%** |

> **Important note on coverage**: The 0% coverage reflects the absence of any REST/SOAP API. However, significant data is available through non-API channels:
> - **EDI**: Booking, shipping instructions, shipment status, vessel schedules (marked as ⚠️ above)
> - **Web portal**: Tracking milestones, schedules, cutoffs (marked as ⚠️ above)
> - **Third-party aggregators**: Vizion, Terminal49, INTTRA/E2open all provide SM Line tracking data via their own APIs
>
> If aggregator access is counted, effective coverage for tracking milestones and transport events rises substantially.

---

## Endpoint Reference

SM Line does not expose any public REST or SOAP API endpoints. This section is intentionally omitted.

### Lookup Methods Summary

| Identifier Type | Supported? | Which Endpoints? | Notes |
|----------------|-----------|-----------------|-------|
| **Bill of Lading (B/L) number** | Web portal + EDI + Aggregators | Portal: `esvc.smlines.com/smline/CUP_HOM_3301.do` | B/L format: SMLM + 8-12 alphanumeric characters |
| **Booking reference** | Web portal + EDI + Aggregators | Portal tracking page | |
| **Container number** | Web portal + Aggregators | Portal tracking page | |
| **Carrier booking number** | Web portal + EDI | Portal tracking page | Same as booking reference |
| **Vessel IMO / voyage** | Web portal (schedule only) | Portal schedule page | |

---

## Rate Limits & Quotas

| Detail | Value | Source |
|--------|-------|--------|
| **Global rate limit** | N/A -- no API | N/A |
| **Per-endpoint limits** | N/A | N/A |
| **Daily/monthly quota** | N/A | N/A |
| **Rate limit response** | N/A | N/A |
| **Rate limit by** | N/A | N/A |
| **Burst allowance** | N/A | N/A |
| **Different tiers** | N/A | N/A |

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

No webhook or push notification support available. SM Line does not offer a public API.

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | https://esvc.smlines.com/smline/CUP_HOM_3301.do |
| **Login required?** | Partial -- basic tracking is accessible without login; "My Tracking" and some detailed features require login |
| **Data available on portal but NOT in API** | All data is portal-only since there is no API. Portal shows: container status with seal number, size, event dates, location, piece count, weight, VGM; sailing information with vessel name, ports, ETD/ETA; sequential status updates with timestamps; US customs/cargo release information; rail tracking data |
| **Scraping feasibility** | Difficult -- the portal is a Java-based web application (JSP) with session-based navigation; requires login for full data; anti-scraping measures not assessed but ToS likely prohibits automated access |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Yes |
| **EDI message types** | Outbound: Booking Request, Booking Confirmation, Shipping Instruction, Bills of Lading. Inbound: Arrival Notice, Shipment Status, Vessel Schedule |
| **EDI standards** | ANSI X.12, UN/EDIFACT, XML |
| **EDI connection method** | Unknown -- contact SM Line IT team for connectivity details |
| **EDI documentation** | https://esvc.smlines.com/smline/CUP_HOM_3050.do (overview page; detailed technical docs require carrier contact) |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Unknown | Not confirmed in available documentation; project44 claims 98%+ global ocean coverage but SM Line not explicitly listed |
| **FourKites** | Unknown | Not confirmed; FourKites covers 85+ ocean carriers but SM Line not explicitly mentioned |
| **Vizion** | Yes | SM Line (SMLM) listed as supported carrier. Tracking via container number, booking number, or B/L. Source: https://www.vizionapi.com/carrier-tracking/sm-lines |
| **INTTRA / E2open** | Yes | SM Line joined the INTTRA network. Provides booking and tracking through INTTRA's multi-carrier platform for intra-Asia and Asia-US routes. Source: https://www.inttra.com/newsroom/press-releases/sm-line-joins-inttra-network/ |
| **CargoSmart** | Unknown | Not confirmed in available documentation |
| **Terminal49** | Yes | SM Line (SMLM) listed as supported carrier with active status monitoring. Provides standardized milestones and attributes. Source: https://terminal49.com/shipping-lines |
| **ShipsGo** | Yes | Offers SM Line container tracking API. Source: https://shipsgo.com/ocean/carriers/smline/container-tracking |
| **Portcast** | Yes | Provides SM Line tracking with predictive ETA. Source: https://www.portcast.io/carrier-coverage/sm-line-container-tracking |

> **Aggregator note**: Since SM Line has no direct API, third-party aggregators are the only path to programmatic tracking data. Vizion, Terminal49, and INTTRA/E2open are the most established options. These aggregators likely obtain SM Line data through a combination of EDI feeds, web scraping, and AIS vessel tracking. The aggregator route will provide normalized milestone data but may lag behind the carrier's own portal for freshness, and will not provide booking or shipping instruction capabilities.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown -- no direct API; aggregator freshness depends on their SM Line data pipeline | Unknown |
| **API uptime/reliability** | N/A -- no API | N/A |
| **Historical data depth** | Unknown | Unknown |
| **Timezone handling** | Portal appears to use local port times; EDI format-dependent | Estimated (from portal observation) |
| **Character encoding** | Unknown | Unknown |

### Known Issues & Gotchas

- SM Line has no public API whatsoever -- all programmatic access must go through third-party aggregators or EDI
- The web portal is a Java/JSP application with session-based navigation, making it resistant to simple HTTP scraping
- Portal login is required for full tracking detail and "My Tracking" watchlist features
- B/L numbers use the SMLM prefix followed by 8-12 alphanumeric characters; some aggregators require stripping the prefix
- SM Line's route network is relatively narrow (intra-Asia, transpacific, Middle East) compared to global mega-carriers, which limits the number of shipments that would need tracking
- The carrier distinguishes between "coastal schedule" and "actual schedule" on its portal, which may cause confusion when interpreting ETD/ETA data
- SM Line cooperates with HMM on Asia-US West Coast services (since 2024), so some SM Line bookings may appear on HMM vessels and vice versa

### Recently Deprecated or Changed

- No deprecated endpoints (no API has ever existed)
- SM Line previously participated in 2M cooperation with Maersk/MSC (2020) but this arrangement has ended

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | Partial -- only through third-party aggregator integration (Vizion, Terminal49, or INTTRA/E2open). No direct carrier API exists |
| **Implementation effort** | High -- requires aggregator integration rather than direct carrier API. Alternatively, Very High if attempting EDI-based integration |
| **DCSA base adapter usable?** | No -- SM Line is not DCSA-compliant and has no API; aggregator responses would need custom normalization |

### Recommended Approach

The recommended approach for SM Line is to integrate through a third-party aggregator rather than attempting direct carrier integration. **Vizion** or **Terminal49** are the strongest candidates since both explicitly list SM Line (SMLM) as a supported carrier and provide REST APIs with normalized container tracking data.

The adapter should implement a generic "aggregator adapter" pattern that translates aggregator-specific tracking responses into the SSL canonical data model. This pattern would be reusable for other small carriers that lack their own APIs. The adapter would call the aggregator's tracking API using the B/L number, container number, or booking reference as the lookup key, and map the returned milestones to DCSA-equivalent events.

If SSL already has or plans to establish an INTTRA/E2open relationship, that platform offers both booking and tracking capabilities for SM Line, which would provide broader coverage than tracking-only aggregators.

### Recommended Lookup Method

**Bill of Lading (B/L) number** is the recommended primary lookup method. SM Line B/L numbers follow a consistent format (SMLM + 8-12 alphanumeric characters), making them easy to identify and validate. All aggregators and the web portal support B/L-based lookup. Container number is a solid secondary option.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Every 4 hours -- SM Line is a smaller carrier with limited route network; high-frequency polling is unnecessary. Adjust to every 2 hours for shipments approaching key milestones (vessel departure, arrival at destination) |
| **Incremental filter** | Depends on aggregator capabilities -- Vizion supports webhook push and timestamp-based polling; Terminal49 supports webhooks. Use aggregator webhooks where available to supplement polling |
| **Batch tracking** | Depends on aggregator -- Terminal49 supports tracking multiple containers per request; Vizion supports bulk reference submission. One aggregator API call typically covers one shipment reference |

### Auth Implementation Notes

Authentication will depend on the chosen aggregator:
- **Vizion**: API key-based authentication (header: `X-API-Key`)
- **Terminal49**: API key-based authentication (header: `Authorization: Token token=...`)
- **INTTRA/E2open**: Enterprise platform with separate onboarding; typically OAuth2 or SAML-based

The adapter should abstract aggregator authentication behind the standard `CarrierAdapter` auth interface so the aggregator can be swapped without consumer impact.

### Edge Cases to Handle

- SM Line vessels may operate under HMM cooperation agreements, causing tracking data to reference HMM vessel names or codes
- Transshipment events may be sparse for SM Line's intra-Asia routes but common on transpacific routes
- Aggregator data for SM Line may have longer delays than for major carriers due to less frequent data pipeline updates
- B/L prefix stripping: some aggregators require "SMLM" prefix removal, others include it -- normalize during lookup
- The carrier's portal shows US customs/cargo release data that aggregators may not capture

### Mapping Complexity

Mapping complexity is **medium** when using an aggregator. The aggregator (Vizion, Terminal49) will provide pre-normalized milestone data, but there will be gaps:
- Cutoff data (ERD, EFC, DCO, VCO, FCO, LCO) is unlikely to be available through tracking-only aggregators
- Change detection (retracted events, delay reason codes) will not be available
- Event classifier progression (PLN/EST/ACT) depends on aggregator data richness
- The mapping from aggregator milestone names to DCSA event codes is straightforward for standard container milestones but may require custom logic for SM Line-specific status descriptions

---

## Open Questions

- [ ] Does SSL have an existing relationship with any aggregator (Vizion, Terminal49, INTTRA/E2open) that covers SM Line?
- [ ] What volume of SM Line shipments does SSL handle? (This determines whether a dedicated integration is justified)
- [ ] Is SSL willing to establish an EDI connection with SM Line for richer data (booking, shipping instructions, cutoffs)?
- [ ] Does SM Line's cooperation with HMM mean that some SM Line shipments can be tracked through HMM's API instead?
- [ ] Are SM Line's EDI Shipment Status messages rich enough to provide all container milestones, or are they limited to key events only?

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | https://smlines.com |
| Company History | https://www.smlines.com/en/history.php |
| e-Service Portal | https://esvc.smlines.com/smline/CUP_HOM_3256.do?sessLocale=en |
| Cargo Tracking (Portal) | https://esvc.smlines.com/smline/CUP_HOM_3301.do |
| Vessel Schedule (Portal) | https://esvc.smlines.com/smline/CUP_HOM_3005.do?sessLocale=en |
| Point-to-Point Schedule (Portal) | https://esvc.smlines.com/smline/CUP_HOM_3001.do?sessLocale=en |
| EDI Services Page | https://esvc.smlines.com/smline/CUP_HOM_3050.do |
| SM Group Business Overview | https://www.smgroup.co.kr/eng/business/view.do?IDX=45 |
| INTTRA Partnership Announcement | https://www.inttra.com/newsroom/press-releases/sm-line-joins-inttra-network/ |
| Vizion -- SM Lines Tracking | https://www.vizionapi.com/carrier-tracking/sm-lines |
| Terminal49 -- Shipping Lines | https://terminal49.com/shipping-lines |
| ShipsGo -- SM Line Tracking | https://shipsgo.com/ocean/carriers/smline/container-tracking |
| Portcast -- SM Line Tracking | https://www.portcast.io/carrier-coverage/sm-line-container-tracking |
| Hanjin Shipping (History Context) | https://en.wikipedia.org/wiki/Hanjin_Shipping |
