# CMA CGM — API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only — not verified with live API testing
> **Researched by**: Agent
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | CMA CGM S.A. (commonly "CMA CGM") |
| **SCAC Code** | CMDU (also: CMDA, CACM, CMAU accepted by some third-party services) |
| **Parent Company** | CMA CGM Group (privately held, Rodolphe Saade family) |
| **Alliance** | Ocean Alliance (with COSCO Shipping, Evergreen, OOCL) — extended until 2032 |
| **Primary Services** | Container shipping, logistics, inland transport. Group includes APL (APLU), ANL, CNC |
| **Market Position** | Third-largest container shipping line globally |
| **Headquarters** | Marseille, France |
| **Website** | https://www.cma-cgm.com |

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | Yes |
| **Developer portal URL** | https://api-portal.cma-cgm.com |
| **API documentation URL(s)** | https://api-portal.cma-cgm.com (SPA — catalog browsable without login; Swagger specs and product details require registration) |
| **Documentation quality** | Good — DCSA-standard APIs have detailed descriptions, event tables, and Swagger tabs; proprietary APIs have briefer descriptions |
| **OpenAPI/Swagger spec available?** | Yes — Swagger tab on API detail pages (requires login). DCSA standard specs also at https://github.com/dcsaorg/DCSA-OpenAPI |
| **Sandbox/test environment?** | No dedicated sandbox. Free trial provides 1 month of direct production access with limited data collection |
| **Developer registration** | Requires approval — register for free trial, API key delivered within 2-3 days (public APIs) or ~1 week (private APIs) |
| **Developer support channels** | Business requests via https://api-portal.cma-cgm.com/contact-us/business-request; customer service at https://mycustomerservice.cma-cgm.com/s/selfcare/article/API-Solution?language=en_US |
| **Community/third-party libraries** | Minimal — no dedicated CMA CGM client libraries on npm or PyPI. Python multi-carrier library at https://github.com/dhruvkar/tracktrace lists CMA CGM (CMDU) support (possibly scraping-based) |
| **API changelog / release notes** | Yes — release notes shown on API detail pages (e.g., Track & Trace v1.2.7, 02/21/2025) |
| **API status page** | Not found publicly |

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | Yes — founding member (April 2019) |
| **DCSA APIs implemented** | TNT (Track & Trace), CS (Commercial Schedules — PILOT) |
| **DCSA TNT version** | v2.2.0 (references DCSA Information Model v3.3). API version on portal: v1.2.7 (02/21/2025) |
| **DCSA Booking version** | N/A — proprietary Booking Request API (v1.10.0); DCSA standard alignment "Scheduled for future releases" |
| **DCSA Schedules version** | v1.0.7 (PILOT status, dated 02/18/2024) |
| **Known DCSA deviations** | Shipment events and subscription management are NOT covered by the DCSA Track & Trace API. CMA CGM explicitly states: "shipment events and subscription management are not covered yet." DCSA TNT subscription endpoints (`POST /event-subscriptions`, etc.) are not implemented. CMA CGM offers a separate proprietary event push/webhook system instead |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Yes | IFTMBF (Booking), IFTMIN (Shipping instructions), IFTSTA (Tracking/container status), IFTMCS (Bill of Lading), IFTSAI (Schedules, 12-week horizon), VERMAS (VGM) |
| **INTTRA integration** | Yes | Booking, schedules, rates, visibility/tracking via INTTRA Ocean Execution APIs (reported) |
| **BIC (Bureau International des Containers)** | Yes | Standard container ID format used throughout APIs |
| **UN/LOCODE** | Yes | Used in DCSA-compliant endpoints. CMA CGM also has proprietary location codification available via referential APIs |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | Dual: API Key (public APIs) + OAuth2 Client Credentials (private APIs) |
| **Auth documentation** | https://api-portal.cma-cgm.com/usage-guide |
| **Registration process** | 1. Browse product catalog at https://api-portal.cma-cgm.com 2. Register for free trial 3. Information checked by backend system 4. Account activated with confirmation email + API token 5. Access technical guides and free referential APIs 6. Production access under free trial (1 month) 7. Request subscription for continued access |
| **Registration URL** | https://api-portal.cma-cgm.com |
| **Partner program required?** | No for public APIs (API key). Private APIs require being identified on booking as Booking Party, Deciding Party, Consignee, Notifier, or Shipper |
| **Partner program URL** | N/A |
| **Credential type** | API Key (header: `KeyId: <API_Key_Value>`) for public APIs; Client ID + Client Secret (OAuth2 `client_credentials`) for private APIs |
| **Token refresh supported?** | Yes — re-request via OAuth2 client_credentials flow |
| **Token lifetime** | 299 seconds (~5 minutes) for OAuth2 tokens (Official — from usage guide example: `"expires_in": 299`) |
| **Access tiers** | Public (API Key — standard events), Private (OAuth2 — additional events like inland moves, GPS), Free Trial (1 month production), Subscription (paid, some calls chargeable) |
| **IP whitelisting required?** | Unknown |

### Authentication Details

**API Key (Public APIs):**
```
Header: KeyId: <API_Key_Value>
```
Generated during onboarding, available in portal application data. Rotatable on request. Provides access to standard equipment moves, transshipment moves, and planned vessel departure/arrival dates.

