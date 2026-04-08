# Turkon America Line -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing
> **Researched by**: Agent
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | Turkon Container Transportation and Shipping Inc. (commonly "Turkon Line" or "Turkon America Line") |
| **SCAC Code** | TRKU |
| **Parent Company** | Privately owned (Turkish) |
| **Alliance** | Independent (no alliance membership) |
| **Primary Services** | Container shipping (FCL), East Mediterranean-US transatlantic trade, intra-Mediterranean services |
| **Market Position** | Niche regional carrier specializing in Turkey-US and Turkey-Europe trade corridors. Operates ~26 vessels with ~35,000 TEU capacity. One of the top five Turkish container operators |
| **Headquarters** | Istanbul, Turkey |
| **Website** | https://turkon.com/en |

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | No |
| **Developer portal URL** | N/A |
| **API documentation URL(s)** | N/A -- no public API documentation found |
| **Documentation quality** | None |
| **OpenAPI/Swagger spec available?** | No |
| **Sandbox/test environment?** | No |
| **Developer registration** | N/A |
| **Developer support channels** | General contact via turkon.com; no developer-specific channels |
| **Community/third-party libraries** | None found for direct Turkon API. Third-party aggregators (Terminal49, ShipsGo, Portcast, TRADLINX) provide Turkon tracking as part of multi-carrier platforms |
| **API changelog / release notes** | Not published |

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | No -- DCSA members are MSC, Maersk, CMA CGM, Hapag-Lloyd, ONE, Evergreen, Yang Ming, HMM, ZIM, and PIL. Turkon is not a member |
| **DCSA APIs implemented** | None |
| **DCSA TNT version** | N/A |
| **DCSA Booking version** | N/A |
| **DCSA Schedules version** | N/A |
| **Known DCSA deviations** | N/A -- Turkon does not implement DCSA APIs |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Yes | Booking requests, shipping instructions, and tracking via INTTRA/e2open |
| **INTTRA integration** | Yes | Turkon joined the INTTRA carrier network in July 2018. Provides booking requests, shipping instructions, and Track and Trace through INTTRA |
| **BIC (Bureau International des Containers)** | Yes | Standard container ID format (TRKU prefix) |
| **UN/LOCODE** | Unknown | Port codes used internally not documented |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | N/A -- no public API |
| **Auth documentation** | N/A |
| **Registration process** | N/A -- no developer registration available |
| **Registration URL** | N/A |
| **Partner program required?** | N/A |
| **Partner program URL** | N/A |
| **Credential type** | N/A |
| **Token refresh supported?** | N/A |
| **Token lifetime** | N/A |
| **Access tiers** | N/A |
| **IP whitelisting required?** | N/A |

### Access Requirements Summary for SSL

Turkon Line does not offer a public API or developer portal. There is no self-service or partnership-based API access path. SSL cannot obtain direct API credentials from Turkon.

