# Eimskip -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing. Research based on the public API help page at api.eimskip.com/Help, Eimskip corporate website (eimskip.com), customer portal information, third-party aggregator carrier lists, and public web presence. No API credentials were obtained or used.
> **Researched by**: Agent (carrier API inventory workflow)
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | Eimskipafelag Islands hf. (Eimskip) |
| **SCAC Code** | EIMU |
| **Parent Company** | Independent (publicly traded on Nasdaq Iceland as EIM) |
| **Alliance** | Independent (not a member of 2M, THE Alliance, Ocean Alliance, or Gemini Cooperation) |
| **Primary Services** | Container (reefer and dry), refrigerated bulk, multipurpose container/bulk, LCL, project cargo, hazardous materials, cold chain logistics |
| **Market Position** | Leading transportation company in the North Atlantic; niche specialist in Iceland, Faroe Islands, Greenland, and North Atlantic trade lanes. Not a top-20 global container carrier by TEU volume but dominant in its regional niche, particularly for frozen and chilled commodities |
| **Headquarters** | Reykjavik, Iceland |
| **Website** | [https://www.eimskip.com/](https://www.eimskip.com/) |

### Company Background

Eimskip was founded on 17 January 1914 and is the oldest shipping company in Iceland. The company operates 56 offices in 20 countries across four continents (Europe, North America, South America, Asia). Eimskip operates seven vessels, including the Dettifoss and Bruarfoss (received in 2020), which sail in collaboration with Greenlandic shipping company Royal Arctic Line between Iceland, Greenland, the Faroe Islands, and Scandinavia.

### Key Trade Lanes

| Route | Description |
|-------|-------------|
| **Blue Route** | One of four named service rotations (routes are color-coded: blue, green, yellow, gray) |
| **Green Route** | Second named service rotation |
| **Yellow Route** | Third named service rotation |
| **Gray Route** | Fourth named service rotation |
| **Trans-Atlantic** | Portland (Maine), Halifax (Nova Scotia), Argentia (Newfoundland) to/from Iceland, Faroe Islands, Northern Europe, UK, Scandinavia, Baltics, Mediterranean |
| **North Atlantic Short-Sea** | Newfoundland, Nova Scotia, New England feeder services |
| **European Feeder** | Feeder services throughout Europe, including Denmark, UK, Norway |

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | **Yes (minimal)** -- a public ASP.NET Web API help page is available at api.eimskip.com/Help |
| **Developer portal URL** | [http://api.eimskip.com/Help](http://api.eimskip.com/Help) |
| **API documentation URL(s)** | [http://api.eimskip.com/Help](http://api.eimskip.com/Help) -- auto-generated ASP.NET Web API help page listing endpoints with basic parameter descriptions |
| **Documentation quality** | **Poor** -- auto-generated help pages with minimal descriptions. Many endpoints have "No documentation available" for their descriptions. No usage guides, tutorials, authentication documentation, or integration examples. Some individual endpoint pages return server errors |
| **OpenAPI/Swagger spec available?** | No -- documentation is ASP.NET Web API Help Pages format, not OpenAPI/Swagger |
| **Sandbox/test environment?** | Unknown -- no sandbox or test environment is documented |
| **Developer registration** | Unknown -- no registration process is documented. The API appears to be partially public (e.g., vessel schedules, share info) but tracking likely requires credentials |
| **Developer support channels** | Not documented -- general contact via Eimskip commercial offices |
| **Community/third-party libraries** | None found -- no GitHub repos, npm packages, or PyPI packages for Eimskip API integration |
| **API changelog / release notes** | Not published |

### API Platform Overview

The Eimskip API at `api.eimskip.com` is an ASP.NET Web API application. It exposes the following endpoint groups:

| Group | Endpoints | Purpose |
|-------|-----------|---------|
| **VesselSchedule** | 6 endpoints | Sailing schedules by route, point-to-point search, ports of loading/discharge lists |
| **CargoStatus** | 1 endpoint | Cargo tracking by tracking number |
| **VesselLocation** | 1 endpoint | Vessel position/AIS data by vessel ID |
| **ShareInfo** | 3 endpoints | Eimskip stock/share information and OMX news (investor relations, not shipping) |
| **Employees** | 4 endpoints | Employee directory search (internal HR, not shipping) |

Of the five endpoint groups, only **VesselSchedule**, **CargoStatus**, and **VesselLocation** are relevant to shipping operations.

### Customer Portal (Separate from API)

Eimskip also operates a customer portal at [portals.eimskip.com](https://portals.eimskip.com/en-US/) which provides:
- Booking requests and shipping instructions
- Shipment tracking with live operational data
- Overview of past, current, and upcoming shipments
- Document access
- Service requests
- Cargo status based on live data from the operational system

The customer portal requires login credentials and is separate from the public API at api.eimskip.com. The portal appears to expose more data than the public API (booking, shipping instructions, documents), but it is a web application, not a programmable API.

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | **No** -- Eimskip is not a DCSA member. The DCSA founding members are MSC, Maersk, CMA CGM, Hapag-Lloyd, ONE, Evergreen, Yang Ming, HMM, and ZIM. PIL became the 10th member in 2024. Eimskip is not among them |
| **DCSA APIs implemented** | None -- the Eimskip API is a proprietary REST API, not DCSA-compliant |
| **DCSA TNT version** | N/A |
| **DCSA Booking version** | N/A |
| **DCSA Schedules version** | N/A |
| **Known DCSA deviations** | N/A -- no DCSA implementation. The Eimskip API uses proprietary data models (e.g., VesselSchedule with Voyages/Ports, CargoStatus with trackingNr) that do not follow DCSA conventions |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Unknown | No public documentation of EDI capabilities. Given Eimskip's size and customer base, some EDI support is plausible but unconfirmed |
| **INTTRA integration** | Unknown | Eimskip does not appear on INTTRA/E2open's publicly listed carrier networks, but this is not conclusive |
| **BIC (Bureau International des Containers)** | Unknown | Container prefix EIMU suggests BIC registration |
| **UN/LOCODE** | Unknown | Ports in the schedule API use port names (not UN/LOCODE codes based on sample response structure) |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | Unknown -- not documented in the public API help pages |
| **Auth documentation** | None found |
| **Registration process** | Unknown -- no developer registration process is documented |
| **Registration URL** | N/A |
| **Partner program required?** | Unknown -- likely requires business relationship for tracking/booking features; schedule endpoints may be publicly accessible |
| **Partner program URL** | N/A |
| **Credential type** | Unknown |
| **Token refresh supported?** | Unknown |
| **Token lifetime** | Unknown |
| **Access tiers** | Unknown -- likely single tier for business customers |
| **IP whitelisting required?** | Unknown |

### Access Requirements Summary for SSL

The authentication mechanism for the Eimskip API is entirely undocumented on the public help pages. The API appears to be a partially public system -- vessel schedule and vessel location endpoints may work without authentication (they serve the eimskip.com website), while the CargoStatus endpoint likely requires some form of credentials. SSL would need to contact Eimskip directly to understand:

1. Whether API access is available to third-party integrators
2. What authentication credentials are needed
3. Whether a business/partnership agreement is required
4. What access tiers or usage limits exist

Given Eimskip's position as a niche North Atlantic carrier, API access may be restricted to direct customers rather than offered as a developer platform.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field must have a row.
> Available = Available | Unavailable = Not available | Partial = Partial / limited | Unknown = Unknown

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ✅ | `GET api/VesselSchedule/{lang}/{route}`, `GET api/VesselSchedule/Search`, `GET api/VesselSchedule/{lang}` | VesselSchedule object with Voyages[].Ports[].ArrivalDate | N/A (proprietary) | Four named routes (blue, green, yellow, gray). Point-to-point search available with portFrom, portTo, dateFrom, dateTo params. Returns vessel name, route name, transit time, port arrival dates. Languages: en, is |
| 1.2 | Point-to-Point Route Options | ✅ | `GET api/VesselSchedule/Search` | portFrom, portTo, dateFrom, dateTo parameters | N/A (proprietary) | Search by origin/destination port and date range. Port lists available via GetPOL and GetPOD endpoints |
| 1.3 | Booking Lifecycle | ❌ | N/A | N/A | N/A | No booking API endpoints exist. Booking is handled through the customer portal (portals.eimskip.com) or direct contact with Eimskip offices |
| 1.4 | Shipping Instructions | ❌ | N/A | N/A | N/A | No shipping instruction endpoints exist. SI submission is through the customer portal |
| 1.5 | Rates | ❌ | N/A | N/A | N/A | No rate/pricing API endpoints. Rates handled through commercial agreements and direct contact |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❓ | Unknown | Unknown | `ECP` | Not documented in the public API. May be available through the CargoStatus endpoint or customer portal but unverified |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❓ | Unknown | Unknown | `EFC` | Same as 2.1 -- not documented |
| 2.3 | Documentation Cutoff | DCO | ❓ | Unknown | Unknown | `DCO` | Same as 2.1 -- not documented |
| 2.4 | VGM Cutoff | VCO | ❓ | Unknown | Unknown | `VCO` | Same as 2.1 -- not documented |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ❓ | Unknown | Unknown | `FCO` | Same as 2.1 -- not documented |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❓ | Unknown | Unknown | `LCO` | Same as 2.1 -- not documented |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ❓ | Unknown | Unknown | Inferred from first EquipmentEvent | CargoStatus endpoint accepts a trackingNr; response structure is undocumented. The customer portal shows "cargo status based on live data from our operation system" but what events are exposed programmatically is unknown |
| 3.2 | Empty Container Gate-Out (Pickup) | ❓ | `GET api/CargoStatus?trackingNr={nr}` | Unknown | `GTOT` + `EMPTY` | Response fields not documented |
| 3.3 | Full Container Gate-In | ❓ | `GET api/CargoStatus?trackingNr={nr}` | Unknown | `GTIN` + `LADEN` | Response fields not documented |
| 3.4 | Container Loaded on Vessel | ❓ | `GET api/CargoStatus?trackingNr={nr}` | Unknown | `LOAD` + `LADEN` | Response fields not documented |
| 3.5 | Container Discharged at Transshipment | ❓ | `GET api/CargoStatus?trackingNr={nr}` | Unknown | `DISC` + `LADEN` + transshipment | Response fields not documented. Eimskip operates primarily direct services with limited transshipment, so this event may be rare |
| 3.6 | Container Loaded at Transshipment | ❓ | `GET api/CargoStatus?trackingNr={nr}` | Unknown | `LOAD` + `LADEN` + transshipment | Same as 3.5 |
| 3.7 | Container Discharged at Destination | ❓ | `GET api/CargoStatus?trackingNr={nr}` | Unknown | `DISC` + `LADEN` | Response fields not documented |
| 3.8 | Full Container Gate-Out (Delivery) | ❓ | `GET api/CargoStatus?trackingNr={nr}` | Unknown | `GTOT` + `LADEN` | Response fields not documented |
| 3.9 | Empty Container Returned | ❓ | `GET api/CargoStatus?trackingNr={nr}` | Unknown | `GTIN` + `EMPTY` | Response fields not documented |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ⚠️ | `GET api/VesselSchedule/{lang}/{route}`, `GET api/VesselSchedule/Search` | Voyages[].Ports[].ArrivalDate | `DEPA` + classifier | Schedule endpoints return ArrivalDate per port but no explicit departure date field. ETD may need to be inferred from previous port's arrival + transit patterns. Only planned schedule data; no EST/ACT progression |
| 4.2 | Estimated Time of Arrival | ETA | ✅ | `GET api/VesselSchedule/{lang}/{route}`, `GET api/VesselSchedule/Search` | Voyages[].Ports[].ArrivalDate | `ARRI` + classifier | ArrivalDate available per port in schedule data. Only PLN (planned) equivalent; no EST/ACT progression documented |
| 4.3 | Vessel Arrival at Transshipment | -- | ⚠️ | `GET api/VesselSchedule/{lang}/{route}` | Voyages[].Ports[].ArrivalDate at intermediate ports | `ARRI` at intermediate | Available for ports on the route schedule, but only as planned schedule data. Eimskip routes have limited transshipment |
| 4.4 | Vessel Departure from Transshipment | -- | ❓ | Unknown | Unknown | `DEPA` at intermediate | No explicit departure data in schedule response |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❌ | No webhook or push notification capability documented |
| Event Polling with timestamp filter | ❓ | CargoStatus endpoint exists but filter parameters are unknown |
| Event Classifier Progression (PLN->EST->ACT) | ❌ | No evidence of event classifier progression. Schedule data appears to be planned only |
| Retracted Events | ❌ | No evidence of retracted event support |
| Change Remarks | ❌ | No evidence of change remark fields |
| Delay Reason Codes | ❌ | No evidence of delay reason code support |

### Coverage Summary

| Category | Fields Available | Fields Unavailable | Fields Unknown | Coverage % |
|----------|-----------------|-------------------|----------------|-----------|
| API Domains (1.x) | 2/5 | 3/5 | 0/5 | 40% |
| Cutoffs (2.x) | 0/6 | 0/6 | 6/6 | 0% (all unknown) |
| Container Milestones (3.x) | 0/9 | 0/9 | 9/9 | 0% (all unknown) |
| Transport Events (4.x) | 1/4 | 0/4 | 1/4 | 25% (+ 2 partial) |
| Change Detection (5.x) | 0/6 | 4/6 | 2/6 | 0% |
| **Total** | **3/30** | **7/30** | **18/30** | **10% confirmed + 2 partial** |

---

## Endpoint Reference

### Tracking / Events

| Endpoint | Method | Lookup Params | Pagination | Response Format | Notes |
|----------|--------|--------------|------------|----------------|-------|
| `api/CargoStatus` | GET | trackingNr (booking number or container number) | Unknown | JSON, XML | Response structure is undocumented. The help page has "No documentation available" for this endpoint's description. Individual endpoint detail page returns server error |

### Schedules

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| `api/VesselSchedule/{lang}/{route}` | GET | lang (is/en), route (blue/green/yellow/gray) | None | JSON, XML | Returns VesselSchedule collection with Voyages containing VesselCode, VesselName, RouteName, TransitTime, Ports with ArrivalDate |
| `api/VesselSchedule/Search` | GET | portFrom, portTo, dateFrom, dateTo, lang | Unknown | JSON, XML | Point-to-point schedule search. Endpoint detail page returns server error |
| `api/VesselSchedule/{lang}` | GET | lang (is/en) | None | JSON, XML | Returns all vessel schedules in specified language |
| `api/VesselSchedule/GetPOL/{lang}` | GET | lang (is/en) | None | JSON, XML | Returns all ports of loading |
| `api/VesselSchedule/GetPOD/{lang}` | GET | lang (is/en) | None | JSON, XML | Returns all ports of discharge |
| `api/VesselSchedule/ActiveRoutes/{lang}` | GET | lang (is/en) | None | JSON, XML | Returns active routes. "No documentation available" |

### Vessel Location

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| `api/VesselLocation/{id}` | GET | id (vessel identifier) | None | JSON, XML | Returns AIS-type vessel position data: MMSI, Lat, Longitude, Speed, Course, Timestamp, Shipname, Shiptype, IMO, Callsign, Flag, CurrentPort, LastPort, LastPortTime, Destination, ETA, Length, Width, Draught, GRT, DWT, YearBuilt |

### Other Endpoints (Not Shipping-Relevant)

| Endpoint | Method | Purpose | Key Params | Notes |
|----------|--------|---------|-----------|-------|
| `api/ShareInfo` | GET | Eimskip stock/share information | None | Investor relations data, not shipping |
| `api/ShareInfo/News` | GET | OMX stock exchange news | None | Investor relations data, not shipping |
| `api/Employees` | GET/POST | Employee directory search | searchStr, department, company, title | Internal HR tool, not shipping |

### Lookup Methods Summary

| Identifier Type | Supported? | Which Endpoints? | Notes |
|----------------|-----------|-----------------|-------|
| **Bill of Lading (B/L) number** | ❓ | Possibly CargoStatus | The trackingNr parameter may accept B/L numbers, but this is unverified |
| **Booking reference** | ❓ | Possibly CargoStatus | Third-party tracking sites indicate booking number is accepted |
| **Container number** | ❓ | Possibly CargoStatus | Third-party tracking sites indicate container number is accepted |
| **Carrier booking number** | ❓ | Unknown | May be the same as booking reference |
| **Vessel IMO / voyage** | ⚠️ | VesselLocation (by ID, which may be MMSI or IMO), VesselSchedule (by route) | VesselLocation returns IMO in response. VesselSchedule returns VesselCode and VesselName. No direct vessel IMO lookup for schedules |

---

## Rate Limits & Quotas

| Detail | Value | Source |
|--------|-------|--------|
| **Global rate limit** | Unpublished | Unknown |
| **Per-endpoint limits** | Unpublished | Unknown |
| **Daily/monthly quota** | Unpublished | Unknown |
| **Rate limit response** | Unknown | Unknown |
| **Rate limit by** | Unknown | Unknown |
| **Burst allowance** | Unknown | Unknown |
| **Different tiers** | Unknown | Unknown |

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

No webhook or push notification support available. Eimskip does not offer a documented public API.

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | [https://www.eimskip.com/find-shipment/](https://www.eimskip.com/find-shipment/) |
| **Login required?** | No for basic tracking (find-shipment page); Yes for full customer portal (portals.eimskip.com) |
| **Data available on portal but NOT in API** | The customer portal (portals.eimskip.com) provides: booking creation, shipping instructions submission, document access, service requests, detailed shipment history with live operational data. The public API exposes only schedules, basic cargo status, and vessel location |
| **Scraping feasibility** | Not assessed. The find-shipment page at eimskip.com appears to be a standard web form. ToS not reviewed |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Unknown |
| **EDI message types** | Unknown |
| **EDI connection method** | Unknown |
| **EDI documentation** | Unknown -- contact carrier |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Unknown | No specific evidence found for Eimskip coverage |
| **FourKites** | Unknown | No specific evidence found for Eimskip coverage |
| **Vizion** | No | Eimskip (EIMU) is not listed on Vizion's supported carriers page (docs.vizionapi.com/docs/supported-carriers) |
| **INTTRA / E2open** | Unknown | No specific evidence found. Eimskip not among commonly listed INTTRA carriers |
| **CargoSmart** | Unknown | CargoSmart claims 40+ ocean carriers but specific Eimskip support unconfirmed |
| **Terminal49** | No | Eimskip is not listed among Terminal49's 34 integrated shipping lines (terminal49.com/shipping-lines) |
| **Cargoson** | Yes | Cargoson lists Eimskip integration for booking and tracking via their unified API (cargoson.com/en/integrations/eimskipafelag-islands-hf). However, Cargoson is a freight forwarding platform, not a pure tracking aggregator |
| **SeaRates** | Yes | SeaRates provides Eimskip container tracking (searates.com/sealine/eimskip), likely via web scraping |
| **GoComet** | Yes | GoComet offers Eimskip container tracking with "Real-Time BL Status" (gocomet.com/online-container-tracking/carriers/eimskip), likely via web scraping |
| **Fluent Cargo** | Yes | Fluent Cargo lists Eimskip sailing schedules by SCAC EIMU (fluentcargo.com/carriers/scac/EIMU) |

> **Aggregator note**: The major professional-grade aggregators (project44, FourKites, Vizion, Terminal49) do not appear to support Eimskip. Coverage is available only through lighter-weight platforms (Cargoson, SeaRates, GoComet) which likely rely on web scraping or Eimskip's public API/portal rather than direct carrier integrations. This limits the options for a high-quality aggregator-based integration path.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown | Unknown |
| **API uptime/reliability** | Unknown -- some individual endpoint documentation pages return server errors, which may indicate intermittent API issues or simply poor documentation hosting | Observed during research |
| **Historical data depth** | Unknown | Unknown |
| **Timezone handling** | Timestamps in sample responses use ISO 8601 with timezone offset (e.g., `2026-02-17T20:36:31...+00:00`) | Official (api.eimskip.com/Help) |
| **Character encoding** | Unknown -- Icelandic content (lang=is) may include special characters (thorn, eth, etc.) | Estimated |

### Known Issues & Gotchas

- The API documentation is hosted over plain HTTP (not HTTPS) at `http://api.eimskip.com/Help`. It is unknown whether the API itself requires HTTPS.
- Several individual endpoint documentation pages return "An error occurred while processing your request" (specifically the CargoStatus and VesselSchedule/Search detail pages). This may indicate the documentation is partially broken or the endpoints themselves have issues.
- Route names are color-coded (blue, green, yellow, gray) -- a proprietary convention that must be mapped to geographic trade lanes for SSL's use.
- The API serves dual purposes: some endpoints (ShareInfo, Employees) are clearly for the Eimskip corporate website, not for shipping integrations. The shipping-relevant endpoints are a subset of the full API.
- Port identification uses port names rather than standardized codes (e.g., UN/LOCODE), which will require fuzzy matching or a mapping table.
- The VesselLocation endpoint returns AIS-type data (MMSI, lat/lon, speed, course), suggesting it may pull from an AIS data provider rather than Eimskip's operational systems.

### Recently Deprecated or Changed

- No deprecation notices found. The API appears to be a long-standing ASP.NET application with minimal changes.

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | Partial -- schedule data (1.1, 1.2, 4.2) is confirmed available. Tracking (3.x) has an endpoint but its response structure is undocumented and would require live testing to assess. Booking and SI are unavailable |
| **Implementation effort** | High (proprietary API with undocumented tracking endpoint, non-standard identifiers, no DCSA alignment) |
| **DCSA base adapter usable?** | No -- fully custom adapter required. Zero DCSA alignment in data models or conventions |

### Recommended Approach

The Eimskip adapter should be a fully custom, proprietary integration. There is no DCSA compliance to leverage.

**Phase 1 (Schedule + Vessel Location)**: Build an adapter consuming the VesselSchedule endpoints to provide schedule data and ETA information. The VesselLocation endpoint can supplement with real-time vessel position data (AIS). This is achievable with existing documentation.

**Phase 2 (Tracking -- requires live testing)**: The CargoStatus endpoint is the only tracking capability but its response format is entirely undocumented. SSL would need to obtain API credentials, make test calls, and reverse-engineer the response structure before implementation. This is the critical unknown.

**Phase 3 (Cutoffs and Milestones -- may not be feasible)**: If the CargoStatus endpoint returns milestone events and cutoff dates, these can be mapped to the canonical model. If it returns only basic status (e.g., "in transit", "delivered"), the adapter's value will be limited to schedule-level data.

An alternative approach is to integrate via a platform like Cargoson which already has Eimskip connectivity, though this adds a dependency and cost.

### Recommended Lookup Method

Based on third-party tracking sites (GoComet, SeaRates, e-tracking.net), both container number and booking number appear to be supported by Eimskip's tracking. Container number is the recommended primary lookup method as it is the most universal identifier across carrier APIs.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Every 4-6 hours (Eimskip operates weekly services with relatively long transit times in the North Atlantic; high-frequency polling is unnecessary) |
| **Incremental filter** | Unknown -- likely full re-fetch required since no timestamp filter parameters are documented for CargoStatus |
| **Batch tracking** | Unknown -- the CargoStatus endpoint appears to accept a single trackingNr. Batch tracking would require one call per shipment |

### Auth Implementation Notes

Authentication details are entirely unknown. The adapter implementation must be designed to accommodate whatever auth mechanism Eimskip requires once credentials are obtained. Given the ASP.NET platform, possibilities include: API key in header, bearer token, basic auth, or session-based auth. The adapter should use a pluggable auth strategy pattern.

### Edge Cases to Handle

- Eimskip operates in the North Atlantic where weather delays are frequent -- schedule changes may be common
- Port names rather than UN/LOCODE codes require a mapping layer
- Route color codes (blue, green, yellow, gray) need translation to geographic descriptions
- Icelandic language content (lang=is) includes special characters that may need encoding handling
- Eimskip collaborates with Royal Arctic Line on some routes -- shared vessel operations may complicate vessel/route tracking
- Small fleet (7 vessels) means vessel rotation patterns are relatively predictable but schedule disruptions affect a larger proportion of services

### Mapping Complexity

**Medium-High**. The primary challenges are:

1. **Undocumented tracking response**: The CargoStatus response format is unknown, making milestone mapping impossible to plan without live testing.
2. **Port name normalization**: Converting Eimskip's port names to UN/LOCODE requires a mapping table covering North Atlantic ports (many of which are smaller ports not always consistently named).
3. **No event type codes**: Unlike DCSA carriers, Eimskip likely uses proprietary status descriptions rather than standardized event codes.
4. **Schedule-only ETD**: Departure times must be inferred from schedule data since only arrival dates are documented.
5. **No event progression model**: No PLN/EST/ACT classifier system means change detection must rely on comparing fetched values over time rather than carrier-provided progressions.

---

## Open Questions

- [ ] Does SSL have or need an existing business relationship with Eimskip?
- [ ] Is Eimskip a priority carrier for SSL, or a low-volume niche carrier? (This determines investment level)
- [ ] What does the CargoStatus endpoint actually return? Live testing with credentials is required to answer this
- [ ] Does the API require authentication for all endpoints, or are schedule/vessel endpoints publicly accessible?
- [ ] Does Eimskip support EDI messaging (IFTMIN, COPARN, IFTSTA)?
- [ ] Is the customer portal at portals.eimskip.com built on the same API, or does it use a different backend?
- [ ] Are there any unpublished API endpoints beyond what appears on the help page?
- [ ] Does Eimskip plan to adopt DCSA standards in the future?

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | [https://www.eimskip.com/](https://www.eimskip.com/) |
| API Help Page | [http://api.eimskip.com/Help](http://api.eimskip.com/Help) |
| Customer Portal | [https://portals.eimskip.com/en-US/](https://portals.eimskip.com/en-US/) |
| Customer Portal Info | [https://www.eimskip.com/customer-portal/](https://www.eimskip.com/customer-portal/) |
| Find Shipment (Tracking) | [https://www.eimskip.com/find-shipment/](https://www.eimskip.com/find-shipment/) |
| Liner Services | [https://www.eimskip.com/services/liner-services/](https://www.eimskip.com/services/liner-services/) |
| Vessel Fleet | [https://www.eimskip.com/about-eimskip/vessel-fleet/](https://www.eimskip.com/about-eimskip/vessel-fleet/) |
| Sailing Schedule (Web) | [https://www.eimskip.com/sailing-schedule/](https://www.eimskip.com/sailing-schedule/) |
| VesselSchedule API Endpoint | [http://api.eimskip.com/Help/Api/GET-api-VesselSchedule-lang](http://api.eimskip.com/Help/Api/GET-api-VesselSchedule-lang) |
| VesselSchedule Route Endpoint | [http://api.eimskip.com/Help/Api/GET-api-VesselSchedule-lang-route](http://api.eimskip.com/Help/Api/GET-api-VesselSchedule-lang-route) |
| VesselLocation Endpoint | [http://api.eimskip.com/Help/Api/GET-api-VesselLocation-id](http://api.eimskip.com/Help/Api/GET-api-VesselLocation-id) |
| Cargoson Integration | [https://www.cargoson.com/en/integrations/eimskipafelag-islands-hf](https://www.cargoson.com/en/integrations/eimskipafelag-islands-hf) |
| SeaRates Tracking | [https://www.searates.com/sealine/eimskip](https://www.searates.com/sealine/eimskip) |
| GoComet Tracking | [https://www.gocomet.com/online-container-tracking/carriers/eimskip](https://www.gocomet.com/online-container-tracking/carriers/eimskip) |
| Fluent Cargo Schedules | [https://www.fluentcargo.com/carriers/scac/EIMU](https://www.fluentcargo.com/carriers/scac/EIMU) |
| Vizion Supported Carriers | [https://docs.vizionapi.com/docs/supported-carriers](https://docs.vizionapi.com/docs/supported-carriers) |
| Terminal49 Shipping Lines | [https://terminal49.com/shipping-lines](https://terminal49.com/shipping-lines) |
