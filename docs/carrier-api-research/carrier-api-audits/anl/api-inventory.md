# ANL Container Line -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing
> **Researched by**: Agent
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

> **IMPORTANT -- CMA CGM Subsidiary**: ANL does not operate independent API infrastructure. All API access for ANL shipments is through CMA CGM's API portal at https://api-portal.cma-cgm.com. CMA CGM's APIs explicitly cover "all carriers of the CMA CGM group" including ANL. The CMA CGM API inventory at `docs/carriers/cma-cgm/api-inventory.md` is the authoritative and complete reference. This inventory documents ANL-specific details and references the parent inventory for shared infrastructure.

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | ANL Container Line (commonly "ANL"; formerly Australian National Line) |
| **SCAC Code** | ANNU |
| **Parent Company** | CMA CGM Group (acquired from Australian Government in 1998) |
| **Alliance** | Ocean Alliance (via CMA CGM, with COSCO Shipping, Evergreen, OOCL) -- extended until 2032 |
| **Primary Services** | Container shipping -- Oceania (Australia, New Zealand), Southeast Asia, Pacific Islands |
| **Market Position** | Regional specialist, Oceania and Pacific trade lanes. Part of CMA CGM Group (third-largest global carrier) |
| **Headquarters** | Melbourne, Australia |
| **Website** | https://www.anl.com.au |

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | No (uses CMA CGM's portal) |
| **Developer portal URL** | https://api-portal.cma-cgm.com (CMA CGM Group portal) |
| **API documentation URL(s)** | https://api-portal.cma-cgm.com (same as CMA CGM -- covers all group carriers) |
| **Documentation quality** | Good (inherited from CMA CGM -- DCSA-standard APIs have detailed descriptions; proprietary APIs briefer) |
| **OpenAPI/Swagger spec available?** | Yes -- via CMA CGM portal (requires login). DCSA standard specs also at https://github.com/dcsaorg/DCSA-OpenAPI |
| **Sandbox/test environment?** | No (same as CMA CGM -- free trial provides 1 month production access) |
| **Developer registration** | Requires approval -- register at CMA CGM portal, API key delivered within 2-3 days (public) or ~1 week (private) |
| **Developer support channels** | Business requests via https://api-portal.cma-cgm.com/contact-us/business-request; customer service at https://mycustomerservice.cma-cgm.com/s/selfcare/article/API-Solution?language=en_US |
| **Community/third-party libraries** | None ANL-specific. Python `tracktrace` library at https://github.com/dhruvkar/tracktrace supports CMA CGM (CMDU) which covers ANL |
| **API changelog / release notes** | Same as CMA CGM -- release notes on API detail pages |

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | No (ANL itself is not a DCSA member; parent CMA CGM is a founding member) |
| **DCSA APIs implemented** | TNT (Track & Trace), CS (Commercial Schedules -- PILOT) -- via CMA CGM infrastructure |
| **DCSA TNT version** | v2.2.0 (references DCSA Information Model v3.3) -- via CMA CGM |
| **DCSA Booking version** | N/A -- CMA CGM uses proprietary Booking Request API (DCSA alignment "Scheduled for future releases") |
| **DCSA Schedules version** | v1.0.7 (PILOT status) -- via CMA CGM |
| **Known DCSA deviations** | Same as CMA CGM: shipment events and DCSA subscription management endpoints are NOT implemented. Webhooks are proprietary |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Yes | Same as CMA CGM: IFTMBF, IFTMIN, IFTSTA, IFTMCS, IFTSAI, VERMAS |
| **INTTRA integration** | Yes | Via CMA CGM Group -- booking, schedules, rates, visibility/tracking |
| **BIC (Bureau International des Containers)** | Yes | Standard container ID format used throughout APIs |
| **UN/LOCODE** | Yes | Used in DCSA-compliant endpoints. CMA CGM proprietary APIs use CMA CGM-specific location codes |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | Dual: API Key (public APIs) + OAuth2 Client Credentials (private APIs) -- same as CMA CGM |
| **Auth documentation** | https://api-portal.cma-cgm.com/usage-guide |
| **Registration process** | Same as CMA CGM: 1. Register at portal 2. Account activated (2-3 days) 3. Free trial (1 month) 4. Subscribe for continued access |
| **Registration URL** | https://api-portal.cma-cgm.com |
| **Partner program required?** | No for public APIs. Private APIs require being identified on booking as Booking Party, Deciding Party, Consignee, Notifier, or Shipper |
| **Partner program URL** | N/A |
| **Credential type** | API Key (`KeyId` header) for public APIs; Client ID + Client Secret (OAuth2 `client_credentials`) for private APIs |
| **Token refresh supported?** | Yes -- re-request via OAuth2 client_credentials flow |
| **Token lifetime** | 299 seconds (~5 minutes) for OAuth2 tokens (Official) |
| **Access tiers** | Public (API Key -- standard events), Private (OAuth2 -- inland moves, GPS), Free Trial (1 month), Subscription (paid, some calls chargeable) |
| **IP whitelisting required?** | Unknown |

### Access Requirements Summary for SSL

ANL API access is obtained through CMA CGM's portal -- there is no separate ANL registration or credentialing process. SSL registers once at https://api-portal.cma-cgm.com and gains access to track all CMA CGM group carriers (CMA CGM, APL, ANL, CNC) with the same credentials.

The same access tiers and requirements apply as for CMA CGM: public API Key access for standard tracking events (2-3 day approval), OAuth2 client credentials for private-tier data including inland transport and GPS (requires being identified on the booking). If SSL already has CMA CGM API access, no additional registration is needed for ANL shipments.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field has a row.
> Coverage is identical to CMA CGM since ANL uses the same API infrastructure.
> See `docs/carriers/cma-cgm/api-inventory.md` for detailed endpoint and event code mappings.

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ✅ | CMA CGM: `GET /v1/port-schedules`, `GET /v1/vessel-schedules` (DCSA CS PILOT); Proprietary: Voyages, Lines & Services | Same as CMA CGM | DCSA CS v1 | DCSA endpoints in PILOT status |
| 1.2 | Point-to-Point Route Options | ✅ | CMA CGM: `GET /v1/point-to-point-routes` (DCSA CS PILOT); Proprietary: Routing Finder v2.9.7 | Same as CMA CGM | DCSA CS v1 | Routing Finder covers all CMA CGM group carriers including ANL |
| 1.3 | Booking Lifecycle | ✅ | CMA CGM: Booking Request API v1.10.0 (proprietary); Shipment API v3.14.2 | Same as CMA CGM | Not DCSA -- proprietary | Supports dry, reefer, hazardous, SOC, multi-container, inland |
| 1.4 | Shipping Instructions | ✅ | CMA CGM: Shipping Instruction API v2.5.1 (proprietary) | Same as CMA CGM | Not DCSA -- proprietary | v2.5.1 explicitly supports all CMA CGM group carriers |
| 1.5 | Rates | ❓ | CMA CGM: Pricing category visible on portal (requires login) | Unknown | Not DCSA | Details not accessible without subscription |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❓ | Unknown -- not explicitly documented in CMA CGM materials | Unknown | `ECP` | May be in Routing Finder or Booking response |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❓ | Unknown -- not explicitly documented | Unknown | `EFC` | May be in Routing Finder or Booking response |
| 2.3 | Documentation Cutoff | DCO | ⚠️ | CMA CGM Routing Finder API v2.9.7 (lists "SI cutoffs") | SI cutoff in Routing Finder | `DCO` | Partial confidence without live verification |
| 2.4 | VGM Cutoff | VCO | ⚠️ | CMA CGM Routing Finder API v2.9.7 (lists "VGM cutoffs") | VGM cutoff in Routing Finder | `VCO` | Partial confidence |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ⚠️ | CMA CGM Routing Finder API v2.9.7 (lists "Port cutoffs") | Port cutoff in Routing Finder | `FCO` | Partial confidence |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❓ | Unknown -- not explicitly mentioned | Unknown | `LCO` | No explicit LCL cutoff reference found |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ⚠️ | CMA CGM `GET /events` (TNT v2.2.0) | Inferred from first EquipmentEvent | Inferred from first EquipmentEvent | No explicit "assigned" event |
| 3.2 | Empty Container Gate-Out (Pickup) | ✅ | CMA CGM `GET /events` | `GTOT` + `EMPTY` | `GTOT` + `EMPTY` | Public visibility |
| 3.3 | Full Container Gate-In | ✅ | CMA CGM `GET /events` | `GTIN` + `LADEN` | `GTIN` + `LADEN` | Public visibility |
| 3.4 | Container Loaded on Vessel | ✅ | CMA CGM `GET /events` | `LOAD` + `LADEN` | `LOAD` + `LADEN` | Public visibility |
| 3.5 | Container Discharged at Transshipment | ✅ | CMA CGM `GET /events` | `DISC` + `LADEN` (transshipment) | `DISC` + `LADEN` + transshipment | Public visibility |
| 3.6 | Container Loaded at Transshipment | ✅ | CMA CGM `GET /events` | `LOAD` + `LADEN` at transshipment | `LOAD` + `LADEN` + transshipment | Inferred from location context |
| 3.7 | Container Discharged at Destination | ✅ | CMA CGM `GET /events` | `DISC` + `LADEN` | `DISC` + `LADEN` | Public visibility |
| 3.8 | Full Container Gate-Out (Delivery) | ✅ | CMA CGM `GET /events` | `GTOT` + `LADEN` | `GTOT` + `LADEN` | Public visibility |
| 3.9 | Empty Container Returned | ✅ | CMA CGM `GET /events` | `GTIN` + `EMPTY` | `GTIN` + `EMPTY` | Public visibility. ERT reference type in v1.2.7 |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ✅ | CMA CGM `GET /events`; Schedules APIs | `DEPA` with PLN/EST/ACT classifiers | `DEPA` + classifier | Full progression. Private tier adds inland departure |
| 4.2 | Estimated Time of Arrival | ETA | ✅ | CMA CGM `GET /events`; Schedules APIs | `ARRI` with PLN/EST/ACT classifiers | `ARRI` + classifier | Full progression. Private tier adds inland + GPS |
| 4.3 | Vessel Arrival at Transshipment | -- | ✅ | CMA CGM `GET /events` | `ARRI` at intermediate port | `ARRI` at intermediate | Distinguishable by location context |
| 4.4 | Vessel Departure from Transshipment | -- | ✅ | CMA CGM `GET /events` | `DEPA` at intermediate port | `DEPA` at intermediate | Distinguishable by location context |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ✅ (proprietary) | CMA CGM proprietary push system (NOT DCSA subscription model). Equipment, Shipment, Transport, Schedules, Shipment Release, Pricing event categories |
| Event Polling with timestamp filter | ✅ | DCSA TNT v2.2.0 `GET /events` with cursor-based pagination |
| Event Classifier Progression (PLN->EST->ACT) | ✅ | Standard DCSA classifier codes for transport events |
| Retracted Events | ❓ | Unknown -- in DCSA spec but CMA CGM implementation unconfirmed |
| Change Remarks | ❓ | Unknown -- in DCSA spec but CMA CGM implementation unconfirmed |
| Delay Reason Codes | ❓ | Unknown -- in DCSA spec but CMA CGM implementation unconfirmed |

### Coverage Summary

| Category | Fields Available | Fields Partial | Fields Unavailable | Fields Unknown | Coverage % |
|----------|-----------------|---------------|-------------------|----------------|-----------|
| API Domains (1.x) | 4/5 | 0/5 | 0/5 | 1/5 | 80% |
| Cutoffs (2.x) | 0/6 | 3/6 | 0/6 | 3/6 | 0% confirmed (3 partial) |
| Container Milestones (3.x) | 8/9 | 1/9 | 0/9 | 0/9 | 89% (1 partial) |
| Transport Events (4.x) | 4/4 | 0/4 | 0/4 | 0/4 | 100% |
| Change Detection (5.x) | 3/6 | 0/6 | 0/6 | 3/6 | 50% |
| **Total** | **19/30** | **4/30** | **0/30** | **7/30** | **63% confirmed (13% partial)** |

> **Note**: Coverage is identical to CMA CGM because ANL uses the same API infrastructure. See `docs/carriers/cma-cgm/api-inventory.md` for detailed notes on each field.

---

## Endpoint Reference

ANL shipments use the same endpoints as CMA CGM. See `docs/carriers/cma-cgm/api-inventory.md` for the complete endpoint reference. Key endpoints summarized below.

### Tracking / Events

| Endpoint | Method | Lookup Params | Pagination | Response Format | Notes |
|----------|--------|--------------|------------|----------------|-------|
| `GET /events` (unique tracking ref) | GET | B/L, booking ref, or container number | DCSA cursor-based (`limit`, page headers) | JSON (DCSA TNT v2.2.0) | Works for ANL shipments; mixed auth: OAuth2 + ApiKey |
| `GET /events` (search) | GET | Broader search parameters | Same cursor-based | JSON (DCSA TNT v2.2.0) | Broader event search across CMA CGM group |

### Schedules

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| `GET /v1/point-to-point-routes` | GET | Origin, destination, date range | DCSA cursor-based | JSON (DCSA CS v1) | PILOT. Covers ANL routes |
| `GET /v1/port-schedules` | GET | Port UNLocationCode, date | DCSA cursor-based | JSON (DCSA CS v1) | PILOT |
| `GET /v1/vessel-schedules` | GET | Service, voyage, vessel, location | DCSA cursor-based | JSON (DCSA CS v1) | PILOT |
| Routing Finder (proprietary) | GET | CMA CGM location codes | Range-based (HTTP 206) | JSON (proprietary) | v2.9.7. Returns ANL routes. Includes cutoffs, CO2 |

### Booking

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| Booking Request API | POST/PUT/DELETE | Booking reference, cargo details | Range-based | JSON (proprietary) | v1.10.0. Covers ANL bookings |
| Shipment API | GET | Shipment/booking reference | Range-based | JSON (proprietary) | v3.14.2. Live status for ANL shipments |

### Lookup Methods Summary

| Identifier Type | Supported? | Which Endpoints? | Notes |
|----------------|-----------|-----------------|-------|
| **Bill of Lading (B/L) number** | ✅ | Track & Trace, Shipment API | Primary lookup method |
| **Booking reference** | ✅ | Track & Trace, Shipment API, Booking API | Available pre-B/L issuance |
| **Container number** | ✅ | Track & Trace | Per-container tracking |
| **Carrier booking number** | ✅ | Same as booking reference | Interchangeable |
| **Vessel IMO / voyage** | ✅ | Schedules APIs, Track & Trace filtering | Schedule-level queries |

---

## Rate Limits & Quotas

Same as CMA CGM. See `docs/carriers/cma-cgm/api-inventory.md` for details.

| Detail | Value | Source |
|--------|-------|--------|
| **Global rate limit** | Yes -- per-application limits. Specific numbers unpublished | Official (CMA CGM) |
| **Per-endpoint limits** | Unpublished | Official (CMA CGM) |
| **Daily/monthly quota** | Unpublished | Unknown |
| **Rate limit response** | HTTP 429 with `retry-after` header (e.g., 3600 seconds) | Official (CMA CGM) |
| **Rate limit by** | Per-application (API key / OAuth token) | Official (CMA CGM) |
| **Burst allowance** | Unknown | Unknown |
| **Different tiers** | Some API calls are chargeable (200, 201, 204, 206, 400 billed; 401, 403, 429, 5XX not billed) | Official (CMA CGM) |

---

## Webhook / Push Support

Same as CMA CGM. See `docs/carriers/cma-cgm/api-inventory.md` for details.

| Detail | Value |
|--------|-------|
| **Webhooks supported?** | Yes -- CMA CGM proprietary event push system (NOT DCSA subscription model) |
| **Subscription endpoint** | Proprietary -- via CMA CGM portal |
| **Subscription management** | Proprietary -- portal-based configuration |
| **Subscribable event types** | Equipment, Shipment, Transport, Schedules, Shipment Release, Pricing |
| **Callback format** | Proprietary (not DCSA event JSON) |
| **Callback authentication** | API Key or OAuth2 Client Credentials (OAuth2 recommended) |
| **Retry policy on failure** | Configurable: max event age (default 24h), linear or exponential retry. 5XX retried; 4XX not |
| **Documented reliability** | No published SLA. Default 24h max event age |

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | https://www.anl.com.au/ebusiness/tracking (ANL-branded); also https://www.cma-cgm.com/ebusiness/tracking (CMA CGM, works for ANL shipments) |
| **Login required?** | No for basic tracking. Registered users (My ANL / My CMA CGM) get map view and event notifications |
| **Data available on portal but NOT in API** | Map visualization of container position at sea (portal-only rendering) |
| **Scraping feasibility** | Not assessed -- API coverage should be sufficient |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Yes (via CMA CGM Group) |
| **EDI message types** | IFTMBF (Booking), IFTMIN (Shipping instructions), IFTSTA (Tracking), IFTMCS (Bill of Lading), IFTSAI (Schedules), VERMAS (VGM) |
| **EDI connection method** | Unknown -- contact CMA CGM |
| **EDI documentation** | https://www.cma-cgm.com/products-services/ecommerce/edi-api-channels/EDI-catalog |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Yes | Explicitly lists ANL tracking at https://www.project44.com/tracking/container/anl/ |
| **FourKites** | Yes | Ocean visibility coverage via CMA CGM group |
| **Vizion** | Yes | Container tracking via CMA CGM group infrastructure |
| **INTTRA / E2open** | Yes | Via CMA CGM Group -- booking, schedules, rates, visibility |
| **CargoSmart** | Yes | Via CMA CGM group |
| **Terminal49** | Yes | Via CMA CGM (CMDU SCAC) |

> **Aggregator note**: ANL shipments are accessible through the same aggregators as CMA CGM. For tracking-only use cases, aggregators like project44 or Vizion offer a simpler integration path than CMA CGM's dual-auth direct API. Aggregators may not expose private-tier data (inland events, GPS, proof of delivery).

---

## Data Quality & Operational Notes

Same as CMA CGM. See `docs/carriers/cma-cgm/api-inventory.md` for details.

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown -- not published by CMA CGM | Unknown |
| **API uptime/reliability** | No public status page or SLA | Unknown |
| **Historical data depth** | Unknown | Unknown |
| **Timezone handling** | Expected ISO 8601 with timezone per DCSA spec | Estimated (DCSA spec) |
| **Character encoding** | Expected UTF-8 per DCSA spec | Estimated (DCSA spec) |

### Known Issues & Gotchas

All CMA CGM gotchas apply to ANL shipments. Key ones:

- **5-minute OAuth2 token lifetime (299 seconds)**: Aggressive token refresh required. Cache tokens and refresh proactively at ~200 seconds.

- **Dual auth with different data visibility**: Public (API Key) and Private (OAuth2) tiers return different event sets for the same shipment. The adapter must handle both tiers gracefully.

- **DCSA subscription endpoints not implemented**: Webhooks are proprietary, not DCSA standard.

- **Proprietary location codes for Routing Finder**: Requires CMA CGM-specific location codification from Location Referential API, not standard UN/LOCODEs.

- **Chargeable API calls**: CMA CGM charges for successful responses and 400 errors. Input validation must be thorough to avoid paying for malformed requests.

- **CMA CGM group multi-carrier responses**: Events may include data from CMA CGM (CMDU), APL (APLU), ANL (ANNU), CNC. The adapter must correctly attribute events to the originating carrier SCAC.

- **ANL SCAC attribution**: When tracking ANL shipments through the CMA CGM API, ensure the adapter correctly maps the ANNU SCAC code. Responses may use CMA CGM group identifiers rather than carrier-specific SCACs.

### Recently Deprecated or Changed

Same as CMA CGM:
- Track & Trace v1.2.7 (02/21/2025): Added ERT (Empty Return Reference) and LOAD reference types
- Shipping Instruction API v2.5.1 (02/04/2026): New version with multi-carrier group support

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | Yes -- ANL uses CMA CGM's API infrastructure, which is comprehensively documented and DCSA-aligned for tracking |
| **Implementation effort** | Low -- reuse the CMA CGM adapter with SCAC configuration. No ANL-specific API differences |
| **DCSA base adapter usable?** | Yes with overrides -- same as CMA CGM (DCSA base for tracking, proprietary overrides for webhooks, auth, cutoffs) |

### Recommended Approach

**ANL should NOT have a separate adapter.** The CMA CGM adapter should handle ANL shipments as a carrier alias / SCAC configuration. The recommended architecture:

1. **Single CMA CGM Group adapter** that accepts SCAC codes CMDU, APLU, ANNU (and CNC) as carrier identifiers. The adapter routes all requests to the same CMA CGM API endpoints regardless of which group carrier's shipment is being tracked.

2. **SCAC-based carrier resolution**: When the SDK receives a tracking request for SCAC "ANNU", the carrier adapter registry should resolve it to the CMA CGM Group adapter. No code duplication needed.

3. **Same auth, same endpoints, same data model**: Since ANL shipments flow through identical API infrastructure, the adapter implementation is a configuration-level concern, not a code-level one. Register ANNU as an alias in the carrier registry pointing to the CMA CGM adapter.

This approach avoids maintaining duplicate adapters and ensures ANL inherits all CMA CGM adapter improvements automatically.

### Recommended Lookup Method

Same as CMA CGM: **Bill of Lading (B/L) number** as primary, **booking reference** as secondary, **container number** as supplementary. The Track & Trace API accepts standard document references for any CMA CGM group carrier.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Every 4-6 hours for active shipments (same as CMA CGM -- chargeable API calls require cost awareness) |
| **Incremental filter** | Use DCSA timestamp filtering on `GET /events` |
| **Batch tracking** | One API call per shipment. Use webhooks to minimize polling volume and costs |

### Auth Implementation Notes

Identical to CMA CGM. Same credentials work for ANL shipments:

```
OAuth2 (Private APIs):
  POST https://auth.cma-cgm.com/as/token.oauth2
  Body: grant_type=client_credentials&client_id={id}&client_secret={secret}&scope={scope}
  Token lifetime: 299 seconds

API Key (Public APIs):
  Header: KeyId: <API_Key_Value>
```

No ANL-specific authentication is needed. CMA CGM credentials cover all group carriers.

### Edge Cases to Handle

- **SCAC code mapping**: SDK must map ANNU to the CMA CGM adapter. Consider also handling lookups where the user knows the carrier as "ANL" but the API returns events tagged with CMA CGM group identifiers.

- **Carrier name in responses**: CMA CGM API responses may reference the operating carrier as "ANL", "CMA CGM", or use SCAC codes interchangeably. The adapter should normalize carrier attribution in the response.

- **ANL-specific trade lanes**: ANL primarily operates Oceania/Pacific routes. Schedule queries for ANL services should work through CMA CGM's schedule APIs, but results may include the full CMA CGM group network. Filter by service/route if ANL-specific schedules are needed.

### Mapping Complexity

**Low complexity.** ANL uses identical API infrastructure to CMA CGM. There is zero additional mapping work beyond the CMA CGM adapter. The only "mapping" required is at the carrier registry level: SCAC "ANNU" resolves to the CMA CGM Group adapter.

---

## Open Questions

- [ ] **Does SSL already have CMA CGM API portal access?** -- If yes, ANL tracking works immediately with no additional setup
- [ ] **Do ANL shipment events explicitly identify ANNU as the carrier SCAC, or do they use CMDU?** -- Affects how the adapter attributes events to the correct carrier
- [ ] **Are there ANL-specific services/routes in the CMA CGM schedule APIs?** -- Need to verify ANL service identifiers for schedule filtering
- [ ] **Same open questions as CMA CGM** -- see `docs/carriers/cma-cgm/api-inventory.md` Open Questions section

---

## Source Links

| Resource | URL |
|----------|-----|
| ANL Website | https://www.anl.com.au |
| ANL EDI/API Solutions | https://www.anl.com.au/products-services/ecommerce/edi-api-channels |
| ANL Tracking Portal | https://www.anl.com.au/ebusiness/tracking |
| ANL Schedules | https://www.anl.com.au/products-services/line-services/schedules |
| CMA CGM API Portal | https://api-portal.cma-cgm.com |
| CMA CGM API Usage Guide | https://api-portal.cma-cgm.com/usage-guide |
| CMA CGM EDI/API Solutions | https://www.cma-cgm.com/products-services/ecommerce/edi-api-channels |
| CMA CGM Tracking Portal | https://www.cma-cgm.com/ebusiness/tracking |
| OAuth2 Token Endpoint | https://auth.cma-cgm.com/as/token.oauth2 |
| API Base URL (Production) | https://apis.cma-cgm.net |
| project44 ANL Tracking | https://www.project44.com/tracking/container/anl/ |
| Fluent Cargo ANL (SCAC: ANNU) | https://www.fluentcargo.com/carriers/scac/ANNU |
| DCSA Members | https://dcsa.org/about-us-our-work-and-what-we-do-dcsa/members/ |
| CMA CGM API Inventory (parent) | `docs/carriers/cma-cgm/api-inventory.md` |
