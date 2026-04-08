# American President Lines (APL) — API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only — not verified with live API testing. Research based on APL's public web presence (apl.com), CMA CGM API portal documentation (api-portal.cma-cgm.com), CMA CGM group carrier coverage statements, Wikipedia, industry news sources, and third-party aggregator listings. No API credentials were obtained or used.
> **Researched by**: Agent (carrier API audit workflow)
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | American President Lines, LLC (APL) |
| **SCAC Code** | APLU |
| **Parent Company** | CMA CGM Group (acquired NOL/APL in 2016) |
| **Alliance** | Ocean Alliance (via CMA CGM, alongside COSCO, Evergreen, OOCL) |
| **Primary Services** | Container shipping — since October 2020, focused exclusively on U.S. Government and military logistics plus Guam-Pacific trade. Commercial transpacific operations transferred to CMA CGM brand |
| **Market Position** | Niche operator — U.S. Government logistics specialist. Second-largest carrier of U.S. Department of Defense cargo. Operates eleven U.S.-flagged container vessels across five weekly services linking North America to Asia, the Mediterranean, Africa, the Middle East, and Guam |
| **Headquarters** | Scottsdale, Arizona, United States |
| **Website** | https://www.apl.com |

### APL's Position Within the CMA CGM Group

APL became a subsidiary of CMA CGM in June 2016 when CMA CGM acquired over 90% of NOL (Neptune Orient Lines) stock. In October 2020, CMA CGM reorganized its transpacific network:

- **CMA CGM** became the sole commercial carrier brand for transpacific trade
- **APL** refocused exclusively on U.S. Government and military cargo, plus Guam-Pacific trade
- **ANL** serves Oceania trade
- **CNC** operates as the intra-Asia shortsea specialist

This effectively ended APL's 170+ year legacy as a commercial transpacific carrier. Today, APL operates under the CMA CGM Group's digital infrastructure, including shared API systems.

### Key Implication for SDK Development

APL shipments are trackable through CMA CGM's API portal (api-portal.cma-cgm.com). CMA CGM's APIs explicitly state they cover "all carriers of the CMA CGM group," including APL (APLU), ANL, and CNC. APL does not maintain a separate, independent developer API portal. The apl.com website's EDI/API Solutions page describes creating "efficient connections between your system and CMA CGM's" and references the same API infrastructure.