**OAuth2 Client Credentials (Private APIs):**
```
POST https://auth.cma-cgm.com/as/token.oauth2
Content-Type: application/x-www-form-urlencoded
Body: grant_type=client_credentials&client_id={id}&client_secret={secret}&scope={scope}
Response: {"access_token":"...","token_type":"Bearer","expires_in":299}
Usage: Authorization: Bearer {access_token}
```
Each endpoint specifies required scopes (e.g., `imdg:read:be`, `commodity:be`, `charges:read:be`). Provides access to private events: actual rail/ramp moves, planned inland departure/arrival, GPS positions, proof of delivery.

**CORS:** Not supported. Client-side browser calls (Ajax) are not possible. Server-to-server integration only.

### Access Requirements Summary for SSL

CMA CGM requires a registration and approval process that takes 2-3 days for public API access or approximately 1 week for private API access. Unlike Maersk's instant self-service model, SSL will need to register through the portal, wait for account activation, and then operate under a 1-month free trial before subscribing for continued access.

For the private (OAuth2) tier — which is needed for inland transport events, GPS tracking, and proof of delivery — SSL must be identified on the booking as a Booking Party, Deciding Party, Consignee, Notifier, or Shipper. As an NVOCC/freight forwarder, SSL should qualify in the Booking Party role, but this needs confirmation during onboarding. Some API calls are chargeable (responses 200, 201, 204, 206, 400 are billed; auth errors and rate limits are not).

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field has a row.
> ✅ = Available | ❌ = Not available | ⚠️ = Partial / limited | ❓ = Unknown

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ✅ | `GET /v1/port-schedules`, `GET /v1/vessel-schedules` (DCSA CS PILOT); Proprietary: Voyages API v2.6.2, Lines & Services API v2.2.1 | Vessel rotations, port calls, ETAs/ETDs, operational dates | DCSA CS v1 `port-schedules`, `vessel-schedules` | DCSA endpoints in PILOT status. Proprietary Voyages API provides additional operational details (berth, unberth, cutoffs) |
| 1.2 | Point-to-Point Route Options | ✅ | `GET /v1/point-to-point-routes` (DCSA CS PILOT); Proprietary: Routing Finder API v2.9.7 | Route options with legs, transit times, transshipment points | DCSA CS v1 `point-to-point-routes` | Routing Finder adds CO2/emissions data, cutoffs (port, VGM, SI, customs), covers all CMA CGM group carriers. Requires CMA CGM location codification (from referential APIs) |
| 1.3 | Booking Lifecycle | ✅ | Booking Request API v1.10.0 (proprietary); Shipment API v3.14.2 | Submit, update, cancel bookings; track shipment status | **Not DCSA** — proprietary. DCSA alignment "Scheduled for future" | Supports dry, reefer, hazardous, SOC, multi-container, inland transport. Missing: OOG, multiple commodities (planned). Shipment API retrieves booking details and live status |
| 1.4 | Shipping Instructions | ✅ | Shipping Instruction API v1.8.1 and v2.5.1 (proprietary) | Create/update shipping instructions, manage split bookings | **Not DCSA** — proprietary | v2.5.1 (02/04/2026) supports all CMA CGM group carriers. No DCSA eDocumentation API found |
| 1.5 | Rates | ❓ | Pricing category visible on portal but requires login to view | Unknown | **Not DCSA** | Pricing API and Pricing Events exist on the portal but details are not accessible without subscription |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❓ | Unknown — not explicitly documented in available Track & Trace or Schedules materials | Unknown | `ECP` | May be available in Routing Finder cutoff data (which includes "standard & special booking acceptance cutoffs") or in Booking/Shipment response. Requires live testing |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❓ | Unknown — not explicitly documented | Unknown | `EFC` | Same as 2.1 — may be in Routing Finder or Booking response. Requires live testing |
| 2.3 | Documentation Cutoff | DCO | ⚠️ | Routing Finder API v2.9.7 (explicitly lists "SI cutoffs") | SI cutoff in Routing Finder response | `DCO` | Routing Finder explicitly mentions SI (Shipping Instruction) cutoffs. May also appear in Booking/Shipment response. Partial confidence without live verification |
| 2.4 | VGM Cutoff | VCO | ⚠️ | Routing Finder API v2.9.7 (explicitly lists "VGM cutoffs") | VGM cutoff in Routing Finder response | `VCO` | Routing Finder explicitly mentions VGM cutoffs |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ⚠️ | Routing Finder API v2.9.7 (explicitly lists "Port cutoffs") | Port cutoff in Routing Finder response | `FCO` | Routing Finder mentions "Port cutoffs" and "standard & special booking acceptance cutoffs" |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❓ | Unknown — not explicitly mentioned in available documentation | Unknown | `LCO` | No explicit LCL cutoff reference found. May be included under Routing Finder cutoff data or conditional on shipment type |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ⚠️ | `GET /events` (Track & Trace DCSA TNT v2.2.0) | Inferred from first EquipmentEvent on the booking | Inferred from first EquipmentEvent | No explicit "assigned" event. Infer from first GTOT/GTIN event presence |
| 3.2 | Empty Container Gate-Out (Pickup) | ✅ | `GET /events` (Track & Trace) | `GTOT` + `EMPTY`: "Container to shipper", "Empty Picked-up at Depot", "Gate out to Consignee" | `GTOT` + `EMPTY` | Public visibility. Multiple sub-events available |
| 3.3 | Full Container Gate-In | ✅ | `GET /events` (Track & Trace) | `GTIN` + `LADEN`: "Gate in at Port terminal", "Received for export transfer", "Received for import transfer" | `GTIN` + `LADEN` | Public visibility |
| 3.4 | Container Loaded on Vessel | ✅ | `GET /events` (Track & Trace) | `LOAD` + `LADEN`: "Loaded Full at Shipper", "Loaded on board" | `LOAD` + `LADEN` | Public visibility. Also: "Full Load on rail for export/import" for rail legs |
| 3.5 | Container Discharged at Transshipment | ✅ | `GET /events` (Track & Trace) | `DISC` + `LADEN`: "Discharged in transshipment" | `DISC` + `LADEN` + transshipment | Public visibility. Explicitly listed as "Discharged in transshipment" |
| 3.6 | Container Loaded at Transshipment | ✅ | `GET /events` (Track & Trace) | `LOAD` + `LADEN` at transshipment port | `LOAD` + `LADEN` + transshipment | Inferred — no explicit "Loaded at transshipment" label, but LOAD+LADEN events at transshipment locations serve this purpose |
| 3.7 | Container Discharged at Destination | ✅ | `GET /events` (Track & Trace) | `DISC` + `LADEN`: "Discharged", "Discharged full at Consignee" | `DISC` + `LADEN` | Public visibility. "Discharged full at Consignee" explicitly covers destination discharge |
| 3.8 | Full Container Gate-Out (Delivery) | ✅ | `GET /events` (Track & Trace) | `GTOT` + `LADEN`: "Gate out to Consignee", "Container to Shipper", "Container in transit for import" | `GTOT` + `LADEN` | Public visibility |
| 3.9 | Empty Container Returned | ✅ | `GET /events` (Track & Trace) | `GTIN` + `EMPTY`: "Container Empty Returned" | `GTIN` + `EMPTY` | Public visibility. Also: reference type `ERT` (Empty Return Reference) added in v1.2.7 |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ✅ | `GET /events` (Track & Trace); Schedules APIs | `DEPA` with classifiers: Planned (Public: Barge/Train/Vessel Departure), Estimated (Public: Vessel Departure), Actual (Public: Barge/Vessel Departure; Private: Departure at Consignee/Shipper/Depot/Ramp) | `DEPA` + classifier | Full PLN/EST/ACT progression for vessel departures. Private tier adds inland departure events |
| 4.2 | Estimated Time of Arrival | ETA | ✅ | `GET /events` (Track & Trace); Schedules APIs | `ARRI` with classifiers: Planned (Public: Barge/Train/Vessel Arrival; Private: Road Arrival), Estimated (Public: Vessel Arrival), Actual (Public: Barge/Train/Vessel Arrival; Private: Arrival at Consignee/Shipper/Depot/Ramp) | `ARRI` + classifier | Full PLN/EST/ACT progression. Private tier adds inland and GPS (`IOT` event: "GPS Last Position") |
| 4.3 | Vessel Arrival at Transshipment | -- | ✅ | `GET /events` (Track & Trace) | `ARRI` at intermediate transshipment port | `ARRI` at intermediate | Vessel Arrival events at transshipment ports distinguishable by location context |
| 4.4 | Vessel Departure from Transshipment | -- | ✅ | `GET /events` (Track & Trace) | `DEPA` at intermediate transshipment port | `DEPA` at intermediate | Same as above for departure |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ✅ (proprietary) | CMA CGM offers a proprietary event push system (NOT DCSA subscription model). Equipment, Shipment, Transport, Schedules, Shipment Release, and Pricing event categories. Webhook URL provided by customer; CMA CGM pushes events to it |
| Event Polling with timestamp filter | ✅ | DCSA TNT v2.2.0 `GET /events` endpoint supports polling. Cursor-based pagination with `limit` parameter. Specific timestamp filtering capabilities require live verification |
| Event Classifier Progression (PLN->EST->ACT) | ✅ | DCSA-standard classifier codes supported: Planned, Estimated, Actual events all documented for transport events (ARRI/DEPA) |
| Retracted Events | ❓ | Unknown — not explicitly documented in available CMA CGM materials. DCSA TNT v2.2.0 spec supports retracted events but CMA CGM's implementation status is unconfirmed |
| Change Remarks | ❓ | Unknown — DCSA TNT v2.2.0 spec includes `changeRemark` but CMA CGM's implementation not confirmed |
| Delay Reason Codes | ❓ | Unknown — DCSA TNT v2.2.0 spec includes `delayReasonCode` but CMA CGM's implementation not confirmed |

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
> - Cutoffs are the biggest gap in confirmed coverage. The Routing Finder API explicitly mentions port, VGM, SI, and customs cutoffs, but field-level mapping requires live testing. Three cutoffs (DCO, VCO, FCO) are marked partial based on Routing Finder documentation mentions.
> - Container milestone 3.1 (Container Assigned) is marked partial because it must be inferred from the first equipment event rather than an explicit assignment event.
> - Container milestone 3.6 (Loaded at Transshipment) is available but inferred from LOAD+LADEN at transshipment location rather than an explicitly labeled event.
> - Change detection has 3 unknown fields because CMA CGM's Track & Trace is DCSA TNT v2.2.0, which includes retracted events, change remarks, and delay reason codes in the spec, but CMA CGM's implementation of these specific features is unconfirmed.
> - The Rates domain (1.5) is unknown because the Pricing API exists but is not accessible without subscription.
> - CMA CGM's APIs cover all carriers of the CMA CGM group (APL, ANL, CNC), not just CMA CGM itself.

