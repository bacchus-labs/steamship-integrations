# Matson Navigation Company -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing. Research based on Matson's public website, online services pages, EDI documentation references, DCSA membership records, third-party aggregator listings (Terminal49, INTTRA, Shipsgo, Portcast), and community resource searches. No API credentials were obtained or used because Matson does not offer a public API.
> **Researched by**: Agent (carrier API audit workflow)
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | Matson, Inc. / Matson Navigation Company, Inc. |
| **SCAC Code** | MATS |
| **Parent Company** | Matson, Inc. (publicly traded, NYSE: MATX) |
| **Alliance** | Independent (US Jones Act carrier) |
| **Primary Services** | Container shipping, ConRo (container + roll-on/roll-off), vehicle shipping, household goods |
| **Market Position** | Dominant US Jones Act carrier for Pacific trade. Duopoly with Pasha Hawaii for Hawaii shipping. Fleet of 22 US-flagged vessels. Not a global container line -- focused on US domestic and near-Pacific routes |
| **Headquarters** | Honolulu, Hawaii, USA |
| **Website** | [https://www.matson.com](https://www.matson.com) |

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | **No** |
| **Developer portal URL** | N/A |
| **API documentation URL(s)** | N/A -- no public API documentation exists |
| **Documentation quality** | **None** -- no API documentation available. Web portal and EDI service pages exist but describe no REST/SOAP APIs |
| **OpenAPI/Swagger spec available?** | No |
| **Sandbox/test environment?** | No |
| **Developer registration** | N/A -- no developer registration process exists |
| **Developer support channels** | General customer service only. No developer-specific support. EDI setup requires contacting a Matson sales professional |
| **Community/third-party libraries** | None found -- no GitHub repos, npm packages, or PyPI packages for Matson API integration |
| **API changelog / release notes** | N/A |

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | **No** -- Matson is not among the nine DCSA member carriers. As a regional US Jones Act carrier, DCSA membership is not expected |
| **DCSA APIs implemented** | **None** |
| **DCSA TNT version** | N/A |
| **DCSA Booking version** | N/A |
| **DCSA Schedules version** | N/A |
| **Known DCSA deviations** | N/A |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | **Unknown** | Matson explicitly supports ANSI X12 (300 and 200 series). UN/EDIFACT support not confirmed -- X12 is the documented standard |
| **ANSI X12 (EDI)** | **Yes** | Ocean 300 series (300, 301, 315, 322) and Motor Carrier 200 series (204, 210, 214, 990). EDI Partner Profile available. Source: [Matson Online Services](https://www.matson.com/matnav/online_services/index.html) |
| **INTTRA integration** | **No** | Matson is not listed on INTTRA/E2open's ocean carrier network. Confirmed absent. Source: [INTTRA Ocean Carrier Network](https://www.inttra.com/ocean-carrier-network/) |
| **BIC (Bureau International des Containers)** | Yes | Container IDs follow BIC ISO 6346 format (MATSU/MATU prefixes) |
| **UN/LOCODE** | Unknown | Likely used in EDI messages but not confirmed from public documentation |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | N/A -- no API exists |
| **Auth documentation** | N/A |
| **Registration process** | N/A for API. EDI setup requires contacting Matson sales. Customer portal requires business account |
| **Registration URL** | N/A |
| **Partner program required?** | N/A for API. Yes for EDI and customer portal access |
| **Partner program URL** | N/A -- contact sales professional |
| **Credential type** | N/A |
| **Token refresh supported?** | N/A |
| **Token lifetime** | N/A |
| **Access tiers** | N/A |
| **IP whitelisting required?** | N/A |

### Access Requirements Summary for SSL

Matson does not offer a public REST/SOAP API. There is no developer portal, no API documentation, and no self-service API key issuance. The only programmatic integration path directly with Matson is EDI (ANSI X12), which requires a business relationship and coordination with a Matson sales professional.

For API-based access, SSL would need to use a third-party aggregator such as Terminal49 (confirmed Matson support), project44 (likely), or Vizion (likely). Alternatively, web scraping of the public tracking portal at matson.com/shipment-tracking.html is technically feasible but would need ToS review.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field must have a row.
> Assessment is based on **direct Matson capabilities** (web portal + EDI). Third-party aggregator availability noted separately.
> ✅ = Available | ❌ = Not available | ⚠️ = Partial / limited | ❓ = Unknown

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ⚠️ | Web: Interactive Vessel Schedule (IVS) | N/A (web-only) | N/A | Available on website and mobile app but not via API. PDF schedules also published. No programmatic access |
| 1.2 | Point-to-Point Route Options | ❌ | N/A | N/A | N/A | Not available via any programmatic interface. Routes visible on website only |
| 1.3 | Booking Lifecycle | ⚠️ | EDI: X12 300/301 | 300 (Booking Request), 301 (Booking Confirmation) | N/A | Available via EDI only. Requires business relationship and EDI setup. No REST API |
| 1.4 | Shipping Instructions | ❓ | Unknown | Unknown | N/A | Not confirmed via any public documentation. May be handled via EDI or customer portal |
| 1.5 | Rates | ❌ | N/A | N/A | N/A | No programmatic rate access. Rates handled through sales relationships |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❓ | Unknown | Unknown | `ECP` | May be included in EDI booking confirmation (X12 301) but not confirmed |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❓ | Unknown | Unknown | `EFC` | May be included in EDI booking confirmation but not confirmed |
| 2.3 | Documentation Cutoff | DCO | ⚠️ | Web portal / EDI (probable) | Unknown | `DCO` | Likely available via web portal booking details and possibly in EDI messages. Not confirmed programmatically |
| 2.4 | VGM Cutoff | VCO | ⚠️ | Web portal / EDI (probable) | Unknown | `VCO` | SOLAS requirement means Matson must communicate this. Likely in booking confirmations. Not confirmed programmatically |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ⚠️ | Web portal / EDI (probable) | Unknown | `FCO` | Terminal cutoffs likely provided in booking confirmations and on web portal. Not confirmed in EDI |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❓ | Unknown | Unknown | `LCO` | Matson's primary service is FCL. LCL cutoff availability unknown |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ❓ | Unknown | Unknown | Inferred from first EquipmentEvent | May be visible on web portal but not confirmed programmatically |
| 3.2 | Empty Container Gate-Out (Pickup) | ⚠️ | Web portal; EDI X12 315/322 | Equipment status codes | `GTOT` + `EMPTY` | Visible on web tracking portal. Available via EDI 315 (Status Details -- Ocean) and 322 (Equipment Movement). No API |
| 3.3 | Full Container Gate-In | ⚠️ | Web portal; EDI X12 315/322 | Equipment status codes | `GTIN` + `LADEN` | Same as 3.2 -- visible on portal, available via EDI |
| 3.4 | Container Loaded on Vessel | ⚠️ | Web portal; EDI X12 315 | Status code for vessel load | `LOAD` + `LADEN` | Visible on web tracking. Available via EDI 315 |
| 3.5 | Container Discharged at Transshipment | ⚠️ | Web portal; EDI X12 315 | Status code for discharge | `DISC` + `LADEN` + transshipment | Matson operates mostly direct services with limited transshipment. When applicable, likely in EDI 315 |
| 3.6 | Container Loaded at Transshipment | ⚠️ | Web portal; EDI X12 315 | Status code for reload | `LOAD` + `LADEN` + transshipment | Same as 3.5 -- limited applicability for Matson's direct service routes |
| 3.7 | Container Discharged at Destination | ⚠️ | Web portal; EDI X12 315 | Status code for discharge | `DISC` + `LADEN` | Core milestone visible on web tracking and available via EDI |
| 3.8 | Full Container Gate-Out (Delivery) | ⚠️ | Web portal; EDI X12 315/322 | Equipment status codes | `GTOT` + `LADEN` | Visible on web tracking. Available via EDI |
| 3.9 | Empty Container Returned | ⚠️ | Web portal; EDI X12 315/322 | Equipment status codes | `GTIN` + `EMPTY` | Visible on web tracking. Available via EDI |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ⚠️ | Web: IVS schedule; GPS tracking | N/A (web-only) | `DEPA` + classifier | Available on Interactive Vessel Schedule and GPS tracking pages. No programmatic access |
| 4.2 | Estimated Time of Arrival | ETA | ⚠️ | Web: IVS schedule; GPS tracking; shipment tracking | N/A (web-only) | `ARRI` + classifier | Available on web tracking and vessel schedule. No programmatic access |
| 4.3 | Vessel Arrival at Transshipment | -- | ❓ | Unknown | Unknown | `ARRI` at intermediate | Limited applicability -- Matson operates mostly direct services |
| 4.4 | Vessel Departure from Transshipment | -- | ❓ | Unknown | Unknown | `DEPA` at intermediate | Limited applicability -- same as 4.3 |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❌ | No webhook or push notification API exists |
| Event Polling with timestamp filter | ❌ | No polling API exists. EDI 315 provides status updates but not via polling |
| Event Classifier Progression (PLN->EST->ACT) | ❌ | No DCSA event model. Web portal may show schedule changes but not programmatically |
| Retracted Events | ❌ | Not applicable -- no event API |
| Change Remarks | ❌ | Not available programmatically |
| Delay Reason Codes | ❌ | Not available programmatically |

### Coverage Summary

| Category | Fields Available | Fields Unavailable | Fields Unknown | Coverage % |
|----------|-----------------|-------------------|----------------|-----------|
| API Domains (1.x) | 0/5 | 2/5 | 1/5 | 0% (2 partial via web/EDI, 1 unknown) |
| Cutoffs (2.x) | 0/6 | 0/6 | 3/6 | 0% (3 partial via web/EDI, 3 unknown) |
| Container Milestones (3.x) | 0/9 | 0/9 | 1/9 | 0% (8 partial via web/EDI, 1 unknown) |
| Transport Events (4.x) | 0/4 | 0/4 | 2/4 | 0% (2 partial via web/IVS, 2 unknown) |
| Change Detection (5.x) | 0/6 | 6/6 | 0/6 | 0% |
| **Total** | **0/30** | **8/30** | **7/30** | **0% via API (50% partial via web/EDI, 23% unknown)** |

> **Coverage note**: The 0% coverage reflects the absence of any REST/SOAP API. Many fields are marked Unknown rather than Unavailable because Matson's EDI (X12 315, 322, 300, 301) and web portal likely expose this data, but it cannot be accessed via a modern API. Via third-party aggregators (especially Terminal49), effective coverage improves significantly -- see Third-Party Aggregators section below.
>
> **EDI-adjusted assessment**: If EDI (X12) is considered an acceptable integration method, estimated coverage rises to approximately 50-60% for container milestones and booking lifecycle, though cutoff and change detection coverage remains uncertain.

---

## Endpoint Reference

Matson does not expose REST/SOAP API endpoints. This section is replaced by the EDI transaction reference below.

### EDI Transaction Reference

| X12 Transaction | Description | Direction | Series | SSL Relevance |
|----------------|-------------|-----------|--------|---------------|
| 300 | Reservation Booking Request | Outbound (to Matson) | Ocean | Booking lifecycle |
| 301 | Confirmation (Booking) | Inbound (from Matson) | Ocean | Booking confirmation, may include cutoffs |
| 315 | Status Details (Ocean) | Inbound (from Matson) | Ocean | Container milestones, vessel events |
| 322 | Terminal Operations and Intermodal Ramp Activity | Inbound (from Matson) | Ocean | Equipment movements at terminals |
| 204 | Motor Carrier Load Tender | Outbound (to Matson) | Motor | Drayage/trucking |
| 210 | Motor Carrier Freight Details and Invoice | Inbound (from Matson) | Motor | Freight billing |
| 214 | Transportation Carrier Shipment Status | Inbound (from Matson) | Motor | Trucking status updates |
| 990 | Response to a Load Tender | Inbound (from Matson) | Motor | Load tender acknowledgment |

Source: [Matson Online Services](https://www.matson.com/matnav/online_services/index.html), [Matson EDI Partner Profile](https://www.matson.com/matnav/online_services/forms/Matson_EDI_Partner_Profile.doc)

### Lookup Methods Summary

| Identifier Type | Supported? | Which Endpoints? | Notes |
|----------------|-----------|-----------------|-------|
| **Bill of Lading (B/L) number** | ⚠️ Web only | Web tracking portal | Supported on matson.com/shipment-tracking.html. No API |
| **Booking reference** | ⚠️ Web + EDI | Web tracking portal; EDI 300/301 | Web portal and EDI booking flow |
| **Container number** | ⚠️ Web only | Web tracking portal | Primary lookup on portal. No API |
| **Carrier booking number** | ⚠️ Web only | Web tracking portal | Same as booking reference for Matson |
| **Vessel IMO / voyage** | ⚠️ Web only | Interactive Vessel Schedule | Vessel schedule lookup on IVS page. No API |

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

Matson does not support webhooks or push notifications via API.

The **FaxTrack** service provides daily shipment status information via fax and email. This is a legacy notification mechanism, not a webhook system. Configuration requires contacting Matson customer service.

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | [https://www.matson.com/shipment-tracking.html](https://www.matson.com/shipment-tracking.html) |
| **Login required?** | No -- basic container status is public. Advanced features require customer portal login |
| **Data available on portal but NOT in API** | All tracking data is portal-only since no API exists. Includes: current container status, movement history, shipment details, vessel schedules, GPS vessel positions, gate cam images |
| **Scraping feasibility** | Feasible -- standard server-rendered HTML pages. No obvious anti-bot measures observed. ToS review required before implementation |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | **Yes** -- primary programmatic integration method |
| **EDI message types** | ANSI X12: 300, 301, 315, 322 (Ocean series); 204, 210, 214, 990 (Motor Carrier series) |
| **EDI connection method** | Unknown -- not publicly documented. Estimated: VAN or AS2 (industry standard) |
| **EDI documentation** | [Matson EDI Partner Profile](https://www.matson.com/matnav/online_services/forms/Matson_EDI_Partner_Profile.doc) (.doc download). Setup requires contacting Matson sales |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Likely Yes | project44 claims 98%+ global ocean freight coverage. Matson not specifically named but coverage is probable. Contact project44 for confirmation |
| **FourKites** | Unknown | No specific evidence of Matson integration found |
| **Vizion** | Likely Yes | Vizion claims 99% ocean freight coverage. Not specifically confirmed for Matson |
| **INTTRA / E2open** | **No** | Matson is NOT listed on INTTRA's ocean carrier network. Confirmed absent. Source: [INTTRA Carrier Network](https://www.inttra.com/ocean-carrier-network/) |
| **CargoSmart** | Unknown | No specific evidence found |
| **Terminal49** | **Yes** | Confirmed Matson (MATS) support. Tracks B/L and Booking numbers. Container number lookup unsupported. Provides container milestones including port operations, vessel movements, rail events. Source: [Terminal49 Matson page](https://terminal49.com/shipping-lines/mats-matson-navigation-company-container-tracking) |
| **Shipsgo** | **Yes** | Offers Matson tracking API. Source: [Shipsgo Matson](https://shipsgo.com/ocean/carriers/matson/container-tracking) |
| **Portcast** | **Yes** | Offers Matson container tracking with predictive ETAs. Source: [Portcast Matson](https://www.portcast.io/carrier-coverage/matson-container-tracking) |

> **Aggregator note**: Since Matson has no direct API, third-party aggregators are the only path to REST API-based tracking. Terminal49 is the best-documented option with confirmed Matson support and detailed milestone coverage. Terminal49 likely obtains data by scraping Matson's web portal or through a private data-sharing arrangement.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown -- no API to measure. Web portal updates are estimated to be within hours of physical events based on industry norms for US domestic carriers | Estimated |
| **API uptime/reliability** | N/A -- no API | N/A |
| **Historical data depth** | 90 days on web portal | Official (matson.com tracking page) |
| **Timezone handling** | Unknown -- web portal likely uses US Pacific or local port time. Matson routes span multiple time zones (US West Coast, Hawaii, Alaska, Guam, Asia) | Estimated |
| **Character encoding** | Unknown | Unknown |

### Known Issues & Gotchas

- **No API at all**: The most fundamental limitation. All programmatic integration requires either EDI (heavyweight, requires business relationship) or third-party aggregators (additional vendor dependency and cost)
- **Regional carrier scope**: Matson serves only US domestic Jones Act routes (Hawaii, Alaska, Guam) and limited Asia-Pacific routes. Not a global carrier -- do not expect worldwide port coverage
- **Container number tracking gap at Terminal49**: Terminal49 does not support container number lookups for Matson -- only B/L and Booking numbers work
- **EDI is legacy**: X12 EDI is functional but heavyweight to implement compared to REST APIs. Requires VAN/AS2 setup and carrier coordination
- **Limited transshipment visibility**: Matson operates mostly direct services with minimal transshipment, so transshipment-related fields (3.5, 3.6, 4.3, 4.4) have limited practical applicability

### Recently Deprecated or Changed

- No known recent deprecations. Matson's digital offerings appear stable and unchanged

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | Partial -- via third-party aggregator (Terminal49 recommended) or web scraping. No direct API integration possible |
| **Implementation effort** | High (no direct API; aggregator dependency or scraping required) |
| **DCSA base adapter usable?** | No -- fully custom. Matson has no DCSA compliance |

### Recommended Approach

The recommended approach for Matson is a **third-party aggregator adapter**, with Terminal49 as the primary data source. Terminal49 has confirmed Matson (MATS) carrier support and provides container milestone tracking via B/L and Booking number lookups.

The adapter would be built as a Terminal49 API client that maps Terminal49's standardized event format to SSL's canonical data model. This avoids the need for web scraping (fragile, ToS concerns) or EDI integration (heavyweight, requires business relationship). The downside is an additional vendor dependency and cost, but this is the most practical path for a carrier with no public API.

If SSL establishes a direct business relationship with Matson for EDI, a secondary EDI-based adapter could be built to receive X12 315 (status) and 322 (equipment movement) transactions. This would provide more reliable and potentially more comprehensive data than the aggregator path, but requires significant setup effort.

### Recommended Lookup Method

**Bill of Lading number** is the recommended primary lookup identifier. It is supported on both the web portal and Terminal49. Booking number is a secondary option. Container number lookup is not supported via Terminal49 for Matson and should not be relied upon.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Every 4 hours via Terminal49 (Matson's routes are relatively short -- 4-5 days US West Coast to Hawaii -- so 4-hour polling provides adequate granularity) |
| **Incremental filter** | Depends on aggregator API. Terminal49 supports event-based updates with webhooks. Use webhook subscription if available; otherwise poll for updated events |
| **Batch tracking** | Terminal49 API allows tracking multiple shipments. One API call per shipment for status retrieval |

### Auth Implementation Notes

Authentication depends on the chosen aggregator. For Terminal49: API key-based authentication. For direct Matson integration: N/A (EDI uses VAN/AS2 transport-level authentication, not HTTP-level auth).

### Edge Cases to Handle

- **Limited transshipment**: Matson's mostly-direct service routes mean transshipment events (3.5, 3.6, 4.3, 4.4) will rarely occur. Adapter should handle their absence gracefully
- **Jones Act routes only**: Matson does not provide global container service. Adapter should validate that requested shipments are on Matson's service routes
- **Container number lookup failure**: Terminal49 does not support container number lookup for Matson. Adapter must require B/L or Booking number and should return clear errors for container-only lookups
- **Intermodal handoff**: Matson provides both ocean and domestic trucking services (200-series EDI). Container may have ocean and motor carrier legs under the same Matson booking
- **ConRo cargo**: Matson carries vehicles and roll-on/roll-off cargo alongside containers. Some bookings may be for non-containerized cargo

### Mapping Complexity

**High complexity**. Since Matson has no API or DCSA compliance, all data mapping must go through a third-party aggregator's format (Terminal49) or be reverse-engineered from web portal scraping. Terminal49 provides a somewhat standardized format, but the mapping from Terminal49 events to SSL's canonical fields requires custom logic. The lack of DCSA event codes means no reusable DCSA mapping layer can be applied.

If EDI is used, X12 315 status codes must be mapped to SSL's canonical milestones. X12 uses different code sets (e.g., STP status codes) than DCSA event codes, requiring a dedicated translation layer.

---

## Open Questions

- [ ] Does SSL have an existing business relationship with Matson that would enable EDI integration?
- [ ] Is Terminal49 already in SSL's vendor stack, or would this require a new vendor agreement?
- [ ] What is Matson's web portal ToS regarding automated data retrieval (scraping)?
- [ ] Do Matson's EDI 315 messages include cutoff dates (DCO, VCO, FCO) or only movement status codes?
- [ ] Does Matson provide any private/partner API that is not publicly documented?
- [ ] What is the exact EDI connection method (VAN, AS2, SFTP) and which VANs does Matson support?
- [ ] Are project44 and Vizion confirmed to cover Matson, or only assumed from their global coverage claims?

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | [https://www.matson.com](https://www.matson.com) |
| Ocean Shipping Division | [https://www.matson.com/matnav/index.html](https://www.matson.com/matnav/index.html) |
| Online Services | [https://www.matson.com/matnav/online_services/index.html](https://www.matson.com/matnav/online_services/index.html) |
| Shipment Tracking (Public) | [https://www.matson.com/shipment-tracking.html](https://www.matson.com/shipment-tracking.html) |
| Interactive Vessel Schedule | [https://www.matson.com/matnav/schedules/interactive_vessel_schedule.html](https://www.matson.com/matnav/schedules/interactive_vessel_schedule.html) |
| GPS Vessel Tracking | [https://www.matson.com/track.html](https://www.matson.com/track.html) |
| Mobile App (iOS) | [https://apps.apple.com/us/app/track-my-container/id1299640687](https://apps.apple.com/us/app/track-my-container/id1299640687) |
| Mobile App (Android) | [https://play.google.com/store/apps/details?id=com.matson.containertrack](https://play.google.com/store/apps/details?id=com.matson.containertrack) |
| EDI Partner Profile | [https://www.matson.com/matnav/online_services/forms/Matson_EDI_Partner_Profile.doc](https://www.matson.com/matnav/online_services/forms/Matson_EDI_Partner_Profile.doc) |
| Terminal49 Matson Page | [https://terminal49.com/shipping-lines/mats-matson-navigation-company-container-tracking](https://terminal49.com/shipping-lines/mats-matson-navigation-company-container-tracking) |
| Shipsgo Matson Tracking | [https://shipsgo.com/ocean/carriers/matson/container-tracking](https://shipsgo.com/ocean/carriers/matson/container-tracking) |
| Portcast Matson Tracking | [https://www.portcast.io/carrier-coverage/matson-container-tracking](https://www.portcast.io/carrier-coverage/matson-container-tracking) |
| INTTRA Carrier Network (Matson absent) | [https://www.inttra.com/ocean-carrier-network/](https://www.inttra.com/ocean-carrier-network/) |
| DCSA Website (Matson not a member) | [https://dcsa.org/](https://dcsa.org/) |
| Wikipedia -- Matson, Inc. | [https://en.wikipedia.org/wiki/Matson,_Inc.](https://en.wikipedia.org/wiki/Matson,_Inc.) |