For tracking data, SSL should use a third-party aggregator such as Terminal49 (which confirms Turkon/TRKU support with container milestones) or ShipsGo. For booking and shipping instructions, INTTRA/e2open is the established digital channel, as Turkon has been on the INTTRA network since July 2018.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field has a row.
> Availability legend: check = Available | x = Not available | warning = Partial / limited | question = Unknown
>
> **Note:** Since Turkon has no public API, "Available?" reflects what can be obtained through the primary aggregator pathway (Terminal49 for tracking, INTTRA for booking/SI). Web portal tracking at my.turkon.com is also considered.

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ❌ | N/A | N/A | N/A | No schedule API. Schedules available on turkon.com website and via third-party platforms (Fluent Cargo) but not programmatically from Turkon |
| 1.2 | Point-to-Point Route Options | ❌ | N/A | N/A | N/A | No routing API |
| 1.3 | Booking Lifecycle | ⚠️ | INTTRA/e2open | Booking requests via INTTRA EDI | N/A | Booking submission available through INTTRA since July 2018. No REST API from Turkon directly |
| 1.4 | Shipping Instructions | ⚠️ | INTTRA/e2open | Shipping instructions via INTTRA EDI | N/A | SI submission available through INTTRA. No REST API from Turkon directly |
| 1.5 | Rates | ❌ | N/A | N/A | N/A | No rate API. Rates handled through traditional sales channels |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❓ | Unknown | Unknown | `ECP` | Not available via aggregators. May be communicated in booking confirmation via INTTRA |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❓ | Unknown | Unknown | `EFC` | Not available via aggregators. May be communicated in booking confirmation via INTTRA |
| 2.3 | Documentation Cutoff | DCO | ❓ | Unknown | Unknown | `DCO` | May be available via INTTRA booking confirmation or web portal. Not confirmed |
| 2.4 | VGM Cutoff | VCO | ❓ | Unknown | Unknown | `VCO` | May be available via INTTRA or web portal. Not confirmed |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ❓ | Unknown | Unknown | `FCO` | May be available via INTTRA booking confirmation or web portal. Not confirmed |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❓ | Unknown | Unknown | `LCO` | May be available via INTTRA booking confirmation or web portal. Not confirmed |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ❓ | N/A | N/A | Inferred from first EquipmentEvent | Not exposed through aggregators. May be inferred from first tracking event |
| 3.2 | Empty Container Gate-Out (Pickup) | ✅ | Terminal49 API / ShipsGo | "Empty Out" milestone | `GTOT` + `EMPTY` | Terminal49 confirms "Empty Out" milestone supported for TRKU |
| 3.3 | Full Container Gate-In | ✅ | Terminal49 API / ShipsGo | "Full In" milestone | `GTIN` + `LADEN` | Terminal49 confirms "Full In" milestone supported for TRKU |
| 3.4 | Container Loaded on Vessel | ✅ | Terminal49 API / ShipsGo | "Vessel Loaded" milestone | `LOAD` + `LADEN` | Terminal49 confirms "Vessel Loaded" milestone supported for TRKU |
| 3.5 | Container Discharged at Transshipment | ✅ | Terminal49 API / ShipsGo | "Transshipment Discharged" milestone | `DISC` + `LADEN` + transshipment | Terminal49 confirms "Transshipment Discharged" milestone supported for TRKU |
| 3.6 | Container Loaded at Transshipment | ✅ | Terminal49 API / ShipsGo | "Transshipment Loaded" milestone | `LOAD` + `LADEN` + transshipment | Terminal49 confirms "Transshipment Loaded" milestone supported for TRKU |
| 3.7 | Container Discharged at Destination | ✅ | Terminal49 API / ShipsGo | "Vessel Discharged" milestone | `DISC` + `LADEN` | Terminal49 confirms "Vessel Discharged" milestone supported for TRKU |
| 3.8 | Full Container Gate-Out (Delivery) | ✅ | Terminal49 API / ShipsGo | "Full Out" milestone | `GTOT` + `LADEN` | Terminal49 confirms "Full Out" milestone supported for TRKU |
| 3.9 | Empty Container Returned | ✅ | Terminal49 API / ShipsGo | "Empty Returned" milestone | `GTIN` + `EMPTY` | Terminal49 confirms "Empty Returned" milestone supported for TRKU |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ⚠️ | Terminal49 API / ShipsGo | ETA/ETD data in tracking | `DEPA` + classifier | Available through aggregators as part of tracking data. No direct schedule API |
| 4.2 | Estimated Time of Arrival | ETA | ⚠️ | Terminal49 API / ShipsGo | ETA data in tracking | `ARRI` + classifier | Available through aggregators. Terminal49 provides ETAs for TRKU shipments |
| 4.3 | Vessel Arrival at Transshipment | -- | ⚠️ | Terminal49 API | "Vessel Arrived" at intermediate port | `ARRI` at intermediate | Terminal49 confirms "Vessel Arrived" milestone. Transshipment context distinguishable by port |
| 4.4 | Vessel Departure from Transshipment | -- | ❓ | Unknown | Unknown | `DEPA` at intermediate | Not explicitly confirmed by aggregator documentation. May be inferred from transshipment load event |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ⚠️ | Not from Turkon directly. Terminal49 provides webhook notifications for TRKU containers. ShipsGo offers tracking API with ETA updates |
| Event Polling with timestamp filter | ⚠️ | Not from Turkon directly. Terminal49 API supports polling for TRKU container updates |
| Event Classifier Progression (PLN->EST->ACT) | ❌ | No DCSA classifier system. Turkon is not DCSA-compliant |
| Retracted Events | ❌ | No retraction mechanism available |
| Change Remarks | ❌ | No change remark field available |
| Delay Reason Codes | ❌ | No delay reason codes available |

### Coverage Summary

| Category | Fields Available | Fields Partial | Fields Unavailable | Fields Unknown | Coverage % |
|----------|-----------------|---------------|-------------------|----------------|-----------|
| API Domains (1.x) | 0/5 | 2/5 | 3/5 | 0/5 | 0% confirmed (2 partial via INTTRA) |
| Cutoffs (2.x) | 0/6 | 0/6 | 0/6 | 6/6 | 0% (all unknown) |
| Container Milestones (3.x) | 8/9 | 0/9 | 0/9 | 1/9 | 89% (via Terminal49 aggregator) |
| Transport Events (4.x) | 0/4 | 3/4 | 0/4 | 1/4 | 0% confirmed (3 partial via aggregator) |
| Change Detection (5.x) | 0/6 | 2/6 | 4/6 | 0/6 | 0% (2 partial via aggregator) |
| **Total** | **8/30** | **7/30** | **7/30** | **8/30** | **27% confirmed (23% partial, 27% unknown)** |