---

## Endpoint Reference

### Tracking / Events

| Endpoint | Method | Lookup Params | Pagination | Response Format | Notes |
|----------|--------|--------------|------------|----------------|-------|
| `GET /events` (with unique tracking reference) | GET | Unique tracking reference (B/L, booking ref, or container number — specific param names require Swagger spec) | DCSA cursor-based: `limit` query param; response headers `Current-Page`, `Next-Page`, `Prev-Page`, `Last-Page`, `First-Page`. Cursor example: `fE9mZnNldHw9MTAmbGltaXQ9MTA=`. Always returns HTTP 200 | JSON (DCSA TNT v2.2.0) | `getMoveOnCommercialCycle` — retrieve events for a specific shipment. Mixed auth: OAuth2 + ApiKey |
| `GET /events` (search) | GET | Broader search parameters (details require Swagger spec access) | Same DCSA cursor-based pagination | JSON (DCSA TNT v2.2.0) | `searchMoveOnCommercialCycle` — broader event search. Mixed auth: OAuth2 + ApiKey |

### Schedules

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| `GET /v1/point-to-point-routes` | GET | Origin, destination, date range (DCSA CS v1 standard params) | DCSA cursor-based | JSON (DCSA CS v1) | PILOT status. Single or multiple end-to-end route options with transport legs, estimated timings, interdependencies |
| `GET /v1/port-schedules` | GET | Port (UNLocationCode), starting date | DCSA cursor-based | JSON (DCSA CS v1) | PILOT status. All arriving/departing vessels with estimated timestamps |
| `GET /v1/vessel-schedules` | GET | Service, voyage, vessel, location | DCSA cursor-based | JSON (DCSA CS v1) | PILOT status. Estimated departure/arrival times for each port call |
| Routing Finder (proprietary) | GET | CMA CGM location codes (from referential APIs) | Proprietary: default 50 results, HTTP 206 if more. `content-range` header: `0-49/408`. Request `range` header: `50-99` | JSON (proprietary) | v2.9.7. Returns routes for all CMA CGM group carriers. Includes cutoffs, emissions (CO2, NOx, SOx, PM10). Requires CMA CGM-specific location codes |
| Lines & Services (proprietary) | GET | Carrier, trade line parameters | Proprietary range-based | JSON (proprietary) | v2.2.1. Loop routing details, service frequency, ports & terminals, transit time, vessel fleet |
| Voyages (proprietary) | GET | Service, vessel, voyage | Proprietary range-based | JSON (proprietary) | v2.6.2. Operational voyage details: berth, unberth, cutoffs, terminals |

