# Wan Hai Lines -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing
> **Researched by**: Claude (automated)
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | Wan Hai Lines Ltd. (Wan Hai) |
| **SCAC Code** | WHLC |
| **Parent Company** | Independent |
| **Alliance** | Independent (no alliance membership) |
| **Primary Services** | Container shipping (FCL/LCL) |
| **Market Position** | 11th largest global container line; leading intra-Asia carrier by market share. ~123 vessels, ~530,000 TEU capacity. Expanding into long-haul trades (Americas, Middle East). |
| **Headquarters** | Taipei, Taiwan |
| **Website** | https://www.wanhai.com/ |

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | No |
| **Developer portal URL** | N/A |
| **API documentation URL(s)** | N/A |
| **Documentation quality** | None -- no API documentation exists |
| **OpenAPI/Swagger spec available?** | No |
| **Sandbox/test environment?** | No |
| **Developer registration** | N/A |
| **Developer support channels** | General customer service only; no developer-specific channels |
| **Community/third-party libraries** | None found |
| **API changelog / release notes** | Not published |

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | No (confirmed; DCSA has 10 members and Wan Hai is not among them) |
| **DCSA APIs implemented** | None |
| **DCSA TNT version** | N/A |
| **DCSA Booking version** | N/A |
| **DCSA Schedules version** | N/A |
| **Known DCSA deviations** | N/A |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Yes | EDI services available; XML format supported by mutual agreement. Details require contacting Wan Hai. |
| **INTTRA integration** | Yes | Joined INTTRA (now E2open) in October 2018. Full suite: booking, SI, eVGM, T&T, B/L, schedules. |
| **BIC (Bureau International des Containers)** | Yes | Container prefixes: WHLU (primary), WHLC (legacy SCAC), 22AA (US customs) |
| **UN/LOCODE** | Unknown | Likely used in EDI/INTTRA messages, but not confirmed directly |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | N/A (no public API) |
| **Auth documentation** | N/A |
| **Registration process** | N/A for API. Shipper portal requires customer account. INTTRA requires platform onboarding. |
| **Registration URL** | Shipper portal: https://shipper.wanhai.com/ |
| **Partner program required?** | Yes -- for any programmatic access (INTTRA or EDI both require business relationship) |
| **Partner program URL** | N/A |
| **Credential type** | N/A |
| **Token refresh supported?** | N/A |
| **Token lifetime** | N/A |
| **Access tiers** | N/A |
| **IP whitelisting required?** | Unknown |

### Access Requirements Summary for SSL

Wan Hai does not offer a public REST API. Programmatic access to Wan Hai data requires one of the following approaches:

1. **INTTRA/E2open platform**: The most comprehensive option. Wan Hai joined INTTRA in October 2018 and supports booking, shipping instructions, eVGM, Track & Trace, Bill of Lading, and Ocean Schedules through the INTTRA platform. SSL would need an INTTRA/E2open subscription and onboarding.

2. **Third-party visibility aggregators**: project44 and Vizion both provide Wan Hai tracking data via their APIs. This requires a commercial relationship with the aggregator.