**From an SDK perspective, APL does not need a separate adapter. The CMA CGM adapter (CMDU) handles APLU tracking.**

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | No (independent) — APL uses CMA CGM's API portal |
| **Developer portal URL** | https://api-portal.cma-cgm.com (shared with CMA CGM) |
| **API documentation URL(s)** | https://api-portal.cma-cgm.com (same as CMA CGM); APL's own EDI/API page at https://www.apl.com/products-services/ecommerce/edi-api-channels references CMA CGM infrastructure |
| **Documentation quality** | Good — via CMA CGM's portal (DCSA-standard APIs with Swagger specs). APL-specific documentation is minimal; the apl.com EDI/API pages redirect conceptually to CMA CGM's infrastructure |
| **OpenAPI/Swagger spec available?** | Yes — via CMA CGM portal (requires login). DCSA standard specs also at https://github.com/dcsaorg/DCSA-OpenAPI |
| **Sandbox/test environment?** | No — same as CMA CGM (free trial provides 1 month of production access) |
| **Developer registration** | Requires approval through CMA CGM's portal — register for free trial, API key delivered within 2-3 days (public APIs) or approximately 1 week (private APIs) |
| **Developer support channels** | Via CMA CGM: business requests at https://api-portal.cma-cgm.com/contact-us/business-request; APL customer service channels for government cargo inquiries |
| **Community/third-party libraries** | None specific to APL. Minimal CMA CGM libraries — Python multi-carrier library at https://github.com/dhruvkar/tracktrace lists CMA CGM (CMDU) support (possibly scraping-based) |
| **API changelog / release notes** | Via CMA CGM portal — release notes on API detail pages (e.g., Track & Trace v1.2.7, 02/21/2025) |

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | No — APL is not a DCSA member in its own right. CMA CGM (the parent) is a founding DCSA member (April 2019). APL shipments are covered by CMA CGM's DCSA-compliant APIs |
| **DCSA APIs implemented** | Via CMA CGM: TNT (Track & Trace), CS (Commercial Schedules — PILOT) |
| **DCSA TNT version** | Via CMA CGM: v2.2.0 (API version on portal: v1.2.7, 02/21/2025) |
| **DCSA Booking version** | N/A — CMA CGM uses proprietary Booking Request API (not DCSA-aligned) |
| **DCSA Schedules version** | Via CMA CGM: v1.0.7 (PILOT status, dated 02/18/2024) |
| **Known DCSA deviations** | Same as CMA CGM: Shipment events and subscription management not covered by the DCSA Track & Trace API. Webhooks are proprietary, not DCSA subscription model |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Yes | Via CMA CGM group: IFTMBF (Booking), IFTMIN (Shipping instructions), IFTSTA (Tracking/container status), IFTMCS (Bill of Lading), IFTSAI (Schedules), VERMAS (VGM). APL's EDI page at apl.com lists EDI capabilities. EDI implementation typically takes at least 3 months |
| **INTTRA integration** | Yes | Via CMA CGM — booking, schedules, rates, visibility/tracking (reported) |
| **BIC (Bureau International des Containers)** | Yes | Standard container ID format. APL container prefix: APLU |
| **UN/LOCODE** | Yes | Used in DCSA-compliant endpoints via CMA CGM |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | Dual (via CMA CGM): API Key (public APIs) + OAuth2 Client Credentials (private APIs) |
| **Auth documentation** | https://api-portal.cma-cgm.com/usage-guide |
| **Registration process** | Same as CMA CGM: 1. Register at api-portal.cma-cgm.com 2. Account activated (2-3 days for public, ~1 week for private) 3. Free trial (1 month production access) 4. Subscription for continued access |
| **Registration URL** | https://api-portal.cma-cgm.com |
| **Partner program required?** | No for public APIs (API key). Private APIs require being identified on booking as Booking Party, Deciding Party, Consignee, Notifier, or Shipper |
| **Partner program URL** | N/A |
| **Credential type** | API Key (header: `KeyId: <API_Key_Value>`) for public APIs; Client ID + Client Secret (OAuth2 `client_credentials`) for private APIs |
| **Token refresh supported?** | Yes — re-request via OAuth2 client_credentials flow |
| **Token lifetime** | 299 seconds (~5 minutes) for OAuth2 tokens (Official — from CMA CGM usage guide) |
| **Access tiers** | Public (API Key — standard events), Private (OAuth2 — additional inland/GPS events), Free Trial (1 month), Subscription (paid, some calls chargeable) |
| **IP whitelisting required?** | Unknown |

### Authentication Details

**API Key (Public APIs):**
```
Header: KeyId: <API_Key_Value>
```

**OAuth2 Client Credentials (Private APIs):**
```
POST https://auth.cma-cgm.com/as/token.oauth2
Content-Type: application/x-www-form-urlencoded
Body: grant_type=client_credentials&client_id={id}&client_secret={secret}&scope={scope}
Response: {"access_token":"...","token_type":"Bearer","expires_in":299}
Usage: Authorization: Bearer {access_token}
```

**CORS:** Not supported. Server-to-server integration only.

### Access Requirements Summary for SSL

APL shipments are accessed through CMA CGM's API infrastructure. SSL does not need a separate APL registration or partnership — the same CMA CGM API credentials that track CMDU shipments will also track APLU shipments. CMA CGM's APIs explicitly cover "all carriers of the CMA CGM group."