### Booking

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| Booking Request API (proprietary) | POST/PUT/DELETE | Booking reference, cargo details, routing, container specs | Proprietary range-based (for list queries) | JSON (proprietary) | v1.10.0. Submit, update, cancel bookings. Supports dry, reefer, hazardous, SOC, inland, multi-container. NOT DCSA-aligned (planned for future) |
| `GET Shipments` (Shipment API) | GET | Shipment/booking reference | Proprietary range-based | JSON (proprietary) | v3.14.2. Live status updates (reservations, empty pick-ups, etc.); retrieve booking details for SI submission |
| `GET BL list` (Shipment API) | GET | Date range period | Proprietary range-based | JSON (proprietary) | v3.14.2. Booking references list over a specified range (as deciding party) |

### Shipping Instructions

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| Shipping Instruction API v1 | POST/PUT | Booking reference, SI details | Unknown | JSON (proprietary) | v1.8.1. Original version |
| Shipping Instruction API v2 | POST/PUT | Booking reference, SI details, split booking management | Unknown | JSON (proprietary) | v2.5.1 (02/04/2026). Supports all CMA CGM group carriers |

### Referential APIs (Free)

| Endpoint | Method | Purpose | Key Params | Notes |
|----------|--------|---------|-----------|-------|
| Charge Referential | GET | Surcharges referential | Unknown | v1.0.0 |
| Commercial Lines & Services | GET | Commercial lines and services | Unknown | v1.1.0 |
| Goods Codification | GET | Commodity codification | Scope: `commodity:be` | v2.2.0 |
| IMDG Codification | GET | Dangerous goods referential | Scope: `imdg:read:be` | v1.2.0 |
| Local Voyage Reference | GET | Local voyage references | Unknown | v2.0.0 |
| Location Referential | GET | Points, pools, places, countries | Unknown | v3.11.2. Required for Routing Finder (CMA CGM location codes) |
| Packaging Referential | GET | Containers, bulk, packages | Unknown | v2.2.1 |
| Shipment & Tracking Events Referential | GET | Moves/events descriptions | Unknown | v1.5.0. Complementary to tracking API |
| Shipping Company Referential | GET | CMA CGM group shipping companies | Unknown | v1.3.0 |
| Vessel Referential | GET | Vessel data | Unknown | v1.9.1 |

### Login-Required API Categories (Not Publicly Accessible)

The following API categories are visible on the portal but require login/subscription to view details. They were identified during research but could not be inventoried without authenticated access.

| Category | Portal Visibility | Notes |
|----------|------------------|-------|
| **Pricing** | Category visible, details hidden | Pricing API and Pricing Events exist. Referenced in field 1.5 (Rates) |
| **BL Suite** | Category visible, details hidden | Bill of Lading management APIs. Details unknown without subscription |
| **Documents** | Category visible, details hidden | Document management APIs. Details unknown without subscription |
| **Shipment Release** | Category visible, details hidden | Shipment release APIs. Also available as a push event category |

Source: research-notes.md (API Portal Structure, lines 30-40, 351-356)

### Other API Products (Discovered, Not Core to Tracking)

The following API products were discovered during research. They are not directly relevant to the core tracking/visibility use case but are listed for completeness.