3. **Direct EDI**: Wan Hai supports EDI messaging (with XML format by agreement). This requires a bilateral EDI agreement with Wan Hai.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field must have a row.
> Legend: ✅ = Available | ❌ = Not available | ⚠️ = Partial / limited | ❓ = Unknown

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ⚠️ | N/A (no API) | N/A | N/A | Available via INTTRA Ocean Schedules, shipper portal, and web portal schedule search. Not available via direct API. |
| 1.2 | Point-to-Point Route Options | ⚠️ | N/A (no API) | N/A | N/A | Shipper portal supports origin/destination schedule search. Available via INTTRA. Not available via direct API. |
| 1.3 | Booking Lifecycle | ⚠️ | N/A (no API) | N/A | N/A | Available via INTTRA (booking) and shipper portal. Not available via direct API. |
| 1.4 | Shipping Instructions | ⚠️ | N/A (no API) | N/A | N/A | Available via INTTRA (shipping instructions). Not available via direct API. |
| 1.5 | Rates | ❌ | N/A | N/A | N/A | No rate API or known rate access through any programmatic channel. |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❓ | N/A (no API) | N/A | `ECP` | May be available through INTTRA booking confirmation or shipper portal. Unconfirmed. |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❓ | N/A (no API) | N/A | `EFC` | May be available through INTTRA booking confirmation. Unconfirmed. |
| 2.3 | Documentation Cutoff | DCO | ⚠️ | N/A (no API) | N/A | `DCO` | Likely available in INTTRA booking confirmation and shipper portal. Standard field for ocean bookings. |
| 2.4 | VGM Cutoff | VCO | ⚠️ | N/A (no API) | N/A | `VCO` | Wan Hai supports eVGM via INTTRA, so VGM cutoff is likely available. |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ⚠️ | N/A (no API) | N/A | `FCO` | Likely available via INTTRA and shipper portal. Standard field for ocean bookings. |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❓ | N/A (no API) | N/A | `LCO` | Unknown. May be available through INTTRA for LCL shipments. |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ❓ | N/A (no API) | N/A | Inferred from first EquipmentEvent | Unknown whether INTTRA or portal exposes this. |
| 3.2 | Empty Container Gate-Out (Pickup) | ⚠️ | N/A (no API) | N/A | `GTOT` + `EMPTY` | Likely available via INTTRA T&T and web portal tracking. Third-party aggregators (project44, Vizion) provide this. |
| 3.3 | Full Container Gate-In | ⚠️ | N/A (no API) | N/A | `GTIN` + `LADEN` | Likely available via INTTRA T&T and web portal tracking. Third-party aggregators provide this. |
| 3.4 | Container Loaded on Vessel | ⚠️ | N/A (no API) | N/A | `LOAD` + `LADEN` | Likely available via INTTRA T&T and web portal tracking. Third-party aggregators provide this. |
| 3.5 | Container Discharged at Transshipment | ⚠️ | N/A (no API) | N/A | `DISC` + `LADEN` + transshipment | Likely available via INTTRA T&T. May appear on portal. Third-party aggregators provide this. |
| 3.6 | Container Loaded at Transshipment | ⚠️ | N/A (no API) | N/A | `LOAD` + `LADEN` + transshipment | Likely available via INTTRA T&T. May appear on portal. Third-party aggregators provide this. |
| 3.7 | Container Discharged at Destination | ⚠️ | N/A (no API) | N/A | `DISC` + `LADEN` | Likely available via INTTRA T&T and web portal tracking. Third-party aggregators provide this. |
| 3.8 | Full Container Gate-Out (Delivery) | ⚠️ | N/A (no API) | N/A | `GTOT` + `LADEN` | Likely available via INTTRA T&T and web portal tracking. Third-party aggregators provide this. |
| 3.9 | Empty Container Returned | ⚠️ | N/A (no API) | N/A | `GTIN` + `EMPTY` | Likely available via INTTRA T&T and web portal tracking. Third-party aggregators may provide this. |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ⚠️ | N/A (no API) | N/A | `DEPA` + classifier | Available on web portal, INTTRA schedules, and through aggregators. No direct API. |
| 4.2 | Estimated Time of Arrival | ETA | ⚠️ | N/A (no API) | N/A | `ARRI` + classifier | Available on web portal, INTTRA schedules, and through aggregators. No direct API. |
| 4.3 | Vessel Arrival at Transshipment | -- | ⚠️ | N/A (no API) | N/A | `ARRI` at intermediate | Likely available via INTTRA T&T and aggregators. |
| 4.4 | Vessel Departure from Transshipment | -- | ⚠️ | N/A (no API) | N/A | `DEPA` at intermediate | Likely available via INTTRA T&T and aggregators. |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❌ | No direct API; no webhook support from Wan Hai. Aggregators (project44, Vizion) may offer webhooks for Wan Hai data. |
| Event Polling with timestamp filter | ❌ | No direct API. Aggregator APIs support polling. |
| Event Classifier Progression (PLN->EST->ACT) | ❌ | No DCSA compliance; no direct event classifier support. INTTRA may provide event progression. |
| Retracted Events | ❌ | No evidence of retracted event support. |
| Change Remarks | ❌ | No evidence of change remark support. |
| Delay Reason Codes | ❌ | No evidence of delay reason code support. |