> **Notes on Coverage:**
> - Turkon has no public API, so all tracking data comes through third-party aggregators (primarily Terminal49 and ShipsGo).
> - Terminal49 provides strong container milestone coverage for TRKU, confirming 8 of 9 milestones including transshipment events.
> - Cutoff data is entirely unknown -- it may be available through INTTRA booking confirmations but this cannot be confirmed from desk research.
> - Transport events (ETD/ETA) are partially available through aggregator tracking data but without DCSA classifier progression.
> - Change detection relies entirely on aggregator capabilities (Terminal49 webhooks, ShipsGo alerts), not Turkon's own systems.
> - INTTRA provides booking and SI submission but is an EDI channel, not a REST API.

---

## Endpoint Reference

Turkon does not expose public API endpoints. This section documents the aggregator and EDI access paths instead.

### Tracking / Events (via Aggregators)

| Platform | Method | Lookup Params | Response Format | Notes |
|----------|--------|--------------|----------------|-------|
| Terminal49 API | REST API | B/L, Booking, Container number | JSON | Confirmed TRKU support. Milestones, ETAs, port data. Free tier: 100 containers |
| ShipsGo API | REST API | Container number, B/L | JSON | Turkon tracking API with unlimited calls. ETA predictions |
| Portcast | REST API | Container number | JSON | Real-time and predictive tracking for Turkon |
| TRADLINX | REST API | Container number, B/L, Booking | JSON | Combines carrier data, AIS, and AI for Turkon tracking |

### Booking / Shipping Instructions (via INTTRA/e2open)

| Channel | Method | Capabilities | Notes |
|---------|--------|-------------|-------|
| INTTRA/e2open | EDI (IFTMIN, COPARN) | Booking requests, shipping instructions, Track and Trace | Turkon joined INTTRA network July 2018 |

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | https://my.turkon.com/container-tracking |
| **Login required?** | No -- basic tracking available without login |

### Lookup Methods Summary

| Identifier Type | Supported? | Which Endpoints? | Notes |
|----------------|-----------|-----------------|-------|
| **Bill of Lading (B/L) number** | ✅ | Terminal49, ShipsGo, web portal | Supported by aggregators and web portal |
| **Booking reference** | ✅ | Terminal49, INTTRA, web portal | Supported by aggregators and web portal |
| **Container number** | ✅ | Terminal49, ShipsGo, Portcast, TRADLINX, web portal | Most widely supported lookup method across all platforms |
| **Carrier booking number** | ✅ | Same as booking reference | |
| **Vessel IMO / voyage** | ❌ | Not supported as lookup param | No schedule API or vessel-based lookup |

---

## Rate Limits & Quotas

| Detail | Value | Source |
|--------|-------|--------|
| **Global rate limit** | N/A -- no direct API | N/A |
| **Per-endpoint limits** | N/A | N/A |
| **Daily/monthly quota** | N/A | N/A |
| **Rate limit response** | N/A | N/A |
| **Rate limit by** | N/A | N/A |
| **Burst allowance** | N/A | N/A |
| **Different tiers** | N/A | N/A |

> Rate limits depend on the chosen aggregator. Terminal49 free tier supports 100 containers. ShipsGo claims unlimited API calls. Contact aggregators for production-tier limits and pricing.

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | https://my.turkon.com/container-tracking |
| **Login required?** | No -- basic container tracking without login |
| **Data available on portal but NOT in API** | All Turkon data is only on the portal or via aggregators -- there is no direct API. Portal shows container status, vessel info, ETD/ETA, and port details |
| **Scraping feasibility** | Not assessed -- aggregator integration strongly preferred over scraping |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Yes |
| **EDI message types** | Booking requests, shipping instructions, Track and Trace (specific EDIFACT message types not documented but INTTRA standard set likely includes IFTMIN, COPARN, IFTSTA) |
| **EDI connection method** | Via INTTRA/e2open platform |
| **EDI documentation** | Contact INTTRA/e2open. Partnership announcement: https://www.inttra.com/newsroom/inttra-adds-turkon-line-to-its-carrier-network/ |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Unknown | Not explicitly confirmed for Turkon. project44 covers 55+ shipping lines; Turkon may be included given US trade focus but not verified |
| **FourKites** | Unknown | Not explicitly confirmed. FourKites covers 85+ ocean carriers |
| **Vizion** | Unknown | Vizion claims 99% ocean freight coverage. Turkon likely covered but not explicitly confirmed |
| **INTTRA / E2open** | Yes | Confirmed. Turkon joined INTTRA carrier network July 2018. Provides booking, SI, and Track and Trace |
| **Terminal49** | Yes | Confirmed. TRKU explicitly listed with milestone tracking, ETAs, and API support. Supports B/L, booking, and container number lookups |
| **ShipsGo** | Yes | Confirmed. Offers Turkon tracking API with ETA information and unlimited API calls |
| **Portcast** | Yes | Confirmed. Real-time and predictive tracking for Turkon containers |
| **TRADLINX** | Yes | Confirmed. Combines carrier data, AIS, and AI for Turkon tracking |