| API Product | Category | Version | Auth | Notes |
|------------|----------|---------|------|-------|
| Value Added Services Product Catalog | Transport Execution | v2.2.5 (01/17/2024) | Unknown | Retrieve priced value-added services eligible to a shipment |
| Real Time Vessel Allocation | Allocation | v1.2.0 (10/15/2023), v2.0.0 (03/04/2024) | Unknown | Space visibility per routing for quotation/US Service Contract. Used internally by Booking Request API |
| Invoice Copy PDF | Invoice | v1.4.0 (01/03/2023) | Private connection only | PDF invoice retrieval |
| Invoice Data Service | Invoice | v2.3.1 (06/23/2025) | Private connection only | Structured invoice data |

### Lookup Methods Summary

| Identifier Type | Supported? | Which Endpoints? | Notes |
|----------------|-----------|-----------------|-------|
| **Bill of Lading (B/L) number** | ✅ | Track & Trace `GET /events`, Shipment API `GET BL list` | Web portal also supports B/L lookup |
| **Booking reference** | ✅ | Track & Trace `GET /events`, Shipment API `GET Shipments`, Booking Request API | Primary identifier pre-B/L issuance |
| **Container number** | ✅ | Track & Trace `GET /events` | Web portal also supports container number lookup |
| **Carrier booking number** | ✅ | Same as booking reference | Used interchangeably in CMA CGM context |
| **Vessel IMO / voyage** | ✅ | Schedules APIs (vessel-schedules, voyages), Track & Trace (filtering) | Schedules APIs support vessel/voyage/service filtering |

---

## Rate Limits & Quotas

| Detail | Value | Source |
|--------|-------|--------|
| **Global rate limit** | Yes — per-application limits. Specific numbers unpublished (not visible without authenticated access) | Official |
| **Per-endpoint limits** | Unpublished — contact CMA CGM for higher limits | Official |
| **Daily/monthly quota** | Unpublished | Unknown |
| **Rate limit response** | HTTP 429 with `retry-after` header (time in seconds, e.g., 3600 for 1 hour) | Official |
| **Rate limit by** | Per-application (API key / OAuth token) | Official |
| **Burst allowance** | Unknown | Unknown |
| **Different tiers** | Some API calls are chargeable (200, 201, 204, 206, 400 responses billed). Auth errors (401, 403), rate limits (429), and server errors (5XX) are not chargeable | Official |

**Caching guidance:** CMA CGM returns `cache-control: max-age=3600` and encourages transactional interfaces with local caching over bulk retrieval.

**Gotcha:** The 1-hour `retry-after` value (3600 seconds) observed in documentation is notably aggressive. If rate limits are hit, the lockout period may be very long. This needs careful handling in the adapter to avoid exceeding limits.

---

## Webhook / Push Support

| Detail | Value |
|--------|-------|
| **Webhooks supported?** | Yes — proprietary event push system (NOT DCSA subscription model) |
| **Subscription endpoint** | Proprietary — "Subscription" category visible on portal. Details require login |
| **Subscription management** | Proprietary subscription management (details require portal access) |
| **Subscribable event types** | Equipment events, Shipment events, Transport events, Schedules events, Shipment Release events, Pricing events |
| **Callback format** | Events POSTed to customer-provided webhook URL (proprietary format — not DCSA event JSON) |
| **Callback authentication** | CMA CGM supports authenticating to customer's webhook via API Key or OAuth2 Client Credentials. OAuth2 strongly recommended by CMA CGM |
| **Retry policy on failure** | Configurable per customer. Parameters: Maximum event age (default 24h), Retry frequency (Linear or Exponential). Linear example: every 10 min. Exponential example: 5 min, 10 min, ..., 1 hour (until max event age). 5XX errors retried; 4XX errors not retried. Customer can define rate limit on webhook URL; CMA CGM handles 429 with `retry-after` header |
| **Documented reliability** | No published SLA. Default maximum event age of 24 hours means events older than 24h may be dropped if delivery consistently fails |

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | https://www.cma-cgm.com/ebusiness/tracking |
| **Login required?** | No — basic tracking available without login. Registered users get map view and event notifications |
| **Data available on portal but NOT in API** | Map visualization of container position at sea, notification configuration for shipments. Functional data should be the same as API but map rendering is portal-only |
| **Scraping feasibility** | Not assessed — API coverage should be sufficient. Portal is web-based |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Yes |
| **EDI message types** | IFTMBF (Booking), IFTMIN (Shipping instructions), IFTSTA (Tracking/container status), IFTMCS (Bill of Lading), IFTSAI (Schedules, 12-week horizon), VERMAS (VGM) |
| **EDI connection method** | Unknown — contact CMA CGM directly |
| **EDI documentation** | https://www.cma-cgm.com/products-services/ecommerce/edi-api-channels/EDI-catalog |

### Mobile App

| Detail | Value |
|--------|-------|
| **Mobile app available?** | Yes |
| **Platforms** | iOS (confirmed), Android (reported) |
| **Tracking capabilities** | Container tracking available via app |
| **App URL** | https://www.cma-cgm.com/products-services/ecommerce/mobileapp |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Yes | CMA CGM listed among supported ocean carriers |
| **FourKites** | Yes | Ocean visibility coverage (reported) |
| **Vizion** | Yes | Container tracking via API; supports B/L, booking, container lookup. See https://www.vizionapi.com/carrier-tracking/cma-cgm |
| **INTTRA / E2open** | Yes | Booking, schedules, rates, visibility/tracking via INTTRA Ocean Execution APIs (reported) |
| **CargoSmart** | Yes | Schedule and tracking visibility (reported) |
| **Terminal49** | Yes | Container tracking (CMDU SCAC). See https://terminal49.com/shipping-lines/cmdu-cma-cgm-container-tracking |

