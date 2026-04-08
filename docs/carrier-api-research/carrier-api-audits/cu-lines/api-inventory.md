# CU Lines (China United Lines) -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing
> **Researched by**: Agent
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | China United Lines Co., Ltd (commonly "CU Lines" or "CULines") |
| **SCAC Code** | CULU |
| **Parent Company** | Independent (privately held) |
| **Alliance** | None / Independent |
| **Primary Services** | International container shipping, domestic coastal/Yangtze River trade, Taiwan cross-strait container liner trade, charter business |
| **Market Position** | Regional specialist -- top 30 global container carrier by capacity (~110,000 TEU across 34 vessels). Strong presence on Asia intra-regional, Middle East, Red Sea, East Mediterranean, and East Africa routes |
| **Headquarters** | Shanghai, China (global HQ); Singapore (operational hub) |
| **Website** | https://www.culines.com |

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | No |
| **Developer portal URL** | N/A |
| **API documentation URL(s)** | N/A -- no public API documentation found |
| **Documentation quality** | None |
| **OpenAPI/Swagger spec available?** | No |
| **Sandbox/test environment?** | No / Unknown |
| **Developer registration** | N/A |
| **Developer support channels** | General contact only: Singapore (+65-6681-5696), Shanghai (+86-21-6595-6526), service@culines.com |
| **Community/third-party libraries** | None found. Third-party tracking aggregators (Terminal49, Shipsgo, TimeToCargo) provide tracking data for CU Lines through scraping/data partnerships |
| **API changelog / release notes** | N/A |

### Digital Services Available (Non-API)

CU Lines offers a web-based **eService platform** at https://eservice.culines.com/ with the following capabilities:

- Cargo tracking (by B/L number or container number)
- Port schedule
- Vessel schedule
- Point-to-point schedule
- Long-range schedule
- eBooking
- Tariff rate item search

CU Lines also operates a **US Community Portal** at https://culines.us/ for container tracking, demurrage fee payments, and pickup appointment scheduling.

Mobile apps are available on the Apple App Store, Google Play, and as direct APK download.

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
| **Known DCSA deviations** | N/A -- CU Lines does not implement any DCSA APIs |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Unknown | No explicit EDI documentation found. Given the carrier's size and regional focus, EDI may be available for select trade lanes but is not publicly documented |
| **INTTRA integration** | Unknown | Not confirmed. INTTRA covers 60+ carriers but explicit CU Lines partnership not found |
| **BIC (Bureau International des Containers)** | Yes | Standard container ID format (CULU prefix) used in tracking. B/L format documented as 14 alphanumeric characters (e.g., CULSHA200010001) |
| **UN/LOCODE** | Unknown | Port codes visible on web portal but underlying code standard not confirmed |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | N/A -- no public API exists |
| **Auth documentation** | N/A |
| **Registration process** | N/A -- eService platform has web-based login for booking customers |
| **Registration URL** | N/A |
| **Partner program required?** | N/A |
| **Partner program URL** | N/A |
| **Credential type** | N/A |
| **Token refresh supported?** | N/A |
| **Token lifetime** | N/A |
| **Access tiers** | N/A |
| **IP whitelisting required?** | N/A |

### Access Requirements Summary for SSL

CU Lines does not offer a public developer API or developer portal. There is no documented programmatic access mechanism for tracking, schedules, or booking data. The only digital touchpoints are:

1. **eService web platform** (https://eservice.culines.com/) -- web-based cargo tracking and schedule lookup, requires account for booking
2. **Main website tracking** (https://www.culines.com/en/site/bill) -- public tracking by B/L or container number without login
3. **US Community Portal** (https://culines.us/) -- tracking, demurrage payments, pickup scheduling

SSL would need to either: (a) negotiate a direct data partnership with CU Lines for API/EDI access (contact CU Lines commercial team), (b) use a third-party aggregator like Terminal49 that already supports CULU tracking, or (c) implement web scraping of the public tracking portal (subject to ToS review).

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field has a row.
> Availability legend: check = Available | x = Not available | warning = Partial / limited | question = Unknown

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ⚠️ | eService web portal only | Port schedule, vessel schedule pages | N/A | Available via web portal (eservice.culines.com) but no API. Includes port schedules, vessel schedules, long-range schedules |
| 1.2 | Point-to-Point Route Options | ⚠️ | eService web portal only | Point-to-point schedule page | N/A | Available via web portal but no API. Supports origin-destination route lookup |
| 1.3 | Booking Lifecycle | ⚠️ | eService web portal only (eBooking) | eBooking feature | N/A | eBooking available through web portal. No API for booking creation or management |
| 1.4 | Shipping Instructions | ❌ | N/A | N/A | N/A | No SI submission capability found via API or documented EDI |
| 1.5 | Rates | ⚠️ | eService web portal only | Tariff rate item search | N/A | Tariff lookup available on web portal. No rate API |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❓ | Unknown | Unknown | `ECP` | Not visible in publicly accessible tracking data. May be available to booking customers via eService |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❓ | Unknown | Unknown | `EFC` | Not visible in publicly accessible tracking data |
| 2.3 | Documentation Cutoff | DCO | ❓ | Unknown | Unknown | `DCO` | May be included in booking confirmations via eService but not confirmed |
| 2.4 | VGM Cutoff | VCO | ❓ | Unknown | Unknown | `VCO` | May be included in booking confirmations but not confirmed |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ❓ | Unknown | Unknown | `FCO` | May be included in schedule or booking data but not confirmed |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❓ | Unknown | Unknown | `LCO` | Not confirmed |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ❓ | Web tracking portal | Unknown | Inferred from first EquipmentEvent | Not confirmed in public tracking view |
| 3.2 | Empty Container Gate-Out (Pickup) | ⚠️ | Web tracking portal | Status update with location and timestamp | `GTOT` + `EMPTY` | Web tracking shows sequential status updates. Gate-out events likely included but specific event codes unknown |
| 3.3 | Full Container Gate-In | ⚠️ | Web tracking portal | Status update with location and timestamp | `GTIN` + `LADEN` | Same as 3.2 -- status updates visible on portal |
| 3.4 | Container Loaded on Vessel | ⚠️ | Web tracking portal | Loaded status with vessel/voyage info | `LOAD` + `LADEN` | Terminal49 confirms "vessel loading" milestone is available for CULU. Web portal shows loading event |
| 3.5 | Container Discharged at Transshipment | ⚠️ | Web tracking portal | Discharge event at intermediate port | `DISC` + `LADEN` + transshipment | Terminal49 confirms transshipment activities are trackable. Web portal shows port-level events |
| 3.6 | Container Loaded at Transshipment | ⚠️ | Web tracking portal | Loading event at transshipment port | `LOAD` + `LADEN` + transshipment | Same as 3.5 |
| 3.7 | Container Discharged at Destination | ⚠️ | Web tracking portal | Discharge event at destination | `DISC` + `LADEN` | Web portal shows discharge at destination. Terminal49 confirms this milestone |
| 3.8 | Full Container Gate-Out (Delivery) | ❓ | Web tracking portal | Unknown | `GTOT` + `LADEN` | Terminal49 lists "destination arrival" and "delivery" as in development for CULU |
| 3.9 | Empty Container Returned | ❓ | Web tracking portal | Unknown | `GTIN` + `EMPTY` | Not confirmed in publicly available data |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ⚠️ | Web tracking portal; schedule pages | ETD in schedule and tracking | `DEPA` + classifier | Schedule pages show ETD. Tracking shows estimated vs actual (gray = estimated, colored = actual). No API access |
| 4.2 | Estimated Time of Arrival | ETA | ⚠️ | Web tracking portal; schedule pages | ETA in schedule and tracking | `ARRI` + classifier | Same as 4.1 for arrival times |
| 4.3 | Vessel Arrival at Transshipment | -- | ⚠️ | Web tracking portal | Vessel arrival at intermediate ports | `ARRI` at intermediate | Tracking shows port-level events including transshipment ports |
| 4.4 | Vessel Departure from Transshipment | -- | ⚠️ | Web tracking portal | Vessel departure from intermediate ports | `DEPA` at intermediate | Same as 4.3 for departures |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❌ | No webhook or push notification system available |
| Event Polling with timestamp filter | ❌ | No API available for polling |
| Event Classifier Progression (PLN->EST->ACT) | ⚠️ | Web portal distinguishes estimated (gray) vs actual schedules, but no programmatic access |
| Retracted Events | ❌ | No retraction mechanism found |
| Change Remarks | ❌ | No change remarks found |
| Delay Reason Codes | ❌ | No delay reason codes found |

### Coverage Summary

| Category | Fields Available | Fields Partial | Fields Unavailable | Fields Unknown | Coverage % |
|----------|-----------------|---------------|-------------------|----------------|-----------|
| API Domains (1.x) | 0/5 | 4/5 | 1/5 | 0/5 | 0% confirmed (4 portal-only) |
| Cutoffs (2.x) | 0/6 | 0/6 | 0/6 | 6/6 | 0% (all unknown) |
| Container Milestones (3.x) | 0/9 | 6/9 | 0/9 | 3/9 | 0% confirmed (6 partial via portal) |
| Transport Events (4.x) | 0/4 | 4/4 | 0/4 | 0/4 | 0% confirmed (4 partial via portal) |
| Change Detection (5.x) | 0/6 | 1/6 | 5/6 | 0/6 | 0% (1 partial) |
| **Total** | **0/30** | **15/30** | **6/30** | **9/30** | **0% via API (50% portal-only/partial, 30% unknown)** |

> **Notes on Coverage:**
> - CU Lines has **no public API** whatsoever. All "partial" coverage reflects data visible on the web portal or confirmed via third-party aggregators (Terminal49), not programmatic access.
> - The web portal tracking (culines.com/en/site/bill) provides B/L and container tracking with vessel, voyage, port, and milestone data -- but only through a browser interface.
> - Terminal49 has confirmed it can retrieve tracking data for CULU including vessel loading, discharge, and transshipment milestones, suggesting the underlying data exists even without a direct API.
> - Cutoffs are entirely unknown from desk research -- they may be available to booking customers within the eService platform.
> - Change detection is effectively non-existent without an API to poll.
> - The practical path to programmatic CU Lines data is through a third-party aggregator (Terminal49, Shipsgo) rather than direct integration.

---

## Endpoint Reference

CU Lines does not expose any public API endpoints. This section is intentionally omitted.

### Lookup Methods Summary

| Identifier Type | Supported? | Which Endpoints? | Notes |
|----------------|-----------|-----------------|-------|
| **Bill of Lading (B/L) number** | ⚠️ (portal only) | Web tracking portal | 14-character alphanumeric format (e.g., CULSHA200010001). House B/Ls not accepted |
| **Booking reference** | ⚠️ (portal only) | eService portal | Available to booking customers within eService |
| **Container number** | ⚠️ (portal only) | Web tracking portal | 11-character standard format. Terminal49 notes container lookup currently unsupported via their API for CULU |
| **Carrier booking number** | ❓ | Unknown | May be same as booking reference |
| **Vessel IMO / voyage** | ⚠️ (portal only) | Vessel schedule page | Vessel schedule lookup available on web portal |

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

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | https://www.culines.com/en/site/bill (main site); https://eservice.culines.com/gnoss/CUP_HOM_3301.do?sessLocale=en (eService) |
| **Login required?** | No -- basic tracking by B/L or container number available without login. eBooking and advanced features require login |
| **Data available on portal but NOT in API** | All data is portal-only since there is no API. Portal provides: booking details (booking no., container no., seal no., type/size, weight, PO no.), sailing info (vessel, voyage, POL, POD, ETD, ETA), cargo tracking events (sequential status updates with location, date, estimated vs actual) |
| **Scraping feasibility** | Feasible -- portal is standard web-based. No obvious anti-bot measures detected in initial review. ToS review required before implementation |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Unknown |
| **EDI message types** | Unknown |
| **EDI connection method** | Unknown |
| **EDI documentation** | None found -- contact carrier directly |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Unknown | Not explicitly confirmed for CULU. project44 covers many carriers but explicit CU Lines listing not found |
| **FourKites** | Unknown | Not explicitly confirmed. FourKites covers 85+ ocean carriers but CU Lines status unconfirmed |
| **Vizion** | No | CU Lines / CULU is **not** on Vizion's supported carriers list as of latest check |
| **INTTRA / E2open** | Unknown | Not explicitly confirmed. INTTRA covers 60+ carriers but CU Lines partnership not documented |
| **CargoSmart** | Unknown | Not confirmed |
| **Terminal49** | Yes | Confirmed: Terminal49 supports CULU tracking by B/L and booking number. Container number lookup listed as unsupported. Provides vessel loading, discharge, transshipment milestones. Destination arrival and delivery listed as "in development" |
| **Shipsgo** | Yes | Confirmed: Shipsgo provides CU Lines container tracking |
| **SeaRates** | Yes | Confirmed: SeaRates provides CU Lines tracking |
| **GoComet** | Yes | Confirmed: GoComet provides CU Lines vessel tracking and sailing schedules |

> **Aggregator note:** Given CU Lines has no direct API, third-party aggregators are the only viable path for programmatic data access. Terminal49 is the most promising option as it confirms support for CULU with specific milestone coverage details. The aggregator likely scrapes or has a data partnership with CU Lines. For SSL's SDK, integrating via Terminal49 or a similar aggregator would be the recommended approach rather than attempting direct integration with a carrier that has no API.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown -- no API to measure. Web portal updates are not real-time based on typical portal behavior | Unknown |
| **API uptime/reliability** | N/A -- no API | N/A |
| **Historical data depth** | Unknown | Unknown |
| **Timezone handling** | Unknown -- web portal displays dates but timezone convention not confirmed. Likely China Standard Time (UTC+8) given Shanghai HQ | Estimated |
| **Character encoding** | Unknown -- portal content is bilingual (English/Chinese). UTF-8 assumed | Estimated |

### Known Issues & Gotchas

- **No API whatsoever**: CU Lines is one of the carriers that has not invested in developer-facing API infrastructure. All digital services are web-portal-only. This is a significant barrier to programmatic integration.

- **Regional carrier with growing ambitions**: CU Lines has been expanding rapidly (new services to Middle East, East Africa, Mediterranean) and launched eBooking in 2025. An API may eventually follow, but none exists today.

- **B/L format specificity**: The tracking portal enforces a strict 14-character alphanumeric B/L format and explicitly rejects House B/Ls from NVOCCs. SSL must use the Master B/L for tracking.

- **Container number lookup limitations**: Even Terminal49 notes that container number lookup is "currently unsupported" for CULU, suggesting the underlying data source primarily supports B/L-based tracking.

- **eService platform is login-gated for advanced features**: While basic tracking is public, booking, detailed schedule, and tariff features require an eService account.

- **No English API documentation**: Even Chinese API documentation has not been found, suggesting the carrier simply does not have an API program.

### Recently Deprecated or Changed

- No API has existed to deprecate. CU Lines launched its eBooking platform in early 2025, indicating ongoing digital development.

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | Partial -- only via third-party aggregator (Terminal49) or web scraping. No direct API integration possible |
| **Implementation effort** | Very High (no API) -- requires either aggregator integration or custom web scraping solution |
| **DCSA base adapter usable?** | No -- CU Lines is not a DCSA member, has no API, and exposes no DCSA-compatible data structures |

### Recommended Approach

CU Lines cannot be integrated directly due to the absence of any public API. There are two viable approaches:

1. **Aggregator integration (recommended)**: Use Terminal49's API as the data source for CU Lines tracking. Terminal49 has confirmed support for CULU with B/L and booking number lookups, covering vessel loading, discharge, and transshipment milestones. This approach avoids the legal and maintenance risks of web scraping. The SSL adapter would communicate with Terminal49's normalized API rather than CU Lines directly, and Terminal49's data model would need to be mapped to SSL's canonical DCSA-based model.

2. **Web scraping (fallback)**: If aggregator costs are prohibitive or coverage insufficient, the CU Lines public tracking portal (culines.com/en/site/bill) could be scraped for B/L and container tracking data. This is legally risky (ToS review required), fragile (any portal UI changes break the scraper), and limited in data depth. Not recommended as a primary strategy.

For schedule data, the eService platform offers port, vessel, and point-to-point schedules via the web portal. These could be accessed via aggregator or scraping, but are lower priority than tracking.

### Recommended Lookup Method

**Bill of Lading (B/L) number** is the only reliable lookup method, supported both by the web portal and by Terminal49. The 14-character format (e.g., CULSHA200010001) must be validated before submission.

**Booking reference** as secondary -- supported via eService and Terminal49.

Container number lookup is currently unreliable even through aggregators.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Every 4-6 hours via aggregator (Terminal49). Subject to aggregator's own rate limits and data freshness |
| **Incremental filter** | Depends on aggregator capabilities. Terminal49 supports event-based updates. Full re-fetch may be required if using scraping |
| **Batch tracking** | Depends on aggregator. Terminal49 supports tracking multiple shipments. One-at-a-time if scraping |

### Auth Implementation Notes

No direct auth implementation needed since CU Lines has no API. If using Terminal49 as aggregator:
- Terminal49 uses API Key authentication
- Register at terminal49.com for credentials
- Standard REST API with JSON responses

If web scraping is chosen (not recommended):
- No authentication needed for basic tracking on culines.com
- eService features require session-based login
- Anti-bot mitigation may be needed

### Edge Cases to Handle

- **House B/L rejection**: CU Lines tracking explicitly rejects House B/Ls. The adapter must validate that only Master B/Ls are submitted, or handle the rejection gracefully.

- **Container number unsupported**: Container-based lookups may fail even through aggregators. Fall back to B/L lookup.

- **Limited milestone coverage**: Terminal49 lists destination arrival and delivery tracking as "in development" for CULU. These milestones may not be available initially.

- **Aggregator data lag**: Data from CU Lines reaches aggregators through scraping or partnerships, introducing potential delays beyond what a direct API would have.

- **Regional service focus**: CU Lines primarily serves Asia intra-regional, Middle East, and East Africa routes. Tracking data quality may vary by trade lane.

### Mapping Complexity

**Medium complexity (via aggregator) / Very High (via scraping).** Using Terminal49, the mapping is from Terminal49's normalized data model to SSL's canonical model -- Terminal49 already handles the CU Lines-specific parsing. Via scraping, the raw HTML would need to be parsed, status descriptions interpreted, and events mapped to DCSA milestones -- all without documentation of CU Lines' event taxonomy.

---

## Open Questions

- [ ] Does CU Lines have any undocumented API or EDI capability available to business partners? -- Contact CU Lines commercial team
- [ ] Does SSL have an existing business relationship with CU Lines? -- Would enable direct inquiry about data access
- [ ] What is Terminal49's coverage depth for CULU? -- Need to verify specific milestones and cutoff availability via Terminal49
- [ ] Is CU Lines available via project44 or FourKites? -- Would provide alternative aggregator options
- [ ] Does CU Lines provide cutoff data to any aggregator? -- Critical for full shipment lifecycle tracking
- [ ] Is CU Lines planning to develop a public API? -- The 2025 eBooking launch suggests increasing digital investment
- [ ] What are CU Lines' EDI capabilities, if any? -- May be available for high-volume customers
- [ ] Are there any INTTRA/E2open partnerships for CU Lines? -- Would provide structured data access for booking/SI

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | https://www.culines.com/en/ |
| Company Profile | https://www.culines.com/en/site/about |
| Cargo Tracking (Main Site) | https://www.culines.com/en/site/bill |
| Vessel Schedule | https://www.culines.com/en/site/ship_tracking |
| eService Platform | https://eservice.culines.com/ |
| eService Tracking (English) | https://eservice.culines.com/gnoss/CUP_HOM_3301.do?sessLocale=en |
| US Community Portal | https://culines.us/ |
| Detention & Demurrage Tariffs | https://www.culines.com/en/site/rule |
| Terminal49 CULU Page | https://terminal49.com/shipping-lines/culu-china-united-lines-container-tracking |
| Shipsgo CU Lines Tracking | https://shipsgo.com/ocean/carriers/culines/container-tracking |
| SeaRates CU Lines | https://www.searates.com/sealine/cu_lines |
| GoComet Vessel Tracking | https://www.gocomet.com/vessel-tracking/culu |
| Beacon SCAC Codes List | https://www.beacon.com/resources/ocean-carrier-scac-codes-list |