> **Aggregator note:** Since Turkon has no direct API, aggregator integration is the only programmatic path for tracking data. Terminal49 provides the most comprehensive milestone coverage confirmed for TRKU, including all core container milestones and transshipment events. For booking and SI, INTTRA/e2open is the established channel. SSL should evaluate Terminal49 as the primary tracking data source for Turkon shipments.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown from Turkon directly. Terminal49 claims "updates within minutes" from carrier and terminal sources | Reported (Terminal49) |
| **API uptime/reliability** | N/A for direct API. Depends on chosen aggregator's SLA | N/A |
| **Historical data depth** | Unknown | Unknown |
| **Timezone handling** | Unknown from Turkon. Terminal49 provides timezone data for ports | Reported (Terminal49) |
| **Character encoding** | Unknown | Unknown |

### Known Issues & Gotchas

- **No direct API**: Turkon is a small regional carrier with no public API or developer portal. All programmatic access must go through third-party aggregators or INTTRA EDI.

- **Aggregator dependency**: Tracking data quality and completeness depend entirely on the chosen aggregator's integration with Turkon. Terminal49 shows the most complete milestone coverage but seal numbers and weight data are not available for TRKU shipments.

- **Destination data gaps**: Terminal49 reports that "Destination Name" and "Destination Locode" are unsupported for TRKU shipments, meaning final destination details may need to be sourced from booking data rather than tracking events.

- **No cutoff data via aggregators**: Cutoff timestamps (DCO, VCO, FCO, etc.) are not available through tracking aggregators. These are typically communicated in booking confirmations, which would come via INTTRA EDI, not REST API.

- **Limited fleet and route coverage**: Turkon operates ~26 vessels primarily on Turkey-US and Mediterranean routes. Shipments outside these corridors are unlikely.

- **INTTRA onboarding required**: To use booking and SI capabilities, SSL needs an INTTRA/e2open account and connectivity, which is a separate onboarding process from the carrier itself.

### Recently Deprecated or Changed

- No deprecation notices found. Turkon's digital footprint is minimal and has not changed significantly.

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | Partial -- tracking only via aggregator (Terminal49 or ShipsGo). No direct carrier API exists. Booking/SI only via INTTRA EDI (not REST) |
| **Implementation effort** | Medium -- aggregator passthrough for tracking. The adapter wraps Terminal49 or ShipsGo API rather than a carrier API directly |
| **DCSA base adapter usable?** | No -- Turkon is not DCSA-compliant. However, Terminal49's normalized output may align reasonably well with DCSA event types |

### Recommended Approach

The Turkon adapter should be implemented as an **aggregator-passthrough adapter** rather than a direct carrier integration. The recommended architecture:

1. **Tracking**: Use Terminal49 API as the primary data source. Terminal49 confirms comprehensive milestone coverage for TRKU including all core container events (empty out, full in, vessel loaded/discharged, transshipment loaded/discharged, full out, empty returned) plus ETAs and port data. Terminal49 provides a free developer tier (100 containers) for initial development and testing. The adapter would map Terminal49's normalized event format to SSL's canonical DCSA model.

2. **Booking/SI**: If SSL needs booking or shipping instruction capabilities for Turkon, this must go through INTTRA/e2open EDI. This is a separate integration path from the REST-based tracking adapter and would likely be handled by a dedicated INTTRA adapter that covers multiple carriers, not a Turkon-specific implementation.

3. **Change Detection**: Use Terminal49's webhook capability for push-based milestone updates. Terminal49 sends notifications when container statuses change, providing near-real-time updates without polling.

### Recommended Lookup Method