> **Aggregator note:** CMA CGM's direct API is reasonably comprehensive for tracking, but the proprietary (non-DCSA) booking and shipping instruction APIs add complexity. For tracking-only use cases, direct integration is viable. If SSL needs a faster path to production or wants to avoid the dual-auth complexity, aggregators like Vizion or Terminal49 offer normalized CMA CGM tracking. However, aggregators may not expose the full event detail (private-tier inland events, GPS, proof of delivery) that direct OAuth2 access provides.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown — not published. CMA CGM's DCSA success story quotes API Factory Lead Romain Genoulaz on standardization benefits but does not mention latency. Private-tier events (GPS) suggest near-real-time for some data | Unknown |
| **API uptime/reliability** | No public status page found. No published SLA | Unknown |
| **Historical data depth** | Unknown — not documented in available materials | Unknown |
| **Timezone handling** | Expected ISO 8601 with timezone per DCSA specification for TNT endpoints. Proprietary endpoints unknown | Estimated (DCSA spec) |
| **Character encoding** | Expected UTF-8 per DCSA specification | Estimated (DCSA spec) |

### Known Issues & Gotchas

- **5-minute OAuth2 token lifetime**: CMA CGM OAuth2 tokens expire in 299 seconds (~5 minutes), which is extremely short compared to typical OAuth2 implementations (Maersk is ~1 hour). The adapter must cache tokens aggressively and refresh proactively to avoid mid-request token expiration. For any request sequence taking longer than ~4 minutes, token refresh mid-flow is required.

- **Dual auth with different data visibility**: Public (API Key) and Private (OAuth2) tiers return fundamentally different event sets for the same shipment. Public sees standard vessel and port events; Private adds inland transport, GPS positions, pickup/delivery appointments, and proof of delivery. The adapter must handle both tiers and gracefully degrade when only public access is available.

- **DCSA subscription endpoints not implemented**: Despite implementing DCSA TNT v2.2.0, CMA CGM does NOT implement the DCSA subscription management endpoints. The webhook system is proprietary. This means the DCSA base adapter's subscription handling cannot be reused for CMA CGM — webhook setup requires proprietary implementation.

- **Proprietary location codes**: The Routing Finder API (most detailed schedule/cutoff source) requires CMA CGM-specific location codification, not standard UN/LOCODEs. Location codes must first be retrieved via the Location Referential API. This adds a lookup step not present in pure DCSA implementations.

- **Two pagination systems**: DCSA endpoints use cursor-based pagination with response headers (`Current-Page`, `Next-Page`, etc.). Proprietary endpoints use range-based pagination with HTTP 206 Partial Content and `content-range`/`range` headers. The adapter must support both.

- **Chargeable API calls**: Unlike most carrier APIs, CMA CGM charges for certain API calls (successful responses 200, 201, 204, 206 and even 400 errors are billable). Only auth failures (401, 403), rate limits (429), and server errors (5XX) are free. This has cost implications for polling frequency.

- **CMA CGM group coverage**: APIs return data for all group carriers (APL, ANL, CNC), not just CMA CGM. SCAC codes CMDU, CMDA, CACM, CMAU may all appear. The adapter should handle multi-SCAC responses.

- **No sandbox**: There is no dedicated test environment. The free trial provides production access with limited data, meaning all testing happens against live data.

- **DCSA Commercial Schedules in PILOT**: The DCSA CS endpoints are labeled as PILOT (v1.0.7, dated 02/18/2024). They may have stability or completeness issues compared to the mature proprietary schedule endpoints.

### Recently Deprecated or Changed

- **Track & Trace v1.2.7 (02/21/2025)**: Added new reference types ERT (Empty Return Reference) and LOAD (LOAD reference). Adapter should handle these new reference types.

- **Shipping Instruction API v2.5.1 (02/04/2026)**: New version alongside legacy v1.8.1. The new version adds split booking management and multi-carrier group support. v1 may be deprecated in future.

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | Yes — CMA CGM exposes comprehensive tracking data via DCSA TNT v2.2.0 with rich equipment, transport, and (limited) shipment events. Booking and shipping instructions available through proprietary APIs |
| **Implementation effort** | Medium (DCSA + deviations) — tracking is DCSA-aligned but subscription/webhooks are proprietary; auth is dual with very short token lifetime; two pagination systems; some APIs need proprietary location codes |
| **DCSA base adapter usable?** | Yes with overrides — DCSA base adapter handles event parsing and normalization for Track & Trace. Must override: subscription/webhook handling (proprietary), auth (dual with 5-min tokens), pagination (dual system), cutoff retrieval (proprietary Routing Finder) |

### Recommended Approach

The CMA CGM adapter should extend the DCSA base adapter class for the tracking/events layer, since the Track & Trace API implements DCSA TNT v2.2.0. The event model, equipment/transport event codes, and classifier progression (PLN/EST/ACT) are standard DCSA and can reuse the same parsing logic built for Maersk.

However, significant proprietary overrides are needed:

1. **DCSA Base Layer**: Reuse for `GET /events` parsing, event normalization, DCSA event code mapping, and cursor-based pagination on DCSA endpoints. The response shape for tracking events should match the DCSA TNT v2.2.0 schema.