### Coverage Summary

| Category | Fields Available | Fields Unavailable | Fields Unknown | Coverage % |
|----------|-----------------|-------------------|----------------|-----------|
| API Domains (1.x) | 0/5 | 1/5 | 0/5 | 0% (4 partial via INTTRA/portal) |
| Cutoffs (2.x) | 0/6 | 0/6 | 3/6 | 0% (3 partial via INTTRA/portal, 3 unknown) |
| Container Milestones (3.x) | 0/9 | 0/9 | 1/9 | 0% (8 partial via INTTRA/aggregators, 1 unknown) |
| Transport Events (4.x) | 0/4 | 0/4 | 0/4 | 0% (4 partial via INTTRA/aggregators) |
| Change Detection (5.x) | 0/6 | 6/6 | 0/6 | 0% |
| **Total** | **0/30** | **7/30** | **4/30** | **0% via API (63% partial via INTTRA/aggregators, 13% unknown)** |

> **Important note on coverage**: The 0% direct API coverage reflects that Wan Hai has no public REST API. Through INTTRA/E2open and third-party aggregators (project44, Vizion), 19 of 30 fields are accessible in some form -- marked with ⚠️ above. The "Available?" column reflects direct API availability only, consistent with the methodology used for other carriers in this inventory series.

---

## Endpoint Reference

Wan Hai does not expose any public REST API endpoints. This section is intentionally left minimal.

### Tracking / Events

| Endpoint | Method | Lookup Params | Pagination | Response Format | Notes |
|----------|--------|--------------|------------|----------------|-------|
| N/A | N/A | N/A | N/A | N/A | No direct API. Tracking available via web portal, INTTRA, or aggregators. |

### Schedules

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| N/A | N/A | N/A | N/A | N/A | No direct API. Schedules available via web portal, INTTRA, or aggregators. |

### Booking

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| N/A | N/A | N/A | N/A | N/A | No direct API. Booking available via INTTRA and shipper portal. |

### Lookup Methods Summary

| Identifier Type | Supported? | Which Endpoints? | Notes |
|----------------|-----------|-----------------|-------|
| **Bill of Lading (B/L) number** | ⚠️ | Web portal, INTTRA | Public portal tracking supports B/L lookup |
| **Booking reference** | ⚠️ | Web portal, INTTRA | Public portal tracking supports booking lookup |
| **Container number** | ⚠️ | Web portal, INTTRA, aggregators | Public portal and all aggregators support container lookup |
| **Carrier booking number** | ⚠️ | Web portal, INTTRA | Same as booking reference for Wan Hai |
| **Vessel IMO / voyage** | ⚠️ | Web portal schedule search | Schedule search by vessel available on portal |

---

## Rate Limits & Quotas

| Detail | Value | Source |
|--------|-------|--------|
| **Global rate limit** | N/A (no API) | N/A |
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
| **Webhooks supported?** | No (no direct API) |
| **Subscription endpoint** | N/A |
| **Subscription management** | N/A |
| **Subscribable event types** | N/A |
| **Callback format** | N/A |
| **Callback authentication** | N/A |
| **Retry policy on failure** | N/A |
| **Documented reliability** | N/A |