If SSL already has or obtains CMA CGM API access (see the CMA CGM inventory), APL tracking is included automatically. No additional onboarding or credentials are required for APL-specific shipments. The CMA CGM adapter simply needs to accept APLU as a valid SCAC code alongside CMDU.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field has a row.
> All coverage is via CMA CGM's API infrastructure. Ratings match the CMA CGM inventory exactly.
> ✅ = Available | ❌ = Not available | ⚠️ = Partial / limited | ❓ = Unknown

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ✅ | `GET /v1/port-schedules`, `GET /v1/vessel-schedules` (DCSA CS PILOT); Proprietary: Voyages API, Lines & Services API | Vessel rotations, port calls, ETAs/ETDs | DCSA CS v1 | Via CMA CGM. DCSA endpoints in PILOT status. Routing Finder covers all CMA CGM group carriers including APL |
| 1.2 | Point-to-Point Route Options | ✅ | `GET /v1/point-to-point-routes` (DCSA CS PILOT); Proprietary: Routing Finder API v2.9.7 | Route options with legs, transit times | DCSA CS v1 | Via CMA CGM. Routing Finder explicitly covers all group carriers |
| 1.3 | Booking Lifecycle | ✅ | CMA CGM Booking Request API v1.10.0 (proprietary); Shipment API v3.14.2 | Submit, update, cancel bookings | **Not DCSA** — proprietary | Via CMA CGM. Supports dry, reefer, hazardous, SOC, multi-container, inland transport |
| 1.4 | Shipping Instructions | ✅ | CMA CGM Shipping Instruction API v2.5.1 (proprietary) | Create/update shipping instructions | **Not DCSA** — proprietary | Via CMA CGM. v2.5.1 explicitly supports all CMA CGM group carriers |
| 1.5 | Rates | ❓ | Pricing category visible on CMA CGM portal but requires login | Unknown | **Not DCSA** | Via CMA CGM. Pricing API exists but details not accessible without subscription |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❓ | Unknown — not explicitly documented in CMA CGM materials | Unknown | `ECP` | Via CMA CGM. May be in Routing Finder or Booking response. Requires live testing |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❓ | Unknown — not explicitly documented | Unknown | `EFC` | Via CMA CGM. May be in Routing Finder or Booking response |
| 2.3 | Documentation Cutoff | DCO | ⚠️ | CMA CGM Routing Finder API v2.9.7 (lists "SI cutoffs") | SI cutoff in Routing Finder response | `DCO` | Via CMA CGM. Partial confidence without live verification |
| 2.4 | VGM Cutoff | VCO | ⚠️ | CMA CGM Routing Finder API v2.9.7 (lists "VGM cutoffs") | VGM cutoff in Routing Finder response | `VCO` | Via CMA CGM. Partial confidence without live verification |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ⚠️ | CMA CGM Routing Finder API v2.9.7 (lists "Port cutoffs") | Port cutoff in Routing Finder response | `FCO` | Via CMA CGM. Routing Finder mentions "Port cutoffs" |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❓ | Unknown — not explicitly mentioned in CMA CGM documentation | Unknown | `LCO` | Via CMA CGM. No explicit LCL cutoff reference found |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ⚠️ | CMA CGM `GET /events` (TNT v2.2.0) | Inferred from first EquipmentEvent | Inferred from first EquipmentEvent | Via CMA CGM. No explicit "assigned" event |
| 3.2 | Empty Container Gate-Out (Pickup) | ✅ | CMA CGM `GET /events` | `GTOT` + `EMPTY` | `GTOT` + `EMPTY` | Via CMA CGM. Public visibility |
| 3.3 | Full Container Gate-In | ✅ | CMA CGM `GET /events` | `GTIN` + `LADEN` | `GTIN` + `LADEN` | Via CMA CGM. Public visibility |
| 3.4 | Container Loaded on Vessel | ✅ | CMA CGM `GET /events` | `LOAD` + `LADEN` | `LOAD` + `LADEN` | Via CMA CGM. Public visibility |
| 3.5 | Container Discharged at Transshipment | ✅ | CMA CGM `GET /events` | `DISC` + `LADEN` at transshipment | `DISC` + `LADEN` + transshipment | Via CMA CGM. Explicitly listed |
| 3.6 | Container Loaded at Transshipment | ✅ | CMA CGM `GET /events` | `LOAD` + `LADEN` at transshipment port | `LOAD` + `LADEN` + transshipment | Via CMA CGM. Inferred from location context |
| 3.7 | Container Discharged at Destination | ✅ | CMA CGM `GET /events` | `DISC` + `LADEN` | `DISC` + `LADEN` | Via CMA CGM. Public visibility |
| 3.8 | Full Container Gate-Out (Delivery) | ✅ | CMA CGM `GET /events` | `GTOT` + `LADEN` | `GTOT` + `LADEN` | Via CMA CGM. Public visibility |
| 3.9 | Empty Container Returned | ✅ | CMA CGM `GET /events` | `GTIN` + `EMPTY` | `GTIN` + `EMPTY` | Via CMA CGM. ERT reference type added in v1.2.7 |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ✅ | CMA CGM `GET /events`; Schedules APIs | `DEPA` with PLN/EST/ACT classifiers | `DEPA` + classifier | Via CMA CGM. Full classifier progression |
| 4.2 | Estimated Time of Arrival | ETA | ✅ | CMA CGM `GET /events`; Schedules APIs | `ARRI` with PLN/EST/ACT classifiers | `ARRI` + classifier | Via CMA CGM. Full classifier progression |
| 4.3 | Vessel Arrival at Transshipment | -- | ✅ | CMA CGM `GET /events` | `ARRI` at intermediate transshipment port | `ARRI` at intermediate | Via CMA CGM |
| 4.4 | Vessel Departure from Transshipment | -- | ✅ | CMA CGM `GET /events` | `DEPA` at intermediate transshipment port | `DEPA` at intermediate | Via CMA CGM |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ✅ (proprietary) | Via CMA CGM's proprietary event push system (NOT DCSA subscription model). Equipment, Shipment, Transport, Schedules, Shipment Release, and Pricing event categories |
| Event Polling with timestamp filter | ✅ | Via CMA CGM DCSA TNT v2.2.0 `GET /events` endpoint. Cursor-based pagination |
| Event Classifier Progression (PLN->EST->ACT) | ✅ | DCSA-standard classifier codes supported for transport events via CMA CGM |
| Retracted Events | ❓ | Unknown — not explicitly documented in CMA CGM materials. DCSA TNT v2.2.0 spec supports it but implementation unconfirmed |
| Change Remarks | ❓ | Unknown — DCSA TNT v2.2.0 spec includes `changeRemark` but CMA CGM implementation unconfirmed |
| Delay Reason Codes | ❓ | Unknown — DCSA TNT v2.2.0 spec includes `delayReasonCode` but CMA CGM implementation unconfirmed |

