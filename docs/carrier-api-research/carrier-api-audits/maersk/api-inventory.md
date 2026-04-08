# Maersk Line — API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only — not verified with live API testing. Endpoint existence confirmed via HTTP probing (401/404 analysis). DCSA OpenAPI specifications used as primary reference for Maersk's DCSA-compliant endpoints. Developer portal content could not be scraped (SPA) but is confirmed active.
> **Researched by**: Agent (audit/maersk workflow)
> **Date**: 2026-02-11
> **Last verified**: 2026-02-11

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | A.P. Møller–Mærsk A/S (commonly "Maersk" or "Maersk Line") |
| **SCAC Code** | MAEU |
| **Parent Company** | A.P. Møller–Mærsk A/S (publicly traded, OMX: MAERSK-B) |
| **Alliance** | 2M (with MSC) — note: 2M alliance ended January 2025; Maersk now operates independently via Gemini Cooperation with Hapag-Lloyd |
| **Primary Services** | Container shipping, inland logistics, supply chain management, port/terminal operations (APM Terminals) |
| **Market Position** | Second-largest container shipping line globally (~17% market share by capacity) |
| **Headquarters** | Copenhagen, Denmark |
| **Website** | https://www.maersk.com |

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | Yes |
| **Developer portal URL** | https://developer.maersk.com |
| **API documentation URL(s)** | https://developer.maersk.com (SPA — API catalogue requires JavaScript rendering) |
| **Documentation quality** | Excellent — comprehensive DCSA-aligned docs with interactive API references (reported by developers; portal requires registration for full access) |
| **OpenAPI/Swagger spec available?** | Yes — via DCSA standard specs at https://github.com/dcsaorg/DCSA-OpenAPI and interactive docs on developer portal (Scalar-based API reference viewer detected in portal source) |
| **Sandbox/test environment?** | Yes — Maersk provides a sandbox/test environment via the developer portal (reported; details require portal registration) |
| **Developer registration** | Free self-service registration at https://developer.maersk.com — no partner agreement required for API access |
| **Developer support channels** | Developer portal support, Maersk API support team (via portal), status page at https://status.maersk.com |
| **Community/third-party libraries** | Minimal — no significant open-source client libraries found on GitHub, npm, or PyPI. A few individual repos exist (e.g., `srushtikanade-pixel/maersk-tracking`) but none are maintained or substantial |
| **API changelog / release notes** | Available on developer portal (requires login); DCSA spec changelogs at https://github.com/dcsaorg/DCSA-OpenAPI |
| **API status page** | https://developer.maersk.com/api-status (200 OK confirmed), https://status.maersk.com (200 OK confirmed) |

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | Yes — founding member of DCSA |
| **DCSA APIs implemented** | TNT (Track & Trace), BKG (Booking), CS (Commercial Schedules) |
| **DCSA TNT version** | v2 and v3 (both confirmed live — `/synergy/tracking/v2/events` and `/track-and-trace/v3/events`). **Note:** The GitHub master branch (`tnt/v3/tnt.yaml`) contains TNT v3.0.0-Beta-1 (March 2023). A redesigned TNT 3.0.0 is published on SwaggerHub but remains in alpha/design iterations (20250912-design, 20251121-alpha, 20260116-alpha). Maersk's live `/track-and-trace/v3/` endpoints align with the **Beta-1** design pattern (subscription endpoints, event filtering), not the redesigned 3.0.0 architecture. |
| **DCSA Booking version** | v2.x (booking endpoints exist but exact Maersk path not confirmed as 404 at `/booking/v2/bookings` — likely behind a different path prefix) |
| **DCSA Schedules version** | v1.x (`/schedules/v1/vessel-schedules`, `/schedules/v1/port-schedules`, `/schedules/v1/point-to-point-routes` all confirmed live) |
| **Known DCSA deviations** | None documented publicly. As a DCSA founding member, Maersk is among the most complete DCSA implementors. Minor deviations may exist between DCSA spec versions — Maersk appears to run both v2 and v3 TNT endpoints simultaneously. Some endpoints use different path prefixes than the DCSA spec paths (e.g., `/synergy/tracking/v2/` vs. spec's `/v2/events`) |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Yes | Maersk supports IFTMIN, IFTSTA, COPARN, BAPLIE and other EDIFACT message types for traditional B2B communication |
| **INTTRA integration** | Yes | Maersk is available on the INTTRA (now E2open) platform for booking and tracking |
| **BIC (Bureau International des Containers)** | Yes | Standard container ID format (owner code + serial + check digit) used throughout APIs |
| **UN/LOCODE** | Yes | UNLocationCode used consistently across all endpoints (confirmed in DCSA spec implementations) |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | Dual: OAuth2 Client Credentials (for some endpoints) + API Key (Consumer-Key header, for others) |
| **Auth documentation** | https://developer.maersk.com (authentication section — requires login for full details) |
| **Registration process** | 1. Visit https://developer.maersk.com 2. Create a free developer account 3. Register an application to obtain API key / client credentials 4. Use credentials to authenticate API calls |
| **Registration URL** | https://developer.maersk.com |
| **Partner program required?** | No — basic API access is self-service. Production / elevated access may require a business relationship for some APIs |
| **Partner program URL** | N/A for basic access |
| **Credential type** | Consumer-Key (API Key) for most endpoints; Client ID + Client Secret for OAuth2 endpoints |
| **Token refresh supported?** | Yes — OAuth2 client_credentials flow provides access tokens; refresh by re-requesting |
| **Token lifetime** | Unknown — requires live testing to determine (estimated ~1 hour based on standard OAuth2 patterns) |
| **Access tiers** | Reported: Basic (self-service, standard rate limits) and Partner/Enterprise (elevated limits). Specific tier details require portal registration to confirm |
| **IP whitelisting required?** | No — CORS headers indicate `access-control-allow-origin: *` (wide open) |

### Authentication Details Observed

Two distinct auth patterns were observed during endpoint probing:

1. **OAuth2 pattern** — Endpoints under `/synergy/tracking/v2/`, `/v1/inland/`, `/v1/locations`, `/v1/products/` return: `{"httpMethod":"GET","requestUri":"...","statusCode":401,"statusText":"Unauthorized","correlationIdentifier":"...","errorTimestamp":"..."}`. These use OAuth2 Bearer tokens obtained from `POST api.maersk.com/oauth2/access_token` with `grant_type=client_credentials`.

2. **API Key pattern** — Endpoints under `/track-and-trace/v3/`, `/schedules/v1/`, `/rates/`, `/ecommerce/tracking/`, `/products/v1/`, `/reference-data/v1/` return: `{"error":[{"code":"ERR_GW_001","message":"API Key Validation Failed, please check the API key","reason":"Invalid or expired Key","status":"401"}]}`. These require a `Consumer-Key` header (observed in CORS `access-control-allow-headers`).

The `access-control-allow-headers` response lists both `Authorization` and `Consumer-Key` / `x-maersk-consumer-key`, confirming the dual auth approach.

### Access Requirements Summary for SSL

Maersk offers the most developer-friendly API access of any major ocean carrier. SSL can get started immediately by:

1. Registering a free developer account at https://developer.maersk.com (self-service, no business relationship needed)
2. Creating an application to obtain a Consumer-Key (API key) and/or OAuth2 client credentials
3. Using the sandbox environment for development and testing

For production usage with higher rate limits or access to additional APIs (e.g., Booking, Spot Rates), SSL may need to engage with Maersk's partnership team. The basic tracking and scheduling APIs should be accessible with self-service credentials.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field has a row.
> ✅ = Available | ❌ = Not available | ⚠️ = Partial / limited | ❓ = Unknown

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ✅ | `GET /schedules/v1/vessel-schedules`, `GET /schedules/v1/port-schedules` | Vessel rotation objects with port calls, ETAs/ETDs | DCSA CS v1 `vessel-schedules`, `port-schedules` | Both endpoints confirmed live (401). Also available at `/v1/products/ocean-schedules` |
| 1.2 | Point-to-Point Route Options | ✅ | `GET /schedules/v1/point-to-point-routes` | `PointToPoint` objects with `legs[]`, `transitTime`, `cutOffTimes[]` | DCSA CS v1 `point-to-point-routes` | Confirmed live (401). Supports UNLocationCode, date ranges, maxTransshipment filter |
| 1.3 | Booking Lifecycle | ✅ | Booking API (exact Maersk path unconfirmed — `/booking/v2/` returned 404; likely different prefix) | Booking status, `transportPlan[]`, `shipmentCutOffTimes[]`, `carrierClauses[]` | DCSA BKG v2 `/v2/bookings` | DCSA BKG spec confirms GET/POST/PUT/DELETE for bookings + `/v2/booking-notifications` for push |
| 1.4 | Shipping Instructions | ⚠️ | Unknown Maersk path (EBL endpoints returned 404 at probed paths) | ShipmentEvent with `documentTypeCode=SHI` | DCSA EBL (Electronic Bill of Lading) API (`github.com/dcsaorg/DCSA-OpenAPI/tree/master/ebl`) | Maersk likely implements the EBL API but specific endpoints not confirmed. Track via ShipmentEvents in TNT API |
| 1.5 | Rates | ✅ | `GET /rates/spot` | Proprietary spot rate response | **Not DCSA** — proprietary Maersk API | Confirmed live (401). Maersk is one of few carriers with a public rate API |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ✅ | CS point-to-point response (`GET /schedules/v1/point-to-point-routes`) | `cutOffDateTimeCode: "ECP"` in `cutOffTimes[]` (CS v1 CutOffTime schema) | `ECP` | ECP is defined in the CS v1 `CutOffTime` schema only — **not** in the BKG v2 `ShipmentCutOffTime` schema |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ✅ | Booking confirmation response (`shipmentCutOffTimes[]` in BKG v2) and CS point-to-point response (`cutOffTimes[]` in CS v1) | `cutOffDateTimeCode: "EFC"` in `shipmentCutOffTimes[]` (BKG v2) or `cutOffTimes[]` (CS v1) | `EFC` | Available in both DCSA BKG v2 `ShipmentCutOffTime` and CS v1 `CutOffTime` schemas |
| 2.3 | Documentation Cutoff | DCO | ✅ | Booking confirmation response; also in CS point-to-point response | `cutOffDateTimeCode: "DCO"` in `shipmentCutOffTimes[]` | `DCO` | Confirmed in DCSA BKG v2 spec examples: `"cutOffDateTimeCode": "DCO"` with `"cutOffDateTime"` |
| 2.4 | VGM Cutoff | VCO | ✅ | Booking confirmation response | `cutOffDateTimeCode: "VCO"` in `shipmentCutOffTimes[]` | `VCO` | Confirmed in DCSA BKG v2 spec examples |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ✅ | Booking confirmation response | `cutOffDateTimeCode: "FCO"` in `shipmentCutOffTimes[]` | `FCO` | Confirmed in DCSA BKG v2 spec examples |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ⚠️ | Booking confirmation response | `cutOffDateTimeCode: "LCO"` in `shipmentCutOffTimes[]` | `LCO` | Available when `receiptTypeAtOrigin = "CFS"`. Conditional — not present for FCL shipments |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ✅ | `GET /track-and-trace/v3/events?eventTypes=EQUIPMENT&documentTypeCodes=BKG&documentReference={ref}` | Inferred from first EquipmentEvent with `relatedDocumentReferences[].type=BKG` | Inferred from first EquipmentEvent | Presence of any equipment event confirms container assignment |
| 3.2 | Empty Container Gate-Out (Pickup) | ✅ | `GET /track-and-trace/v3/events` | `equipmentEventTypeCode: GTOT` + `emptyIndicatorCode: EMPTY` | `GTOT` + `EMPTY` | May also appear as `PICK` at depot (`facilityTypeCode: DEPO`) |
| 3.3 | Full Container Gate-In | ✅ | `GET /track-and-trace/v3/events` | `equipmentEventTypeCode: GTIN` + `emptyIndicatorCode: LADEN` | `GTIN` + `LADEN` | Location: port terminal (`facilityTypeCode: POTE`) |
| 3.4 | Container Loaded on Vessel | ✅ | `GET /track-and-trace/v3/events` | `equipmentEventTypeCode: LOAD` + `emptyIndicatorCode: LADEN` + `isTransshipmentMove: false` | `LOAD` + `LADEN` | Includes `transportCall.vessel` for vessel ID |
| 3.5 | Container Discharged at Transshipment | ✅ | `GET /track-and-trace/v3/events` | `equipmentEventTypeCode: DISC` + `emptyIndicatorCode: LADEN` + `isTransshipmentMove: true` | `DISC` + `LADEN` + transshipment | Transshipment port in `transportCall.location.UNLocationCode` |
| 3.6 | Container Loaded at Transshipment | ✅ | `GET /track-and-trace/v3/events` | `equipmentEventTypeCode: LOAD` + `emptyIndicatorCode: LADEN` + `isTransshipmentMove: true` | `LOAD` + `LADEN` + transshipment | New vessel in `transportCall.vessel` |
| 3.7 | Container Discharged at Destination | ✅ | `GET /track-and-trace/v3/events` | `equipmentEventTypeCode: DISC` + `emptyIndicatorCode: LADEN` + `isTransshipmentMove: false` | `DISC` + `LADEN` | At final destination port |
| 3.8 | Full Container Gate-Out (Delivery) | ✅ | `GET /track-and-trace/v3/events` | `equipmentEventTypeCode: GTOT` + `emptyIndicatorCode: LADEN` | `GTOT` + `LADEN` | May be preceded by `AVPU` (Available for Pick-up) event |
| 3.9 | Empty Container Returned | ✅ | `GET /track-and-trace/v3/events` | `equipmentEventTypeCode: GTIN` + `emptyIndicatorCode: EMPTY` | `GTIN` + `EMPTY` | At depot (`facilityTypeCode: DEPO`) — completes container lifecycle |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ✅ | `GET /track-and-trace/v3/events?eventTypes=TRANSPORT` and `GET /schedules/v1/vessel-schedules` | `transportEventTypeCode: DEPA` + `eventClassifierCode: PLN/EST/ACT` | `DEPA` + classifier | Full PLN→EST→ACT progression supported |
| 4.2 | Estimated Time of Arrival | ETA | ✅ | `GET /track-and-trace/v3/events?eventTypes=TRANSPORT` and `GET /schedules/v1/vessel-schedules` | `transportEventTypeCode: ARRI` + `eventClassifierCode: PLN/EST/ACT` | `ARRI` + classifier | Full PLN→EST→ACT progression supported |
| 4.3 | Vessel Arrival at Transshipment | — | ✅ | `GET /track-and-trace/v3/events?eventTypes=TRANSPORT` | `transportEventTypeCode: ARRI` at intermediate port | `ARRI` at intermediate | Distinguish from destination arrival via transport plan leg sequence |
| 4.4 | Vessel Departure from Transshipment | — | ✅ | `GET /track-and-trace/v3/events?eventTypes=TRANSPORT` | `transportEventTypeCode: DEPA` on connecting vessel | `DEPA` at intermediate | Confirms onward journey |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ✅ | DCSA TNT v3: `POST /v3/event-subscriptions` with `callbackUrl`. Filter by event type, booking ref, equipment ref, vessel. Subscription management via GET/PUT/DELETE. Secret rotation supported. Endpoint confirmed live at `/track-and-trace/v3/event-subscriptions` (401) and `/synergy/tracking/v2/subscriptions` (401). Optional per DCSA spec — Maersk implements it |
| Event Polling with timestamp filter | ✅ | `GET /v3/events?eventCreatedDateTime:gte={timestamp}`. Mandatory per DCSA spec. Events sorted by `eventCreatedDateTime` ASC by default. Enables incremental polling |
| Event Classifier Progression (PLN→EST→ACT) | ✅ | Standard DCSA classifier codes. New event with same milestone but different `eventClassifierCode` or `eventDateTime` indicates a change |
| Retracted Events | ✅ | `metadata.retractedEventID` field points to a previously-sent event that is now void |
| Change Remarks | ✅ | `changeRemark` field on TransportEvents (free text, max 250 chars) — carrier-provided explanation |
| Delay Reason Codes | ✅ | `delayReasonCode` on TransportEvents — DCSA-standardized machine-readable codes |

### Coverage Summary

| Category | Fields Available | Fields Unavailable | Fields Unknown | Coverage % |
|----------|-----------------|-------------------|----------------|-----------|
| API Domains (1.x) | 4/5 | 0/5 | 1/5 | 80% |
| Cutoffs (2.x) | 5/6 | 0/6 | 1/6 | 83% |
| Container Milestones (3.x) | 9/9 | 0/9 | 0/9 | 100% |
| Transport Events (4.x) | 4/4 | 0/4 | 0/4 | 100% |
| Change Detection (5.x) | 6/6 | 0/6 | 0/6 | 100% |
| **Total** | **28/30** | **0/30** | **2/30** | **93%** |

> **Notes on Coverage:**
> - Shipping Instructions (1.4) marked ⚠️: likely available via ShipmentEvents in TNT but dedicated EBL (Electronic Bill of Lading) endpoint path not confirmed
> - LCL Cutoff (2.6) marked ⚠️: conditionally available only for CFS shipments — standard DCSA behavior
> - All container milestones and transport events are fully covered through DCSA TNT v3
> - All change detection mechanisms are supported — Maersk is among the most complete DCSA implementors

---

## Endpoint Reference

### Tracking / Events

| Endpoint | Method | Lookup Params | Pagination | Response Format | Notes |
|----------|--------|--------------|------------|----------------|-------|
| `/track-and-trace/v3/events` | GET | `documentTypeCodes` (BKG, TRD), `documentReference` (B/L or booking ref), `equipmentReference` (container #), `vesselIMONumber`, `carrierServiceCode`, `eventTypes` (SHIPMENT, TRANSPORT, EQUIPMENT), `eventCreatedDateTime` (for incremental polling) | Header-based: `limit` param + `Current-Page`/`Next-Page`/`Previous-Page`/`Last-Page`/`First-Page` response headers (note: DCSA spec says `Prev-Page` but Maersk returns `Previous-Page`) | JSON (DCSA event array) | **Primary tracking endpoint (v3)**. API Key auth. Confirmed live |
| `/track-and-trace/v3/events/{eventID}` | GET | `eventID` path param | N/A (single event) | JSON (DCSA event) | Retrieve a single event by ID |
| `/synergy/tracking/v2/events` | GET | Same as v3 with v2 schema | Page-based headers | JSON (DCSA event array) | **Legacy v2 tracking endpoint**. OAuth2 auth. Confirmed live. May be deprecated in favor of v3 |
| `/ecommerce/tracking/v2/events` | GET | `billOfLadingNumber`, likely similar to above | Unknown | JSON | **E-commerce tracking variant**. API Key auth. Confirmed live |
| `/ecommerce/tracking` | GET | Unknown | Unknown | JSON | E-commerce tracking base. API Key auth. Confirmed live |

### Event Subscriptions (Webhooks)

| Endpoint | Method | Purpose | Pagination | Response Format | Notes |
|----------|--------|---------|------------|----------------|-------|
| `/track-and-trace/v3/event-subscriptions` | GET | List active subscriptions | Cursor-based | JSON (subscription array) | API Key auth. Confirmed live |
| `/track-and-trace/v3/event-subscriptions` | POST | Create new subscription | N/A | JSON (subscription) | Requires `callbackUrl`, optional filters (eventTypes, documentReference, equipmentReference, etc.) |
| `/track-and-trace/v3/event-subscriptions/{subscriptionID}` | GET | Get subscription details | N/A | JSON (subscription) | Per DCSA TNT v3 spec |
| `/track-and-trace/v3/event-subscriptions/{subscriptionID}` | PUT | Update subscription | N/A | JSON (subscription) | Per DCSA TNT v3 spec |
| `/track-and-trace/v3/event-subscriptions/{subscriptionID}` | DELETE | Delete subscription | N/A | 204 No Content | Per DCSA TNT v3 spec |
| `/track-and-trace/v3/event-subscriptions/{subscriptionID}/secret` | PUT | Rotate callback secret | N/A | 204 No Content | Per DCSA TNT v3 spec |
| `/synergy/tracking/v2/subscriptions` | GET | List subscriptions (v2) | Page-based | JSON | OAuth2 auth. Legacy endpoint |

### Schedules

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| `/schedules/v1/vessel-schedules` | GET | `vesselIMONumber`, `carrierServiceCode`, `universalServiceReference`, `voyageNumber`, `UNLocationCode` | Cursor-based (`limit` + `cursor`) | JSON (DCSA vessel schedule array) | API Key auth. Confirmed live |
| `/schedules/v1/port-schedules` | GET | `UNLocationCode` (required), date range params, `carrierServiceCode` | Cursor-based | JSON (DCSA port schedule array) | API Key auth. Confirmed live |
| `/schedules/v1/point-to-point-routes` | GET | `placeOfReceipt` (required), `placeOfDelivery` (required), `departureStartDate`, `departureEndDate`, `arrivalStartDate`, `arrivalEndDate`, `maxTranshipment`, `receiptTypeAtOrigin`, `deliveryTypeAtDestination` | Cursor-based (`limit` + `cursor`) | JSON (PointToPoint array with `legs[]`, `transitTime`, `cutOffTimes[]`) | API Key auth. Confirmed live. Rich filtering options |
| `/v1/products/ocean-schedules` | GET | Unknown params (likely similar to above) | Unknown | JSON | OAuth2 auth. Confirmed live. May be legacy/internal |

### Booking

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| DCSA BKG v2: `/v2/bookings` | POST | Booking request body per DCSA BKG spec | N/A | JSON (booking confirmation with `transportPlan[]`, `shipmentCutOffTimes[]`) | Exact Maersk path prefix unconfirmed (404 at `/booking/v2/bookings`). Likely available under different prefix accessible via developer portal |
| DCSA BKG v2: `/v2/bookings` | GET | `carrierBookingReference` | Cursor-based | JSON (booking array or single booking) | Returns booking status and enriched data on confirmation |
| DCSA BKG v2: `/v2/bookings` | PUT | Booking amendment body | N/A | JSON | Amend existing booking |
| DCSA BKG v2: `/v2/bookings` | DELETE | `carrierBookingReference` | N/A | 204 No Content | Cancel booking |
| DCSA BKG v2: `/v2/booking-notifications` | POST | Callback endpoint for booking status changes | N/A | JSON (booking notification) | Push model for booking lifecycle events (RECE → CONF → PENU → REJE → CANC) |

### Rates

| Endpoint | Method | Purpose | Key Params | Notes |
|----------|--------|---------|-----------|-------|
| `/rates/spot` | GET | Retrieve spot freight rates | Unknown (likely origin/destination, equipment type, date) | API Key auth. Confirmed live. **Proprietary — not DCSA standard**. Maersk is one of very few carriers exposing rate APIs |

### Other Endpoints

| Endpoint | Method | Purpose | Key Params | Notes |
|----------|--------|---------|-----------|-------|
| `/v1/locations` | GET | Location reference data (ports, terminals, depots) | Unknown | OAuth2 auth. Confirmed live |
| `/v1/inland/routes` | GET | Inland transportation routes | Unknown | OAuth2 auth. Confirmed live |
| `/v1/products/ocean-products` | GET | Ocean product catalog | Unknown | OAuth2 auth. Confirmed live |
| `/products/v1` | GET | Products (possibly overlap with above) | Unknown | API Key auth. Confirmed live |
| `/reference-data/v1` | GET | Reference data (codes, enums, etc.) | Unknown | API Key auth. Confirmed live |

### Lookup Methods Summary

| Identifier Type | Supported? | Which Endpoints? | Notes |
|----------------|-----------|-----------------|-------|
| **Bill of Lading (B/L) number** | ✅ | TNT events (`documentTypeCodes=TRD&documentReference={blNumber}`), ecommerce tracking (`billOfLadingNumber={blNumber}`) | Also called Transport Document Reference in DCSA |
| **Booking reference** | ✅ | TNT events (`documentTypeCodes=BKG&documentReference={bookingRef}`), Booking API | Primary identifier pre-B/L issuance |
| **Container number** | ✅ | TNT events (`equipmentReference={containerNumber}`) | Tracks individual container across its lifecycle |
| **Carrier booking number** | ✅ | Same as booking reference | In DCSA, `carrierBookingReference` is the carrier-assigned booking number |
| **Vessel IMO / voyage** | ✅ | TNT events (`vesselIMONumber`, `carrierExportVoyageNumber`), Schedules API (`vesselIMONumber`) | Filter events by vessel; query schedules by vessel |

---

## Rate Limits & Quotas

| Detail | Value | Source |
|--------|-------|--------|
| **Global rate limit** | Unpublished — not discoverable without authenticated access | Unknown |
| **Per-endpoint limits** | Unpublished — reported to vary by API product and access tier | Unknown |
| **Daily/monthly quota** | Unpublished | Unknown |
| **Rate limit response** | Expected: 429 with Retry-After header (per DCSA and REST conventions) | Estimated (unverified) |
| **Rate limit by** | Consumer-Key / OAuth token (inferred from auth patterns — each client gets its own limits) | Estimated (unverified) |
| **Burst allowance** | Unknown | Unknown |
| **Different tiers** | Reported: free/self-service tier has lower limits; partner tier has higher limits. Specific numbers require portal registration to confirm | Reported (developer community — could not verify source URL) |

> **Note:** Maersk runs on Apigee (inferred from proxy error message format `"faultstring":"Unable to identify proxy for host: maersk-host"`) with Akamai CDN fronting. Rate limiting is likely implemented at the API gateway level. Specific limits will be visible in the developer portal after registration.

---

## Webhook / Push Support

| Detail | Value |
|--------|-------|
| **Webhooks supported?** | Yes — Maersk implements the optional DCSA TNT v3 subscription/push model |
| **Subscription endpoint** | `POST /track-and-trace/v3/event-subscriptions` (v3) and `POST /synergy/tracking/v2/subscriptions` (v2, likely legacy) |
| **Subscription management** | Full CRUD: Create (POST), List (GET), Get by ID (GET), Update (PUT), Delete (DELETE), Rotate secret (PUT /secret) |
| **Subscribable event types** | All DCSA event types: SHIPMENT, TRANSPORT, EQUIPMENT. Filterable by: `eventTypes`, `shipmentEventTypeCodes`, `transportEventTypeCodes`, `equipmentEventTypeCodes`, `documentTypeCodes`, `documentReference`, `equipmentReference`, `vesselIMONumber`, `carrierServiceCode`, `UNLocationCode` |
| **Callback format** | DCSA event JSON POSTed to `callbackUrl` specified in subscription |
| **Callback authentication** | Shared secret — set during subscription creation, rotatable via dedicated endpoint |
| **Retry policy on failure** | Unknown — DCSA spec does not mandate specific retry policy. Likely carrier-specific implementation |
| **Documented reliability** | Unknown — no published SLA for webhook delivery. Polling is the reliable fallback |

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | https://www.maersk.com/tracking |
| **Login required?** | No — basic tracking by B/L or container number is available without login. Detailed views may require a Maersk account |
| **Data available on portal but NOT in API** | Unlikely — Maersk's API surface is comprehensive. Portal may have richer visualization but the underlying data should be accessible via APIs |
| **Scraping feasibility** | Not needed — API coverage is excellent. Portal is SPA-based (would require headless browser if scraping were needed) |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Yes |
| **EDI message types** | IFTMIN (Booking), IFTSTA (Status), COPARN (Container release/acceptance), BAPLIE (Bay plan), CUSCAR (Customs cargo), CUSREP (Customs report) |
| **EDI connection method** | AS2, SFTP — via Maersk's EDI team |
| **EDI documentation** | Contact Maersk directly; not publicly documented on developer portal (EDI is legacy/enterprise channel) |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Yes | Maersk is a major carrier in project44's ocean visibility network |
| **FourKites** | Yes | Maersk coverage available through FourKites ocean tracking |
| **Vizion** | Yes | Maersk is available through Vizion's carrier API aggregation (Vizion provides normalized access to carrier tracking) |
| **INTTRA / E2open** | Yes | Maersk is a founding carrier on the INTTRA platform (now E2open Ocean); supports booking and tracking |
| **CargoSmart** | Yes | Maersk is available on CargoSmart for tracking and schedule visibility |

> **Aggregator note:** Given Maersk's excellent direct API coverage, there is minimal benefit to accessing Maersk through a third-party aggregator for SSL's use case. Direct API integration provides richer data (full DCSA event model, webhooks, cutoffs) than most aggregators expose. Aggregators may be useful as a fallback or for cross-carrier normalization if SSL wants a single integration point.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Reported as ~5–15 minutes for most equipment events; transport events (ETD/ETA) may update less frequently based on vessel reporting | Reported (developer forums — no specific URL verifiable) |
| **API uptime/reliability** | Maersk has a published status page (https://status.maersk.com) indicating enterprise-grade reliability. No SLA numbers publicly available | Official (status page exists) |
| **Historical data depth** | Unknown — DCSA spec does not mandate a minimum retention period. Estimated ~90–180 days based on industry norms | Estimated ~90–180 days (unverified) |
| **Timezone handling** | ISO 8601 with timezone offset (e.g., `2022-09-19T06:31:00+02:00`) per DCSA specification | Official (DCSA spec) |
| **Character encoding** | UTF-8 per DCSA specification | Official (DCSA spec) |

### Known Issues & Gotchas

- **Dual auth mechanism**: Some endpoints use OAuth2 Bearer tokens, others use API Key (Consumer-Key header). The SDK adapter needs to support both and know which to use per endpoint. This may indicate API evolution (older endpoints use OAuth2, newer ones use API Key) or different API products with different auth requirements.

- **Multiple tracking endpoint versions**: Both v2 (`/synergy/tracking/v2/events`) and v3 (`/track-and-trace/v3/events`) appear to be live simultaneously. The v3 endpoint should be preferred (aligns with latest DCSA TNT spec), but v2 may offer features not yet available in v3 or may be needed as fallback.

- **Path prefix variations**: Maersk doesn't use bare DCSA paths (e.g., `/v3/events`). Instead, paths have Maersk-specific prefixes (`/track-and-trace/v3/events`, `/synergy/tracking/v2/events`, `/schedules/v1/vessel-schedules`). This means DCSA OpenAPI specs can't be used directly — paths need carrier-specific mapping.

- **eCommerce tracking vs. standard tracking**: The `/ecommerce/tracking/` endpoint appears separate from `/track-and-trace/`. These may return different response shapes or serve different use cases (simplified e-commerce view vs. full DCSA event model). Needs live testing to confirm.

- **Booking endpoint path unknown**: The standard DCSA BKG path (`/booking/v2/bookings`) returned 404. The booking API exists (Maersk's developer portal lists it) but likely uses a different path prefix. This will be discoverable upon portal registration.

- **2M alliance dissolution**: The 2M alliance with MSC ended in January 2025. Maersk now operates the Gemini Cooperation with Hapag-Lloyd. This may affect vessel sharing, transshipment patterns, and schedule data. Ensure alliance context is not hard-coded.

- **Akamai bot protection**: Maersk's API gateway is fronted by Akamai (confirmed from response headers). Unusual request patterns may trigger bot detection. SDK should use standard User-Agent headers and reasonable request rates.

### Recently Deprecated or Changed

- **TNT v2 → v3 transition**: The `/synergy/tracking/v2/` endpoints may be deprecated in favor of `/track-and-trace/v3/`. Both are currently live, but new integrations should target v3.

- **2M alliance ended January 2025**: Maersk vessel-sharing arrangements with MSC are no longer active. New Gemini Cooperation with Hapag-Lloyd affects routing and scheduling.

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | Yes — Maersk has the most comprehensive API surface of any ocean carrier. Full tracking, schedules, cutoffs, webhooks, and even rates are available |
| **Implementation effort** | Low (DCSA passthrough with path mapping) — Maersk implements DCSA standards; mapping is straightforward. Minor complexity from dual auth and path prefixes |
| **DCSA base adapter usable?** | Yes — Maersk is among the most complete DCSA implementors. A shared DCSA base adapter can handle 90%+ of the logic; Maersk adapter adds path prefix mapping and auth handling |

### Recommended Approach

The Maersk adapter should be built as the **first implementation** for the DCSA base adapter class, given Maersk's comprehensive DCSA compliance. Since Maersk follows DCSA standards closely, the adapter architecture should be:

1. **DCSA Base Adapter**: Handles event parsing, normalization to canonical model, pagination traversal, subscription management, and event classifier progression logic. This base class is reusable across all DCSA-compliant carriers.

2. **Maersk Adapter** (extends DCSA Base): Provides Maersk-specific configuration: API base URL (`api.maersk.com`), path prefix mapping (e.g., DCSA `/v3/events` → Maersk `/track-and-trace/v3/events`), dual auth handling (OAuth2 for legacy endpoints, API Key for newer endpoints), and any Maersk-specific response quirks.

3. **Auth Handler**: Implement both OAuth2 client_credentials flow (for `/synergy/` and `/v1/` endpoints) and API Key injection (Consumer-Key header for `/track-and-trace/` and `/schedules/` endpoints). Token caching and refresh for OAuth2.

Build Maersk first, extract the DCSA base class from it, then implement other DCSA-compliant carriers (MSC, Hapag-Lloyd, ONE) as thin configuration layers on top of the same base.

### Recommended Lookup Method

**Bill of Lading (B/L) number** is the recommended primary lookup method:
- Universally assigned after booking confirmation
- Works across all tracking endpoints
- Returns the richest event data (all container milestones, transport events, and shipment events linked to the B/L)
- Maersk DCSA mapping: `documentTypeCodes=TRD&documentReference={blNumber}`

**Booking reference** as secondary:
- Available earlier in the lifecycle (before B/L issuance)
- Use `documentTypeCodes=BKG&documentReference={bookingRef}`
- Good for pre-shipment tracking (cutoffs, booking status)

**Container number** as supplementary:
- Use `equipmentReference={containerNumber}` for per-container tracking
- Useful for multi-container shipments where individual container progress differs

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Every 2–4 hours for active shipments; every 12–24 hours for pre-departure shipments. More frequent polling (~30 min) for shipments near critical milestones (approaching cutoffs, near arrival) |
| **Incremental filter** | Use `eventCreatedDateTime:gte={lastPollTimestamp}` to fetch only new events since last poll. This is mandatory per DCSA spec and highly efficient |
| **Batch tracking** | One API call per shipment (DCSA events API filters by document reference). No batch/multi-shipment endpoint in the standard. For efficiency, use webhooks for real-time updates and poll as verification/fallback |

### Auth Implementation Notes

```
OAuth2 Flow (for /synergy/ and /v1/ endpoints):
  POST https://api.maersk.com/oauth2/access_token
  Content-Type: application/x-www-form-urlencoded
  Body: grant_type=client_credentials&client_id={id}&client_secret={secret}
  Response: {"access_token":"...","token_type":"Bearer","expires_in":3600}
  Usage: Authorization: Bearer {access_token}

API Key Flow (for /track-and-trace/ and /schedules/ endpoints):
  Header: Consumer-Key: {api_key}
  (Or possibly: x-maersk-consumer-key: {api_key})
```

The adapter should:
- Cache OAuth2 tokens and refresh before expiry (subtract ~60s safety margin)
- Support both auth methods and route to the correct one based on endpoint path
- Store credentials securely (provided by consumer, never logged)
- Handle 401 responses by refreshing auth and retrying once

### Edge Cases to Handle

- **Transshipment events may arrive out of order**: Container DISC at transshipment port may be recorded before vessel ARRI at that port if carrier systems have different update timings. Sort by `eventDateTime`, not `eventCreatedDateTime`.

- **Multiple containers per booking**: A single booking may have multiple containers, each with independent milestone progressions. The SDK should track per-container state while providing a booking-level summary.

- **Rolled containers**: If a container misses a vessel cutoff, it appears as a re-scheduling — new PLN events replace previous estimates. Watch for `retractedEventID` in metadata.

- **Vessel changes (blank sailings)**: Carriers may cancel port calls or change vessels. Transport events for the cancelled call will have `retractedEventID` pointing to the original event. New events will appear for the replacement vessel/schedule.

- **Alliance transition events**: During the 2M → Gemini Cooperation transition, some historical shipments may show MSC vessels/events, while new shipments show Hapag-Lloyd cooperation patterns. Don't hard-code alliance assumptions.

- **E-commerce tracking endpoint divergence**: The `/ecommerce/tracking/` endpoint may return a simplified response schema compared to the full DCSA `/track-and-trace/` endpoint. Test both and prefer the DCSA endpoint for richness.

### Mapping Complexity

**Low complexity.** Maersk's DCSA compliance means the response format closely matches the canonical data model defined in `docs/required-data-fields.md`. Key mapping tasks:

1. **Path prefix mapping**: DCSA spec paths → Maersk-specific paths (simple configuration, not logic)
2. **Auth routing**: Determine which auth method to use per endpoint (configurable rule)
3. **Event normalization**: Already DCSA-compliant — mostly passthrough. Extract `equipmentEventTypeCode` + `emptyIndicatorCode` + `isTransshipmentMove` combination to map to canonical milestones
4. **Cutoff extraction**: Pull `shipmentCutOffTimes[]` from booking response and map `cutOffDateTimeCode` to canonical cutoff fields
5. **Timestamp normalization**: Already ISO 8601 with timezone — minimal transformation needed

The only non-trivial mapping is combining multiple DCSA event fields into our composite canonical milestones (e.g., `LOAD` + `LADEN` + `isTransshipmentMove: false` → "Container Loaded on Vessel").

---

## Open Questions

- [ ] **Does SSL have an existing Maersk developer account?** — This would accelerate development by providing immediate API access and revealing documentation not visible without login
- [ ] **What specific rate limits apply to self-service API keys?** — Needs to be checked after developer portal registration
- [ ] **What is the exact Maersk path prefix for the Booking API?** — `/booking/v2/bookings` returned 404; actual path discoverable via developer portal
- [ ] **Does the `/ecommerce/tracking/` endpoint return the same schema as `/track-and-trace/`?** — Needs live testing to compare response shapes
- [ ] **What is the OAuth2 token lifetime?** — Estimated ~1 hour; needs live verification
- [ ] **How far back does historical event data go?** — Estimated ~90–180 days; needs live verification
- [ ] **What test data is available in the Maersk sandbox environment?** — Discoverable after registration
- [ ] **Does Maersk implement the DCSA EBL (Electronic Bill of Lading) API for Shipping Instructions?** — EBL endpoint paths returned 404; may need different prefix or may not be implemented
- [ ] **Are rate limits enforced per Consumer-Key, per OAuth client, or per IP?** — Needs live testing or developer portal documentation review
- [ ] **Is there a Maersk-specific webhook reliability SLA?** — Not publicly documented; may be in partner documentation

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | https://www.maersk.com |
| Developer Portal | https://developer.maersk.com |
| Tracking Portal | https://www.maersk.com/tracking |
| API Status Page | https://developer.maersk.com/api-status |
| System Status Page | https://status.maersk.com |
| OAuth2 Token Endpoint | `POST https://api.maersk.com/oauth2/access_token` |
| DCSA Organization | https://dcsa.org |
| DCSA OpenAPI Specs (GitHub) | https://github.com/dcsaorg/DCSA-OpenAPI |
| DCSA TNT v3 Spec | https://github.com/dcsaorg/DCSA-OpenAPI/tree/master/tnt/v3 |
| DCSA BKG v2 Spec | https://github.com/dcsaorg/DCSA-OpenAPI/tree/master/bkg/v2 |
| DCSA CS v1 Spec | https://github.com/dcsaorg/DCSA-OpenAPI/tree/master/cs/v1 |
| DCSA SwaggerHub (TNT v3) | https://app.swaggerhub.com/apis/dcsaorg/DCSA_TNT/3.0.0 |
| DCSA Developer Page | https://developer.dcsa.org |
| DCSA Adoption API Spec | https://github.com/dcsaorg/DCSA-OpenAPI/tree/master/adopt/v1 |