> **Note**: While Wan Hai itself does not offer webhooks, aggregator platforms (project44, Vizion) may offer webhook/push notifications for Wan Hai shipment events through their own APIs.

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | https://www.wanhai.com/views/cargoTrack/CargoTrack.xhtml (public) and https://shipper.wanhai.com/ (registered users) |
| **Login required?** | No for basic tracking; Yes for shipper portal (booking, full features) |
| **Data available on portal but NOT in API** | All data is portal-only since there is no API. Portal shows: container milestones, vessel info, ETD/ETA, port calls. Shipper portal adds: booking management, shipping instructions, schedule search. |
| **Scraping feasibility** | Difficult -- site uses Incapsula (Imperva) WAF with bot detection. ToS likely prohibits scraping. |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Yes |
| **EDI message types** | Specific types not publicly documented. Via INTTRA: booking, shipping instructions, eVGM, T&T, B/L, schedules. XML format available by bilateral agreement. |
| **EDI connection method** | Contact Wan Hai directly. INTTRA provides standardized EDI connectivity. |
| **EDI documentation** | https://www.wanhai.com/views/service/edi.xhtml (requires accessing from browser; blocked by WAF for automated tools) |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Yes | Dedicated Wan Hai tracking page at project44.com. Container tracking confirmed. |
| **FourKites** | Unknown | No specific confirmation found. Likely available given Wan Hai's global presence. |
| **Vizion** | Yes | Wan Hai supported in Vizion API. Changelog references connection maintenance for Wan Hai. |
| **INTTRA / E2open** | Yes | Wan Hai joined INTTRA in October 2018. Full suite: booking, shipping instructions, eVGM, Track & Trace, Bill of Lading, Ocean Schedules. Most comprehensive programmatic access channel. |
| **CargoSmart** | Unknown | No specific confirmation found. |
| **Other**: Terminal49 | Yes | Supports WHLC container tracking. |
| **Other**: Portcast | Yes | Provides Wan Hai tracking and predictive visibility. |
| **Other**: Dockflow | Yes | Offers Wan Hai tracking with API integration. |

> **Aggregator note**: Since Wan Hai has no direct API, aggregator access is the only practical programmatic integration path. INTTRA/E2open provides the broadest coverage (booking + tracking + documents + schedules). For tracking-only needs, project44 or Vizion are viable alternatives that may be simpler to integrate.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown (no direct API). Aggregator freshness depends on the platform. | Unknown |
| **API uptime/reliability** | N/A (no API) | N/A |
| **Historical data depth** | Unknown. Web portal likely shows current shipment data only. | Unknown |
| **Timezone handling** | Unknown | Unknown |
| **Character encoding** | Unknown | Unknown |

### Known Issues & Gotchas

- **No direct API**: All programmatic access must go through INTTRA/E2open or third-party aggregators, adding a dependency and potential latency.
- **Incapsula WAF**: The wanhai.com website is protected by Imperva Incapsula, making web scraping unreliable and likely ToS-violating.
- **Multiple SCAC/prefix codes**: Wan Hai uses WHLU (primary container prefix), WHLC (SCAC code), and 22AA (US customs filings). Ensure correct code usage for each context.
- **INTTRA data format**: INTTRA uses its own standardized message format, not DCSA. Mapping from INTTRA events to the SSL canonical model will require custom logic.
- **Regional focus**: Wan Hai's strongest coverage is intra-Asia. Event granularity may vary for their newer long-haul services.

### Recently Deprecated or Changed

- No deprecations found (no API to deprecate).

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | Partial -- only through aggregator APIs (INTTRA/E2open, project44, or Vizion) |
| **Implementation effort** | High (no direct API; requires aggregator integration) |
| **DCSA base adapter usable?** | No -- Wan Hai is not DCSA-compliant; fully custom mapping required regardless of access method |

### Recommended Approach

The recommended approach for Wan Hai integration is a **multi-tier aggregator strategy**:

1. **Primary path: INTTRA/E2open** -- provides the broadest data coverage (booking, tracking, documents, schedules). If SSL already has or plans an INTTRA integration for other carriers (e.g., OOCL also uses INTTRA/CargoSmart), this is the most efficient path as it covers multiple carriers with one integration.

2. **Alternative path: Visibility aggregator (project44 or Vizion)** -- if SSL only needs tracking/visibility (not booking or documentation), integrating through project44 or Vizion provides a simpler API with standardized event formats. Both confirmed Wan Hai support. This path is especially attractive if SSL already uses these platforms for other carriers.

3. **Fallback: Web scraping** -- not recommended due to Incapsula WAF protection and likely ToS violations. Only consider as a last resort for specific data points not available through aggregators.

The adapter should be built as a thin wrapper around whichever aggregator API is chosen, mapping the aggregator's event format to the SSL canonical data model. No direct Wan Hai API adapter is possible.