### Coverage Summary

| Category | Fields Available | Fields Partial | Fields Unavailable | Fields Unknown | Coverage % |
|----------|-----------------|---------------|-------------------|----------------|-----------|
| API Domains (1.x) | 4/5 | 0/5 | 0/5 | 1/5 | 80% |
| Cutoffs (2.x) | 0/6 | 3/6 | 0/6 | 3/6 | 0% confirmed (3 partial) |
| Container Milestones (3.x) | 8/9 | 1/9 | 0/9 | 0/9 | 89% (1 partial) |
| Transport Events (4.x) | 4/4 | 0/4 | 0/4 | 0/4 | 100% |
| Change Detection (5.x) | 3/6 | 0/6 | 0/6 | 3/6 | 50% |
| **Total** | **19/30** | **4/30** | **0/30** | **7/30** | **63% confirmed (13% partial)** |

> **Notes on Coverage:**
> - All coverage is inherited from CMA CGM's API infrastructure. APL (APLU) shipments are trackable through the same endpoints and return the same data structures as CMA CGM (CMDU) shipments.
> - Coverage percentages are identical to the CMA CGM inventory because the underlying API is the same.
> - The same unknowns and caveats from the CMA CGM inventory apply: cutoffs are the biggest gap in confirmed coverage, retracted events/change remarks/delay reason codes are unconfirmed.
> - Government cargo may have additional data restrictions or access requirements not reflected here.

---

## Endpoint Reference

APL uses CMA CGM's endpoints identically. See the [CMA CGM API Inventory](../cma-cgm/api-inventory.md) for the complete endpoint reference. Key endpoints are summarized below.

### Tracking / Events

| Endpoint | Method | Lookup Params | Pagination | Response Format | Notes |
|----------|--------|--------------|------------|----------------|-------|
| `GET /events` (unique tracking reference) | GET | B/L, booking ref, or container number | DCSA cursor-based: `limit` + page headers | JSON (DCSA TNT v2.2.0) | `getMoveOnCommercialCycle` — works for APLU containers/B/Ls. Mixed auth: OAuth2 + ApiKey |
| `GET /events` (search) | GET | Broader search parameters | Same DCSA cursor-based pagination | JSON (DCSA TNT v2.2.0) | `searchMoveOnCommercialCycle`. Mixed auth: OAuth2 + ApiKey |