2. **Proprietary Overrides**: Webhook/push subscription must be implemented against CMA CGM's proprietary event system (not DCSA `POST /event-subscriptions`). Cutoff data requires the proprietary Routing Finder API with CMA CGM location code lookups. Booking and shipping instruction workflows are fully proprietary.

3. **Auth Handler**: Must implement both API Key (`KeyId` header) and OAuth2 client_credentials flow with aggressive token refresh (299-second lifetime). The auth handler is more complex than Maersk's due to the very short token lifetime and scope-per-endpoint requirements.

The adapter is roughly 60% DCSA-reusable (tracking events) and 40% proprietary (webhooks, cutoffs, booking, auth).

### Recommended Lookup Method

**Bill of Lading (B/L) number** is the recommended primary lookup method for tracking, consistent with the Maersk adapter. The Track & Trace DCSA API accepts standard document references.

**Booking reference** as secondary — available earlier in the lifecycle, usable with both the Track & Trace API and the proprietary Shipment API for status and booking details.

**Container number** as supplementary — useful for per-container tracking in multi-container shipments.

Note: Specific query parameter names for the Track & Trace `GET /events` endpoint require Swagger spec access (behind login). The DCSA TNT v2.2.0 standard uses `documentTypeCodes` and `documentReference`, which CMA CGM should follow.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Every 4-6 hours for active shipments (longer than Maersk due to chargeable API calls). Every 12-24 hours for pre-departure. Consider webhook push as primary with polling as verification/fallback to reduce costs |
| **Incremental filter** | Use DCSA timestamp filtering on `GET /events` (expected: `eventCreatedDateTime` filter per TNT v2.2.0). Verify parameter name after Swagger spec review |
| **Batch tracking** | One API call per shipment. No batch/multi-shipment endpoint in DCSA standard. Use webhooks to minimize polling volume and associated costs |

**Cost-aware polling**: Since CMA CGM charges for API calls, the adapter should track polling costs and consider longer intervals for shipments in stable states (e.g., at sea between port calls). Webhook-first strategy is strongly recommended to minimize billable polling requests.

### Auth Implementation Notes

```
OAuth2 Flow (for Private APIs):
  POST https://auth.cma-cgm.com/as/token.oauth2
  Content-Type: application/x-www-form-urlencoded
  Body: grant_type=client_credentials&client_id={id}&client_secret={secret}&scope={scope}
  Response: {"access_token":"...","token_type":"Bearer","expires_in":299}
  Usage: Authorization: Bearer {access_token}

API Key Flow (for Public APIs):
  Header: KeyId: <API_Key_Value>
```

The adapter must:
- Cache OAuth2 tokens and refresh well before the 299-second expiry (recommend refresh at ~200 seconds / ~3.5 minutes to provide safety margin)
- Support per-endpoint scopes (e.g., `imdg:read:be`, `commodity:be`, `charges:read:be`) — each endpoint may require different scopes
- Route to correct auth method based on whether the API is public or private
- Store credentials securely (provided by consumer, never logged)
- Handle 401 responses by refreshing token and retrying once
- Be aware that token endpoint is on a different domain (`auth.cma-cgm.com`) than the API base URL (`apis.cma-cgm.net`)

**Gotcha: Dual auth is like Maersk but different in implementation.** Maersk splits by endpoint path prefix; CMA CGM splits by API tier (public vs. private). The same tracking endpoint (`GET /events`) accepts BOTH auth methods but returns different data depending on which is used. Public auth = standard events only; Private auth = standard + inland/GPS/POD events.

### Edge Cases to Handle

- **Very short OAuth2 token lifetime (299 seconds)**: Any long-running operation or retry sequence may span multiple token lifetimes. The adapter must handle token refresh transparently within request pipelines, not just between requests.

- **Dual pagination systems in a single adapter**: DCSA endpoints return cursor-based pagination with page headers; proprietary endpoints return HTTP 206 with `content-range`. The adapter must detect which system is in use (based on endpoint type or response status code) and handle accordingly.

- **CMA CGM group multi-carrier responses**: Events and schedules may include data from APL (APLU), ANL, CNC in addition to CMA CGM (CMDU). The adapter should correctly attribute events to the originating carrier within the group.

- **Proprietary location codes for Routing Finder**: The most complete schedule/cutoff data requires CMA CGM location codes. The adapter needs a location code translation layer (UN/LOCODE to CMA CGM code) using the Location Referential API, with caching to avoid repeated lookups.

- **Chargeable 400 errors**: Unlike most APIs where client errors are "free," CMA CGM charges for 400 Bad Request responses. Input validation must be thorough client-side before making API calls to avoid paying for malformed requests.

- **Missing DCSA subscription endpoints**: The adapter cannot use the DCSA base class's subscription management. Webhook setup flows through CMA CGM's proprietary system, likely requiring portal configuration rather than API-based subscription management.

- **PILOT status of DCSA Commercial Schedules**: These endpoints may change or have incomplete coverage. The adapter should fall back to proprietary schedule endpoints (Routing Finder, Voyages) if DCSA schedule data is insufficient.

### Mapping Complexity

**Medium complexity.** The tracking layer is DCSA TNT v2.2.0 compliant, making event-to-canonical mapping straightforward and largely reusable from the DCSA base adapter. The key mapping challenges are:

1. **Event code mapping**: CMA CGM's DCSA events use standard codes (GTOT, GTIN, LOAD, DISC, ARRI, DEPA) with standard classifiers. Direct mapping from the DCSA base adapter.

2. **Public vs. Private event merging**: The same shipment tracked with public auth vs. private auth returns different event sets. The adapter must merge these coherently if both tiers are available, avoiding duplicate events.