**Container number** is the most broadly supported lookup across all aggregators and the web portal. For Terminal49 specifically, B/L, booking, and container number are all supported, so **B/L number** is recommended as the primary lookup for consistency with other carrier adapters.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Every 2-4 hours via Terminal49 API. Alternatively, use Terminal49 webhooks for event-driven updates (preferred) |
| **Incremental filter** | Terminal49 pushes updates via webhooks when container status changes. For polling, re-fetch container status and diff against local state |
| **Batch tracking** | Terminal49 supports adding multiple containers programmatically. One subscription per container, but bulk operations available via API |

### Auth Implementation Notes

No Turkon-specific auth needed. Auth is handled by the aggregator:
- **Terminal49**: API key-based authentication. Free developer key for up to 100 containers. Production keys available on request.
- **ShipsGo**: API key-based authentication. Claims unlimited API calls.
- **INTTRA/e2open**: Separate EDI onboarding with INTTRA-specific credentials and connectivity requirements.

### Edge Cases to Handle

- **Destination data missing**: Terminal49 reports destination name and locode as unsupported for TRKU. The adapter should gracefully handle missing destination data and potentially fill it from booking or SI data.

- **No seal number or weight data**: Terminal49 confirms these fields are unsupported for TRKU. The adapter should not expect these fields.

- **Route concentration**: Turkon operates primarily Turkey-US and Mediterranean routes. Shipments outside these corridors would not exist.

- **Aggregator failover**: If Terminal49 is unavailable, ShipsGo or Portcast could serve as fallback tracking sources. The adapter could support multiple aggregator backends.

### Mapping Complexity

**Low-to-medium complexity.** The mapping challenge is significantly reduced by using Terminal49 as an intermediary:

1. **Terminal49 normalization**: Terminal49 already normalizes carrier data into standardized milestones (Empty Out, Full In, Vessel Loaded, etc.) that map cleanly to DCSA equipment events (GTOT+EMPTY, GTIN+LADEN, LOAD+LADEN, etc.).

2. **Missing fields**: The main complexity is handling the fields Terminal49 does not provide for TRKU (destination locode, seal number, weight, cutoffs). The adapter needs clean fallback logic.

3. **No classifier progression**: Without DCSA PLN/EST/ACT classifiers, the adapter cannot distinguish planned vs. estimated vs. actual for transport events. ETD/ETA changes must be detected by comparing values between polls.

4. **Cutoff data gap**: Cutoff timestamps are not available through the tracking aggregator path. If SSL needs cutoffs for Turkon shipments, a separate INTTRA integration would be required.

---

## Open Questions

- [ ] Does SSL have an INTTRA/e2open account? -- Required for booking/SI capabilities with Turkon
- [ ] Does project44 cover Turkon (TRKU)? -- Would provide another aggregator option if SSL already uses project44
- [ ] Does Vizion cover Turkon? -- Same rationale as project44
- [ ] What cutoff data does Turkon provide in INTTRA booking confirmations? -- Determines whether DCO, VCO, FCO, etc. can be obtained
- [ ] What is Terminal49's pricing for production-tier TRKU tracking? -- Free tier limited to 100 containers
- [ ] Does Turkon plan to develop a public API? -- Small carriers sometimes adopt DCSA over time
- [ ] What volume of Turkon shipments does SSL handle? -- Determines whether aggregator pricing is justified
- [ ] Does the Turkon web portal (my.turkon.com) expose any undocumented API endpoints? -- Browser dev tools inspection could reveal REST calls made by the portal

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | https://turkon.com/en |
| Container Tracking Portal | https://my.turkon.com/container-tracking |
| Online Services Page | https://turkon.com/en/online-services |
| Fleet Information | https://turkon.com/en/solutions/fleet |
| FAQ | https://turkon.com/en/frequently-asked-questions |
| INTTRA Partnership Announcement | https://www.inttra.com/newsroom/inttra-adds-turkon-line-to-its-carrier-network/ |
| AJOT INTTRA Announcement | https://www.ajot.com/news/inttra-adds-turkon-line-to-its-carrier-network |
| Terminal49 TRKU Tracking | https://terminal49.com/shipping-lines/trku-turkon-line-container-tracking |
| ShipsGo Turkon Tracking | https://shipsgo.com/ocean/carriers/turkon/container-tracking |
| Portcast Turkon Tracking | https://www.portcast.io/carrier-coverage/turkon-line-container-tracking |
| Fluent Cargo TRKU Schedules | https://www.fluentcargo.com/carriers/scac/TRKU |
| GoComet Turkon Tracking | https://www.gocomet.com/online-container-tracking/carriers/turkon |
| Beacon Turkon Tracking | https://www.beacon.com/tracking/container/turkon |