### Schedules

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| `GET /v1/point-to-point-routes` | GET | Origin, destination, date range | DCSA cursor-based | JSON (DCSA CS v1) | PILOT status. Covers all CMA CGM group carriers |
| `GET /v1/port-schedules` | GET | Port (UNLocationCode), starting date | DCSA cursor-based | JSON (DCSA CS v1) | PILOT status |
| `GET /v1/vessel-schedules` | GET | Service, voyage, vessel, location | DCSA cursor-based | JSON (DCSA CS v1) | PILOT status |
| Routing Finder (proprietary) | GET | CMA CGM location codes | Proprietary range-based (HTTP 206) | JSON (proprietary) | v2.9.7. Covers all group carriers including APL |

### Booking

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| Booking Request API (proprietary) | POST/PUT/DELETE | Booking reference, cargo details | Proprietary range-based | JSON (proprietary) | v1.10.0. Via CMA CGM |
| Shipment API | GET | Shipment/booking reference | Proprietary range-based | JSON (proprietary) | v3.14.2. Via CMA CGM |

### Lookup Methods Summary

| Identifier Type | Supported? | Which Endpoints? | Notes |
|----------------|-----------|-----------------|-------|
| **Bill of Lading (B/L) number** | ✅ | Track & Trace `GET /events`, Shipment API | APL B/L numbers trackable through CMA CGM API |
| **Booking reference** | ✅ | Track & Trace `GET /events`, Shipment API, Booking Request API | Works for APL bookings |
| **Container number** | ✅ | Track & Trace `GET /events` | APLU-prefixed containers trackable |
| **Carrier booking number** | ✅ | Same as booking reference | Used interchangeably |
| **Vessel IMO / voyage** | ✅ | Schedules APIs | Covers APL vessel services |

---

## Rate Limits & Quotas

Identical to CMA CGM — see the [CMA CGM API Inventory](../cma-cgm/api-inventory.md) for full details.

| Detail | Value | Source |
|--------|-------|--------|
| **Global rate limit** | Yes — per-application limits. Specific numbers unpublished | Official (CMA CGM) |
| **Per-endpoint limits** | Unpublished — contact CMA CGM for higher limits | Official (CMA CGM) |
| **Daily/monthly quota** | Unpublished | Unknown |
| **Rate limit response** | HTTP 429 with `retry-after` header (e.g., 3600 seconds) | Official (CMA CGM) |
| **Rate limit by** | Per-application (API key / OAuth token) | Official (CMA CGM) |
| **Burst allowance** | Unknown | Unknown |
| **Different tiers** | Some API calls are chargeable (200, 201, 204, 206, 400 responses billed) | Official (CMA CGM) |

---

## Webhook / Push Support

Identical to CMA CGM — see the [CMA CGM API Inventory](../cma-cgm/api-inventory.md) for full details.

| Detail | Value |
|--------|-------|
| **Webhooks supported?** | Yes — via CMA CGM's proprietary event push system (NOT DCSA subscription model) |
| **Subscription endpoint** | Proprietary — via CMA CGM portal |
| **Subscription management** | Proprietary subscription management (via CMA CGM portal) |
| **Subscribable event types** | Equipment events, Shipment events, Transport events, Schedules events, Shipment Release events, Pricing events |
| **Callback format** | Events POSTed to customer-provided webhook URL (proprietary format) |
| **Callback authentication** | CMA CGM supports API Key or OAuth2 to customer's webhook. OAuth2 recommended |
| **Retry policy on failure** | Configurable: maximum event age (default 24h), retry frequency (linear or exponential). 5XX retried; 4XX not retried |
| **Documented reliability** | No published SLA. Default 24h maximum event age |

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | https://www.apl.com/ebusiness/tracking (APL-branded portal; also trackable via https://www.cma-cgm.com/ebusiness/tracking) |
| **Login required?** | No — basic tracking without login. Registered users get map view and notifications |
| **Data available on portal but NOT in API** | Map visualization of container position at sea (portal-only rendering). Functional data should match API |
| **Scraping feasibility** | Not assessed — API coverage via CMA CGM should be sufficient |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Yes |
| **EDI message types** | IFTMBF (Booking), IFTMIN (Shipping instructions), IFTSTA (Tracking/container status), IFTMCS (Bill of Lading), IFTSAI (Schedules), VERMAS (VGM) |
| **EDI connection method** | Via CMA CGM — implementation takes at least 3 months |
| **EDI documentation** | https://www.apl.com/products-services/ecommerce/edi-api-channels/EDI-catalog (APL-branded); https://www.cma-cgm.com/products-services/ecommerce/edi-api-channels/EDI-catalog (CMA CGM) |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Yes | APL/APLU covered via CMA CGM group support |
| **FourKites** | Yes | Ocean visibility coverage (reported via CMA CGM group) |
| **Vizion** | Yes | Container tracking via API; supports B/L, booking, container lookup. Vizion covers 99% of ocean freight including APL |
| **INTTRA / E2open** | Yes | Via CMA CGM — booking, schedules, rates, visibility/tracking |
| **CargoSmart** | Yes | Schedule and tracking visibility (reported) |
| **Terminal49** | Yes | Container tracking (APLU SCAC explicitly listed). See https://terminal49.com/shipping-lines/aplu-american-president-lines-container-tracking |

