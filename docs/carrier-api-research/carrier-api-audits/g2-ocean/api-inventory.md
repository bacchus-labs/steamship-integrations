# G2 Ocean -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing. Research based on G2 Ocean's public website (g2ocean.com), MyG2 platform marketing pages, OceanDocs documentation, Shipsgo carrier data, CargoX partnership announcements, Crunchbase, Gearbulk corporate site, and industry publications. No API credentials were obtained or used.
> **Researched by**: Agent (carrier API audit workflow)
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | G2 Ocean AS (commonly "G2 Ocean") |
| **SCAC Code** | GSSW |
| **Parent Company** | Joint venture between Gearbulk Holding and Grieg Maritime Group (Grieg Star) |
| **Alliance** | Independent (not a member of 2M, THE Alliance, or Ocean Alliance) |
| **Primary Services** | Open hatch / breakbulk, bulk, project cargo, forest products, steel, non-ferrous metals |
| **Market Position** | World's largest shipping company in the open hatch segment. Fleet of ~125 open hatch and bulk vessels (23,500-73,000 DWT). Operates 37 trade lanes across ~60 countries with 3,500+ port calls/year. Not a container liner -- specializes in breakbulk and semi-bulk cargo |
| **Headquarters** | Bergen, Norway |
| **Website** | [https://www.g2ocean.com/](https://www.g2ocean.com/) |

### Corporate Structure

| Entity | Role | Digital Infrastructure |
|--------|------|----------------------|
| **G2 Ocean AS** | Operating company (JV between Gearbulk and Grieg Star) | MyG2 platform, OceanDocs |
| **Gearbulk Holding** | Parent/co-owner -- open hatch vessel owner | Separate corporate IT |
| **Grieg Maritime Group (Grieg Star)** | Parent/co-owner -- open hatch/bulk vessel owner | Merged IT via UnITy |
| **UnITy** | Joint IT department (G2 Ocean + Gearbulk + Grieg Star) | Described as "Norway's largest shipping IT hub" |

> **Note on cargo type**: G2 Ocean is **not a container carrier** in the traditional sense. They specialize in open hatch vessels for breakbulk, project cargo, forest products, steel, and bulk commodities. This fundamentally differs from the container liner model that DCSA standards and most tracking APIs are designed for. Container-specific milestones (gate-in/gate-out, equipment events) do not apply in the same way to breakbulk operations.

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | **No** -- no public developer portal or API documentation |
| **Developer portal URL** | N/A |
| **API documentation URL(s)** | N/A -- no publicly documented REST/SOAP API |
| **Documentation quality** | None -- no public API documentation exists |
| **OpenAPI/Swagger spec available?** | No |
| **Sandbox/test environment?** | No / Unknown |
| **Developer registration** | N/A |
| **Developer support channels** | General contact via G2 Ocean commercial offices |
| **Community/third-party libraries** | None found -- no GitHub repos, npm packages, or PyPI packages for G2 Ocean API integration |
| **API changelog / release notes** | N/A |

### Digital Platforms

G2 Ocean operates two customer-facing digital platforms, neither of which exposes a public API:

**MyG2** ([https://myg2.g2ocean.com](https://myg2.g2ocean.com)) -- G2 Ocean's primary digital customer platform. Features include:
- Live cargo tracking (vessel position, shipment status, ETA)
- Live sailing schedules (customizable views)
- Booking management (with integration capability for internal systems)
- Performance data (shipment volumes, transit times, port productivity)
- Scope 3 emissions tracking (live and historical voyage data)
- Historical data access
- Security controls for data protection

MyG2's marketing material states: "You can integrate your internal systems with MyG2 to automate transactions and transfer data related to bookings, including milestones and performance data." This suggests some form of system-to-system integration exists, but no public API documentation is available. The integration capability likely requires a direct business relationship and custom onboarding.

**OceanDocs** ([https://www.g2ocean.com/oceandocs/](https://www.g2ocean.com/oceandocs/)) -- Digital cargo documentation platform for shippers and agents. Features:
- End-to-end supply chain visibility
- Bill of Lading management (creation through to destination)
- Centralized documentation for the voyage journey
- Port Authority access for schedules and cargo line-ups
- Cargo release status visibility at discharge port

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | **No** -- G2 Ocean is not a DCSA member. DCSA membership is limited to container liner carriers (the 10 members are MSC, Maersk, CMA CGM, Hapag-Lloyd, ONE, Evergreen, Yang Ming, HMM, ZIM, and PIL). G2 Ocean operates in the open hatch/breakbulk segment, which is outside DCSA's scope |
| **DCSA APIs implemented** | None |
| **DCSA TNT version** | N/A |
| **DCSA Booking version** | N/A |
| **DCSA Schedules version** | N/A |
| **Known DCSA deviations** | N/A -- no DCSA implementation. DCSA standards are designed for containerized shipping and do not directly apply to G2 Ocean's breakbulk/open hatch operations |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Unknown | No public documentation on EDI support. As a major operator in breakbulk shipping with 3,500+ port calls/year, some EDI capability is likely for terminal/port communications (e.g., BAPLIE for stowage plans), but this is unconfirmed |
| **INTTRA integration** | Unknown | INTTRA (E2open) primarily serves the container liner segment. G2 Ocean's breakbulk focus makes INTTRA integration unlikely |
| **BIC (Bureau International des Containers)** | Unknown | BIC standards are container-focused; limited applicability to open hatch cargo |
| **UN/LOCODE** | Unknown | Likely used internally for port identification given global operations |
| **CargoX (blockchain eBL)** | Yes | G2 Ocean partnered with CargoX in 2019 for blockchain-based electronic Bill of Lading. Pilot completed with Manuchar NV: 5 shipments from Peru to China. Document ownership transfer reduced from days/weeks to minutes |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | N/A -- no public API. MyG2 platform uses web-based authentication (login credentials) |
| **Auth documentation** | N/A |
| **Registration process** | MyG2 access requires a business relationship with G2 Ocean. Registration is not self-service |
| **Registration URL** | N/A |
| **Partner program required?** | Yes -- for any digital platform access |
| **Partner program URL** | N/A -- contact G2 Ocean commercial team |
| **Credential type** | Username/password for MyG2 web portal |
| **Token refresh supported?** | N/A |
| **Token lifetime** | N/A |
| **Access tiers** | Unknown -- likely single tier tied to customer relationship |
| **IP whitelisting required?** | Unknown |

### Access Requirements Summary for SSL

G2 Ocean does not expose a public API. All digital access is through the MyG2 customer portal, which requires an active business relationship with G2 Ocean. SSL would need to:

1. Establish a commercial relationship with G2 Ocean (as a shipper, freight forwarder, or agent)
2. Request MyG2 portal access through the G2 Ocean commercial team
3. Potentially negotiate system-to-system integration access (mentioned in MyG2 marketing but not publicly documented)

The lack of a public API means that programmatic integration would require either (a) direct partnership negotiation for system integration access, (b) third-party aggregator coverage, or (c) web scraping of the MyG2 portal (subject to ToS assessment).

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field must have a row.
> Note: G2 Ocean is a breakbulk/open hatch carrier, not a container liner. Many DCSA container-specific fields do not directly apply.

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ⚠️ | MyG2 portal (no API) | Live sailing schedules via MyG2 | N/A | Available in MyG2 portal but no programmatic API access. Schedules also available by contacting G2 Ocean offices directly |
| 1.2 | Point-to-Point Route Options | ⚠️ | MyG2 portal (no API) | Trade routes and schedule data | N/A | G2 Ocean operates 37 trade lanes; route info visible on website and MyG2 but not via API |
| 1.3 | Booking Lifecycle | ⚠️ | MyG2 portal (no API) | Booking management via MyG2 | N/A | MyG2 supports booking management with integration capability mentioned, but no public API |
| 1.4 | Shipping Instructions | ⚠️ | OceanDocs portal (no API) | Bill of Lading management via OceanDocs | N/A | OceanDocs handles documentation lifecycle but has no public API. CargoX eBL integration piloted |
| 1.5 | Rates | ❌ | N/A | N/A | N/A | No public rate API. Rates obtained via commercial negotiations with G2 Ocean offices |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❌ | N/A | N/A | `ECP` | Not applicable -- G2 Ocean is a breakbulk carrier, not a container liner. Cargo is loaded directly onto vessels, not into containers (in most cases) |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❌ | N/A | N/A | `EFC` | Not applicable -- breakbulk operations |
| 2.3 | Documentation Cutoff | DCO | ❓ | N/A | N/A | `DCO` | Likely exists operationally (documentation deadlines are universal in shipping) but not exposed via any API |
| 2.4 | VGM Cutoff | VCO | ❌ | N/A | N/A | `VCO` | VGM is a SOLAS requirement for containers. Not applicable to breakbulk cargo in the same way |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ❌ | N/A | N/A | `FCO` | Not applicable -- breakbulk operations. Cargo cutoffs may exist operationally but are cargo-receiving deadlines, not container-specific |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❌ | N/A | N/A | `LCO` | Not applicable -- breakbulk operations |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ❌ | N/A | N/A | Inferred from first EquipmentEvent | Not applicable -- breakbulk cargo is not containerized |
| 3.2 | Empty Container Gate-Out (Pickup) | ❌ | N/A | N/A | `GTOT` + `EMPTY` | Not applicable -- no container pickup in breakbulk operations |
| 3.3 | Full Container Gate-In | ❌ | N/A | N/A | `GTIN` + `LADEN` | Not applicable -- cargo delivered directly to port/vessel |
| 3.4 | Container Loaded on Vessel | ⚠️ | MyG2 portal (no API) | Cargo loaded milestone likely tracked in MyG2 | `LOAD` + `LADEN` | Conceptually similar -- cargo loading on vessel is tracked in MyG2 but as breakbulk loading, not container loading. No API access |
| 3.5 | Container Discharged at Transshipment | ❓ | N/A | N/A | `DISC` + `LADEN` + transshipment | Unknown -- breakbulk transshipment is less common but does occur |
| 3.6 | Container Loaded at Transshipment | ❓ | N/A | N/A | `LOAD` + `LADEN` + transshipment | Unknown -- same as above |
| 3.7 | Container Discharged at Destination | ⚠️ | MyG2 portal (no API) | Cargo discharged milestone likely tracked in MyG2 | `DISC` + `LADEN` | Conceptually tracked -- cargo discharge at destination is tracked in MyG2 and OceanDocs (cargo release status at discharge port). No API access |
| 3.8 | Full Container Gate-Out (Delivery) | ❓ | N/A | N/A | `GTOT` + `LADEN` | Unknown -- cargo release from port may be tracked in OceanDocs (release conditions visibility) but not via API |
| 3.9 | Empty Container Returned | ❌ | N/A | N/A | `GTIN` + `EMPTY` | Not applicable -- no containers to return in breakbulk operations |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ⚠️ | MyG2 portal (no API) | ETD in live sailing schedules and cargo tracking | `DEPA` + classifier | Available in MyG2 portal (live tracking shows vessel position and schedule). No API access |
| 4.2 | Estimated Time of Arrival | ETA | ⚠️ | MyG2 portal (no API) | ETA in live tracking and sailing schedules | `ARRI` + classifier | Available in MyG2 portal. Third-party trackers (Shipsgo) also provide ETA predictions. No API access |
| 4.3 | Vessel Arrival at Transshipment | -- | ❓ | N/A | N/A | `ARRI` at intermediate | Unknown -- breakbulk transshipment is less common |
| 4.4 | Vessel Departure from Transshipment | -- | ❓ | N/A | N/A | `DEPA` at intermediate | Unknown -- breakbulk transshipment is less common |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❌ | No public API, no webhook capability |
| Event Polling with timestamp filter | ❌ | No public API |
| Event Classifier Progression (PLN->EST->ACT) | ❌ | No DCSA implementation |
| Retracted Events | ❌ | No event API |
| Change Remarks | ❌ | No event API |
| Delay Reason Codes | ❌ | No event API |

### Coverage Summary

| Category | Fields Available | Fields Unavailable | Fields Unknown | Coverage % |
|----------|-----------------|-------------------|----------------|-----------|
| API Domains (1.x) | 0/5 | 1/5 | 0/5 | 0% |
| Cutoffs (2.x) | 0/6 | 5/6 | 1/6 | 0% |
| Container Milestones (3.x) | 0/9 | 5/9 | 4/9 | 0% |
| Transport Events (4.x) | 0/4 | 0/4 | 2/4 | 0% |
| Change Detection (5.x) | 0/6 | 6/6 | 0/6 | 0% |
| **Total** | **0/30** | **17/30** | **7/30** | **0%** |

> **Note on "Available with caveats" (warning icon) fields**: Several fields are marked with warning icon in the matrix above (Schedules, P2P, Booking, Shipping Instructions, Loaded on Vessel, Discharged at Destination, ETD, ETA) because the data exists in the MyG2 portal but is not accessible via any public API. For the purpose of this coverage summary, these are counted as "unavailable" because there is no programmatic access method. If G2 Ocean were to expose their MyG2 data through an API, the coverage picture would improve significantly for transport-event-like data.

---

## Endpoint Reference

G2 Ocean does not expose any public API endpoints. This section is intentionally left empty.

---

## Rate Limits & Quotas

| Detail | Value | Source |
|--------|-------|--------|
| **Global rate limit** | N/A -- no public API | N/A |
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
| **Tracking URL** | [https://myg2.g2ocean.com/cargo-tracking](https://myg2.g2ocean.com/cargo-tracking) |
| **Login required?** | Yes -- requires MyG2 account (business relationship with G2 Ocean) |
| **Data available on portal but NOT in API** | All data is portal-only: live tracking, vessel positions, ETD/ETA, sailing schedules, booking management, cargo milestones, performance data, emissions data, and cargo release status (via OceanDocs). No API exists |
| **Scraping feasibility** | Difficult -- MyG2 is a JavaScript SPA (Vue.js or similar; page shows "MyG2 doesn't work properly without JavaScript enabled"), requiring login and likely session-based authentication. Anti-bot measures not assessed. ToS not reviewed |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Unknown |
| **EDI message types** | Unknown -- no public documentation. As a major breakbulk operator with 3,500+ port calls/year, BAPLIE support for terminal communication is probable but unconfirmed |
| **EDI connection method** | Unknown |
| **EDI documentation** | Contact G2 Ocean commercial team |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Unknown | project44 focuses primarily on container shipping. G2 Ocean's breakbulk focus makes coverage uncertain |
| **FourKites** | Unknown | FourKites covers ocean, but primarily container-focused carriers |
| **Vizion** | Unknown | Not found in Vizion's supported carrier list. Vizion is container-tracking focused |
| **INTTRA / E2open** | Unknown | INTTRA primarily serves container liner segment; unlikely to cover G2 Ocean's breakbulk operations |
| **CargoSmart** | Unknown | CargoSmart is COSCO-affiliated and container-focused |
| **Shipsgo** | Yes | Shipsgo lists G2 Ocean (SCAC: GSSW) and offers tracking by container number, B/L number, and booking number. Provides ETA predictions, vessel position, sailing/delay notifications, container release alerts. Note: Shipsgo likely uses AIS (vessel tracking) data rather than direct carrier integration for breakbulk visibility |
| **SeaRates** | Yes | SeaRates lists G2 Ocean container tracking, but coverage depth is unclear |
| **E-tracking** | Yes | E-tracking.net lists G2 Ocean for container and B/L tracking |

> **Aggregator note**: Despite being listed on several tracking aggregator platforms, the tracking data for G2 Ocean is likely AIS-based (vessel position tracking) rather than carrier-API-based event tracking. This means vessel-level visibility (ETD/ETA, port calls) may be available, but cargo-level visibility (specific shipment milestones, documentation status) is not available through aggregators. The distinction between vessel tracking and shipment tracking is critical for a breakbulk carrier like G2 Ocean.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown -- no API. MyG2 describes "live tracking" and "up-to-the-minute performance data" but no specific latency figures published | Marketing material (Estimated) |
| **API uptime/reliability** | N/A -- no public API | N/A |
| **Historical data depth** | Unknown -- MyG2 mentions "historical data" as a feature, but depth not specified | Marketing material |
| **Timezone handling** | Unknown | Unknown |
| **Character encoding** | Unknown | Unknown |

### Known Issues & Gotchas

- G2 Ocean is a **breakbulk/open hatch carrier**, not a container liner. DCSA standards and container-specific tracking fields (equipment events, gate-in/gate-out, container assignment) do not apply to their primary cargo types
- The MyG2 platform mentions "integration capability" for internal systems, suggesting some form of API or data exchange exists internally. However, this is not publicly documented and likely requires partnership negotiation
- G2 Ocean's joint IT department "UnITy" (merged with Gearbulk and Grieg Star IT) indicates a centralized tech stack, but the platform appears to be closed/proprietary
- The CargoX blockchain eBL pilot (2019) indicates willingness to adopt digital documentation standards, but the current status of this initiative is unclear
- Third-party tracking platforms list G2 Ocean, but the tracking data is likely AIS-based vessel tracking rather than cargo-level event data from G2 Ocean's systems

### Recently Deprecated or Changed

- No known deprecations (no public API to deprecate)

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | No -- G2 Ocean has no public API. The carrier operates in the breakbulk segment, which is fundamentally different from container shipping and outside SSL's primary tracking use case |
| **Implementation effort** | Very High (no API) -- would require either partnership negotiation for system integration access, web scraping of MyG2 (which is a JS SPA requiring auth), or reliance on AIS-based vessel tracking through third parties |
| **DCSA base adapter usable?** | No -- fully custom. DCSA standards are designed for containerized shipping. G2 Ocean's breakbulk cargo model does not map to DCSA equipment events, container milestones, or cutoff codes |

### Recommended Approach

G2 Ocean is not a viable candidate for the SDK's current container-focused tracking adapter pattern. The carrier has no public API, operates in the breakbulk/open hatch segment rather than container shipping, and DCSA standards do not apply to their cargo model.

If SSL needs to track G2 Ocean shipments, the recommended approach would be:

1. **Partnership negotiation**: Contact G2 Ocean's commercial team to inquire about the system integration capability mentioned in MyG2 marketing materials. This would require a business relationship and likely custom development
2. **AIS-based vessel tracking**: Use a vessel tracking service (MarineTraffic, VesselFinder, or Shipsgo) to get vessel-level visibility (ETD/ETA, port calls). This provides vessel position data but not cargo-level milestones
3. **De-prioritize**: Given that G2 Ocean operates in breakbulk rather than containerized shipping, it may fall outside SSL's primary integration scope. Consider adding G2 Ocean only if specific customer demand requires it

### Recommended Lookup Method

B/L number would be the primary shipment identifier, as booking references and B/L numbers are the standard identifiers in breakbulk shipping. Container numbers have limited applicability since most G2 Ocean cargo is not containerized.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | N/A -- no API to poll |
| **Incremental filter** | N/A |
| **Batch tracking** | N/A |

If AIS-based vessel tracking were used as a fallback:

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Every 4-6 hours (vessel positions update based on AIS transmission intervals) |
| **Incremental filter** | Filter by vessel IMO and compare position/ETA changes |
| **Batch tracking** | Multiple vessels can be monitored per account with most AIS providers |

### Auth Implementation Notes

N/A -- no public API. MyG2 uses web-based session authentication (JavaScript SPA). No OAuth, API key, or bearer token mechanism is publicly documented.

### Edge Cases to Handle

- Breakbulk cargo may be shipped on deck or in holds, with loading/unloading spanning multiple days at a single port (unlike container operations where a single container is loaded in one crane move)
- G2 Ocean vessels may carry cargo for multiple shippers on a single voyage, with partial loading/unloading at multiple ports along a route
- Project cargo shipments may have unique handling requirements that affect timelines in ways not captured by standard container milestones

### Mapping Complexity

Mapping from G2 Ocean's (hypothetical) data model to the SSL canonical model would be very high complexity. The fundamental cargo model differs: breakbulk shipping tracks cargo by commodity/lot/booking rather than by container. Vessel-level events (arrival/departure) map reasonably well, but cargo-level events (loading/discharge) do not follow the DCSA container equipment event pattern. A completely custom mapping layer would be needed, and many SSL canonical fields (container milestones, equipment events, cutoff codes) would simply have no equivalent in breakbulk operations.

---

## Open Questions

- [ ] Does SSL have any customers who ship breakbulk cargo with G2 Ocean and need tracking visibility?
- [ ] Does G2 Ocean's MyG2 "system integration" capability include a REST API, or is it limited to EDI/file-based data exchange?
- [ ] What is the current status of G2 Ocean's CargoX blockchain eBL partnership? Is it in production use or still pilot/dormant?
- [ ] Does G2 Ocean support any EDI message types (IFTMIN, BAPLIE, etc.) for terminal/agent communication?
- [ ] Are any third-party aggregators able to provide cargo-level (not just vessel-level) tracking data for G2 Ocean shipments?

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | [https://www.g2ocean.com/](https://www.g2ocean.com/) |
| MyG2 Platform (About) | [https://www.g2ocean.com/about-myg2/](https://www.g2ocean.com/about-myg2/) |
| MyG2 Cargo Tracking | [https://myg2.g2ocean.com/cargo-tracking](https://myg2.g2ocean.com/cargo-tracking) |
| OceanDocs Platform | [https://www.g2ocean.com/oceandocs/](https://www.g2ocean.com/oceandocs/) |
| G2 Ocean Fleet | [https://www.g2ocean.com/our-fleet/](https://www.g2ocean.com/our-fleet/) |
| G2 Ocean Trades | [https://www.g2ocean.com/our-trades/](https://www.g2ocean.com/our-trades/) |
| Gearbulk - G2 Ocean | [https://www.gearbulk.com/business-areas/shipowning-and-commercial/g2-ocean/](https://www.gearbulk.com/business-areas/shipowning-and-commercial/g2-ocean/) |
| CargoX eBL Partnership | [https://cargox.io/content-hub/g2ocean-blockchain-push-paper-bill-lading-retirement](https://cargox.io/content-hub/g2ocean-blockchain-push-paper-bill-lading-retirement) |
| Shipsgo - G2 Ocean Tracking | [https://shipsgo.com/ocean/carriers/g2ocean/container-tracking](https://shipsgo.com/ocean/carriers/g2ocean/container-tracking) |
| Panjiva SCAC Profile | [https://panjiva.com/scac_profiles/profile/GSSW](https://panjiva.com/scac_profiles/profile/GSSW) |
| DCSA Members | [https://dcsa.org/about-us](https://dcsa.org/about-us) |