3. **Cutoff mapping**: Cutoffs come from the proprietary Routing Finder API (not DCSA booking response). Mapping Routing Finder cutoff fields to canonical cutoff codes (DCO, VCO, FCO, etc.) requires proprietary field analysis after Swagger spec access.

4. **Proprietary schedule enrichment**: DCSA schedule data (PILOT) may need augmentation from proprietary Routing Finder data (emissions, detailed cutoffs, group-wide routes). Merging these two data sources into a unified schedule view adds complexity.

5. **DROP/PICK events**: CMA CGM uses `DROP` events for empty return planning ("Plan Empty Return") and delivery appointments, plus `PICK` events for pickup appointments. These are private-tier events not in the standard DCSA milestone set and need custom mapping.

---

## Open Questions

- [ ] **What are the specific query parameters for the Track & Trace `GET /events` endpoint?** — Swagger spec requires portal login. Do they follow DCSA TNT v2.2.0 exactly (`documentTypeCodes`, `documentReference`, `equipmentReference`, `eventCreatedDateTime`)?
- [ ] **Does SSL have an existing CMA CGM portal account?** — Would accelerate development and reveal Swagger specs, webhook configuration UI, and hidden API products (Pricing, BL Suite, Documents, Shipment Release)
- [ ] **What are the exact cutoff fields in the Routing Finder and Booking/Shipment API responses?** — Critical for mapping ERD/EFC/DCO/VCO/FCO/LCO fields
- [ ] **What are the specific rate limits per application?** — Unpublished; only discoverable after registration and potentially different per subscription tier
- [ ] **How is the proprietary webhook subscription configured?** — Via portal UI? Via API? What event filters are available? This is critical for real-time tracking
- [ ] **Does the DCSA Track & Trace API support `eventCreatedDateTime` filtering?** — Standard in DCSA TNT v2.2.0 but needs confirmation given CMA CGM's stated deviations
- [ ] **What is the response shape difference between public (API Key) and private (OAuth2) tracking requests?** — Same response shape with more events, or different schemas?
- [ ] **Are the DCSA Commercial Schedules endpoints stable enough for production use?** — PILOT status since 02/18/2024 with no version updates raises questions
- [ ] **What is the billing model for API calls?** — Per-call pricing? Subscription tiers? Minimum commitments? This affects the cost model for polling
- [ ] **Does CMA CGM implement retracted events, change remarks, and delay reason codes in their DCSA TNT v2.2.0?** — These are in the DCSA spec but CMA CGM's deviation list suggests incomplete implementation

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | https://www.cma-cgm.com |
| API Portal (main) | https://api-portal.cma-cgm.com |
| API Portal - Visibility (Track & Trace) | https://api-portal.cma-cgm.com/products/visibility |
| API Portal - Track & Trace Detail | https://api-portal.cma-cgm.com/products/api/operation.trackandtrace.v1 |
| API Portal - Schedules | https://api-portal.cma-cgm.com/products/schedules |
| API Portal - Transport Execution | https://api-portal.cma-cgm.com/products/transport-execution |
| API Portal - Allocation | https://api-portal.cma-cgm.com/products/allocation |
| API Portal - Invoice | https://api-portal.cma-cgm.com/products/invoice |
| API Portal - Referential | https://api-portal.cma-cgm.com/products/referential |
| API Usage Guide | https://api-portal.cma-cgm.com/usage-guide |
| API Contact (Business) | https://api-portal.cma-cgm.com/contact-us/business-request |
| EDI/API Solutions Page | https://www.cma-cgm.com/products-services/ecommerce/edi-api-channels |
| EDI Catalog | https://www.cma-cgm.com/products-services/ecommerce/edi-api-channels/EDI-catalog |
| API Starting Guide | https://www.cma-cgm.com/products-services/ecommerce/edi-api-channels/API-starting-guide |
| Tracking Portal (Web) | https://www.cma-cgm.com/ebusiness/tracking |
| Schedules Portal (Web) | https://www.cma-cgm.com/ebusiness/schedules |
| OAuth2 Token Endpoint | https://auth.cma-cgm.com/as/token.oauth2 |
| API Base URL (Production) | https://apis.cma-cgm.net |
| DCSA Success Story (CMA CGM) | https://dcsa.org/newsroom/success-story-dcsa-track-trace-standard |
| DCSA Members Page | https://dcsa.org/about-us-our-work-and-what-we-do-dcsa/members/ |
| DCSA OpenAPI Specs (GitHub) | https://github.com/dcsaorg/DCSA-OpenAPI |
| DCSA Information Model v3.3 | https://dcsa.org/wp-content/uploads/2021/10/202108_DCSA_P1_Information-Model-v3.3_TNT22_Final.pdf |
| Vizion CMA CGM Tracking | https://www.vizionapi.com/carrier-tracking/cma-cgm |
| Terminal49 CMA CGM | https://terminal49.com/shipping-lines/cmdu-cma-cgm-container-tracking |
| GitHub tracktrace library | https://github.com/dhruvkar/tracktrace |
| CMA CGM Customer Service (API) | https://mycustomerservice.cma-cgm.com/s/selfcare/article/API-Solution?language=en_US |
| DCSA Commercial Schedules Standard | https://dcsa.org/standards/commercial-schedules |
| CMA CGM Mobile App | https://www.cma-cgm.com/products-services/ecommerce/mobileapp |
| Port Schedules (Web) | https://www.cma-cgm.com/ebusiness/schedules/port |