> **Aggregator note:** Since APL shipments are fully trackable through CMA CGM's API, there is no advantage to using a third-party aggregator specifically for APL that wouldn't also apply to CMA CGM. If SSL is already integrating directly with CMA CGM, APL coverage is included at no additional effort.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown — not published by CMA CGM. Private-tier events (GPS) suggest near-real-time for some data | Unknown |
| **API uptime/reliability** | No public status page or published SLA from CMA CGM | Unknown |
| **Historical data depth** | Unknown — not documented in CMA CGM materials | Unknown |
| **Timezone handling** | Expected ISO 8601 with timezone per DCSA specification for TNT endpoints | Estimated (DCSA spec) |
| **Character encoding** | Expected UTF-8 per DCSA specification | Estimated (DCSA spec) |

### Known Issues & Gotchas

- **APL is not a separate integration target**: The most important architectural insight is that APL (APLU) does not require a separate adapter, auth flow, or registration. It is entirely served by CMA CGM's API. The SDK should map APLU SCAC to the CMA CGM adapter.

- **Government cargo data access**: APL specializes in U.S. Government and military cargo. Government shipments may have additional data restrictions, classification requirements, or access limitations not reflected in the standard CMA CGM API documentation. SSL should verify whether government cargo tracking behaves identically to commercial cargo tracking through the API.