### Recommended Lookup Method

**Container number** is the most universally supported lookup method across all access channels (web portal, INTTRA, project44, Vizion). B/L number is also widely supported. Booking reference support varies by platform.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Depends on aggregator. For project44/Vizion: every 2-4 hours (per aggregator rate limits). For INTTRA: event-driven or per INTTRA polling guidelines. |
| **Incremental filter** | Aggregator-dependent. project44 and Vizion support timestamp-based incremental polling. INTTRA may support event-based incremental retrieval. |
| **Batch tracking** | Aggregator-dependent. project44 and Vizion typically support batch tracking. INTTRA supports multiple shipment queries. |

### Auth Implementation Notes

Authentication depends entirely on the chosen aggregator:
- **INTTRA/E2open**: Requires INTTRA platform credentials and onboarding. Typically uses INTTRA-specific authentication.
- **project44**: OAuth2 or API key authentication per project44's API documentation.
- **Vizion**: API key authentication per Vizion's API documentation.

No Wan Hai-specific authentication logic is needed since there is no direct API.

### Edge Cases to Handle

- **Multiple container prefix codes**: Map WHLU, WHLC, and 22AA correctly depending on context (container tracking vs. SCAC lookup vs. US customs).
- **INTTRA event format**: INTTRA events use a proprietary format that requires custom mapping to SSL canonical events. The mapping is not 1:1 with DCSA.
- **Transshipment visibility**: Wan Hai operates heavily in intra-Asia with frequent transshipments. Ensure the adapter handles multi-leg journeys with intermediate port events.
- **Data freshness lag**: Aggregator-mediated data may have additional latency compared to direct API access. The lag varies by aggregator and should be measured during testing.

### Mapping Complexity

Mapping complexity is **high** regardless of access method. Since Wan Hai has no DCSA-compliant API, there is no standard event format to map from. The mapping depends on the chosen aggregator:

- **INTTRA**: Uses INTTRA's own standardized event codes and message formats. Requires building a complete INTTRA-to-SSL mapping layer.
- **project44/Vizion**: These platforms provide their own normalized event formats, which are generally easier to map than raw carrier data but still require per-platform mapping logic.

The lack of DCSA compliance means the DCSA base adapter cannot be reused; a fully custom adapter is required.

---

## Open Questions

- [ ] Does SSL have an existing INTTRA/E2open subscription that could be leveraged for Wan Hai access?
- [ ] Does SSL have existing relationships with project44 or Vizion that would simplify Wan Hai integration?
- [ ] What specific EDI message types does Wan Hai support beyond what INTTRA provides?
- [ ] Is FourKites coverage confirmed for Wan Hai? (Likely yes, but unverified.)
- [ ] Does CargoSmart support Wan Hai tracking? (No evidence found, but possible given CargoSmart's broad carrier coverage.)
- [ ] What is the event freshness/latency when accessing Wan Hai data through aggregators?
- [ ] Does the shipper portal expose any data (e.g., detailed cutoff times) not available through INTTRA?

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | https://www.wanhai.com/ |
| Shipper Portal | https://shipper.wanhai.com/ |
| Public Cargo Tracking | https://www.wanhai.com/views/cargoTrack/CargoTrack.xhtml |
| EDI Services Page | https://www.wanhai.com/views/service/edi.xhtml |
| DCSA Members Page | https://dcsa.org/about-us-our-work-and-what-we-do-dcsa/members/ |
| INTTRA/Wan Hai Announcement | https://www.inttra.com/newsroom/wan-hai-lines-joins-inttras-network/ |
| project44 Wan Hai Tracking | https://www.project44.com/container-tracking/wan-hai |
| Vizion API | https://docs.vizionapi.com/changelog |
| Terminal49 WHLC | https://terminal49.com/shipping-lines/whlc-wan-hai-lines-container-tracking |
| Wan Hai Wikipedia | https://en.wikipedia.org/wiki/Wan_Hai_Lines |
| Schedule Search (Fluent Cargo) | https://www.fluentcargo.com/carriers/scac/22AA |