- **APL-branded web portal vs. API**: The apl.com tracking portal (https://www.apl.com/ebusiness/tracking) provides APL-branded tracking, but the underlying data comes from CMA CGM's systems. There may be minor presentation differences between the APL portal and CMA CGM portal, but the API data should be identical.

- **SCAC code handling**: Events returned by CMA CGM's API for APL shipments may use the APLU SCAC code. The adapter should handle multi-SCAC responses within the CMA CGM group (CMDU, CMDA, CACM, CMAU, APLU, and others).

- **All CMA CGM gotchas apply**: The 5-minute OAuth2 token lifetime, dual auth model, chargeable API calls, proprietary location codes for Routing Finder, two pagination systems, and no sandbox — all issues documented in the CMA CGM inventory apply equally to APL shipments tracked through the same infrastructure.

### Recently Deprecated or Changed

- **October 2020 brand transition**: APL's commercial transpacific services were absorbed into the CMA CGM brand. Legacy APL bookings and shipment references from before this transition may exist in historical data. The API should still resolve them, but the event history may show a carrier brand transition.

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | No separate adapter needed — use the CMA CGM adapter. APL (APLU) shipments are fully served by CMA CGM's API with no additional endpoints or deviations |
| **Implementation effort** | Negligible (SCAC mapping only) — add APLU as an alias for the CMA CGM adapter in the carrier registry |
| **DCSA base adapter usable?** | Yes — same as CMA CGM (DCSA base with overrides for webhooks, cutoffs, auth) |

### Recommended Approach

**APL does not need a separate SDK adapter.** The recommended approach is:

1. **SCAC Alias in Carrier Registry**: Register APLU as an alias for the CMA CGM (CMDU) adapter in the `CarrierAdapterRegistry`. When a consumer requests tracking for APLU, the registry returns the CMA CGM adapter instance.

2. **No Code Duplication**: All endpoint URLs, auth flows, event parsing, pagination handling, and normalization logic are identical to CMA CGM. There is no APL-specific API behavior to implement.

3. **SCAC-Aware Event Attribution**: The CMA CGM adapter should already handle multi-SCAC responses (it returns data for CMDU, APLU, ANL, CNC). Ensure the adapter correctly attributes events to the requesting SCAC code when returning results to the consumer.

4. **CarrierCapabilities**: The `getCarrierCapabilities()` response for APLU should return the same capabilities as CMDU, possibly with a note indicating it is served via CMA CGM's infrastructure.

This is the same pattern that would apply to other CMA CGM subsidiaries (ANL, CNC) — they are all aliases for the CMA CGM adapter.

### Recommended Lookup Method

Same as CMA CGM: **Bill of Lading (B/L) number** as primary, **Booking reference** as secondary, **Container number** as supplementary. APLU-prefixed container numbers work through the standard CMA CGM tracking endpoint.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Same as CMA CGM: Every 4-6 hours for active shipments (chargeable API calls). Every 12-24 hours for pre-departure. Webhook-first strategy recommended |
| **Incremental filter** | Use DCSA timestamp filtering on `GET /events` (via CMA CGM) |
| **Batch tracking** | One API call per shipment. No batch endpoint. Use webhooks to minimize costs |

### Auth Implementation Notes

No additional auth implementation needed. The CMA CGM adapter's dual-auth handler (API Key for public + OAuth2 for private) works for APL shipments without modification.

### Edge Cases to Handle

- **SCAC code routing**: Ensure the carrier registry correctly maps APLU to the CMA CGM adapter. This is the only APL-specific implementation task.
- **Government cargo visibility**: APL's U.S. Government shipments may have limited API visibility. The adapter should handle cases where tracking requests for APLU shipments return empty or restricted results.
- **Historical data**: Pre-October 2020 APL shipments may have different data characteristics. The adapter should not make assumptions about APL-specific service patterns.

### Mapping Complexity

**Negligible.** There is no APL-specific mapping. All events use CMA CGM's DCSA TNT v2.2.0 format, the same equipment/transport event codes, and the same response structures. The CMA CGM adapter's existing normalization logic handles APLU shipments without modification.

---

## Open Questions

- [ ] **Does SSL handle any U.S. Government cargo that would use APL specifically?** — If all SSL cargo is commercial, APL's government-focused services may be irrelevant. If SSL does handle government cargo, verify whether API access differs for government-contracted shipments.
- [ ] **Does CMA CGM's API return APLU SCAC codes in event responses for APL shipments?** — Need to verify whether the adapter sees APLU in response data or whether CMA CGM normalizes everything to CMDU.
- [ ] **Are there APL-specific EDI message formats or identifiers?** — While API access is shared, EDI connections may have APL-specific routing or formatting requirements.
- [ ] **Does SSL already have CMA CGM API access?** — If so, APL coverage is already available with no additional work.

---

## Source Links

| Resource | URL |
|----------|-----|
| APL Website | https://www.apl.com |
| APL EDI/API Solutions | https://www.apl.com/products-services/ecommerce/edi-api-channels |
| APL Tracking Portal | https://www.apl.com/ebusiness/tracking |
| APL EDI Catalog | https://www.apl.com/products-services/ecommerce/edi-api-channels/EDI-catalog |
| APL + CMA CGM Services Page | https://www.apl.com/cma-cgm |
| APL Company Overview | https://www.apl.com/about-us/company-overview |
| APL Maritime Services (Gov) | https://www.apl.com/shipping/maritime-services |
| CMA CGM API Portal | https://api-portal.cma-cgm.com |
| CMA CGM API Usage Guide | https://api-portal.cma-cgm.com/usage-guide |
| CMA CGM Tracking Portal | https://www.cma-cgm.com/ebusiness/tracking |
| CMA CGM EDI/API Catalog | https://www.cma-cgm.com/products-services/ecommerce/edi-api-channels |
| CMA CGM Brand Simplification (2020) | https://www.seatrade-maritime.com/containers/cma-cgm-drops-apl-brand-in-transpacific-trade |
| APL Wikipedia | https://en.wikipedia.org/wiki/American_President_Lines |
| Terminal49 APL Tracking | https://terminal49.com/shipping-lines/aplu-american-president-lines-container-tracking |
| DCSA Members Page | https://dcsa.org/about-us-our-work-and-what-we-do-dcsa/members/ |
| DCSA OpenAPI Specs (GitHub) | https://github.com/dcsaorg/DCSA-OpenAPI |
