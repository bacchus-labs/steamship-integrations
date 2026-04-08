# Evergreen Line — API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only — not verified with live API testing. Research based on the ShipmentLink API Developer Portal (publicly accessible Swagger/OpenAPI specifications), DCSA membership records, FAQ documentation, published event examples, and public web presence. No API credentials were obtained or used.
> **Researched by**: Agent (carrier API audit workflow)
> **Date**: 2026-02-11
> **Last verified**: 2026-02-11

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | Evergreen Marine Corporation (Evergreen Line) |
| **SCAC Code** | EGLV |
| **Parent Company** | Evergreen Group (publicly traded, Taiwan) |
| **Alliance** | Ocean Alliance (with CMA CGM, COSCO, OOCL) |
| **Primary Services** | Container shipping (fully containerized — no RoRo or bulk) |
| **Market Position** | 7th largest container carrier globally by TEU capacity. One of the "big 7" carriers. Operates ~200 container vessels |
| **Headquarters** | Taoyuan City, Taiwan |
| **Website** | [https://www.evergreen-line.com](https://www.evergreen-line.com) |

### Evergreen Group — Relevant Digital Entities

| Entity | Role | Digital Infrastructure |
|--------|------|----------------------|
| **Evergreen Line** | Ocean carrier brand and operations | Main website at evergreen-line.com |
| **ShipmentLink** | Evergreen's e-Commerce / digital services platform | shipmentlink.com — hosts API portal, cargo tracking, booking, B/L services |
| **Evergreen Marine Corporation** | Legal entity / corporate parent | Corporate site at evergreen-marine.com |

> **Note on ShipmentLink**: ShipmentLink is Evergreen's dedicated digital services platform. All API documentation, developer registration, EDI services, and web-based tracking are hosted at `shipmentlink.com`. ShipmentLink is **not** a third-party platform — it is Evergreen's own e-commerce subsidiary/division.

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | **Yes** |
| **Developer portal URL** | [https://www.shipmentlink.com/_ec/APIPORTAL_Home](https://www.shipmentlink.com/_ec/APIPORTAL_Home) |
| **API documentation URL(s)** | [API Service Category](https://www.shipmentlink.com/_ec/APIPORTAL_APIServiceCategory) — lists all APIs with links to Swagger UIs |
| **Documentation quality** | **Good** — Swagger/OpenAPI specs published for all 4 API categories, with example payloads. Portal includes FAQ with registration and authentication guidance. Not as polished as Maersk's developer.maersk.com but functional and complete |
| **OpenAPI/Swagger spec available?** | Yes — embedded in Swagger UI pages. TNT uses Swagger 2.0; Booking, SI, and CS use OpenAPI 3.0.3 |
| **Sandbox/test environment?** | Unknown — FAQ mentions a "testing" phase before go-live, but no separate sandbox URL is documented. Testing appears to be done against production or a pre-production environment arranged during onboarding |
| **Developer registration** | **Requires application and approval** — form on API Portal website, verified by Evergreen staff. Not self-service |
| **Developer support channels** | Contact via API Portal (contact page requires login); general inquiries via ShipmentLink customer service |
| **Community/third-party libraries** | **None found** — no GitHub repos, npm packages, or PyPI packages for Evergreen/ShipmentLink API integration |
| **API changelog / release notes** | Not published as a standalone page. Swagger spec pages show version and "Last Updated" dates |

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | **Yes — founding member** (one of 9 carriers that established DCSA in April 2019, alongside MSC, Maersk, CMA CGM, Hapag-Lloyd, ONE, Yang Ming, HMM, and ZIM) |
| **DCSA APIs implemented** | **Track & Trace (TNT), Booking (BKG), Shipping Instructions (eDocumentation), Commercial Schedules (CS)** — full suite |
| **DCSA TNT version** | **v2.2** (Swagger 2.0 format). Last updated 2023-11-15. Note: this is an older version; DCSA TNT v3 is the current standard |
| **DCSA Booking version** | **v2.0.0** (OpenAPI 3.0.3). Last updated 2025-03-18. Aligns with current DCSA Booking v2 standard |
| **DCSA Shipping Instructions version** | **v3.0.0** (OpenAPI 3.0.3). Last updated 2025-04-17. Aligns with current DCSA eDocumentation standard |
| **DCSA Commercial Schedules version** | **v1.0.0** (OpenAPI 3.0.3). Last updated 2025-03-08. Aligns with current DCSA CS v1 standard |
| **Known DCSA deviations** | TNT API is on v2.2 rather than v3 — key structural differences include: (1) v2 uses a single `/events` endpoint with `eventType` discriminator vs. v3's separate event endpoints; (2) v2 lacks `isTransshipmentMove` field; (3) v2 uses `eventClassifierCode: "PLAN"` in some examples where the DCSA standard uses `"PLN"`. Booking, SI, and CS appear to follow current DCSA versions |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Yes | EDI services available via ShipmentLink ([EDI Register](https://www.shipmentlink.com/tam1/jsp/TAM1_EdiRegisterNotice.jsp)). Specific message types not documented on the public-facing pages |
| **INTTRA integration** | Unknown | Not confirmed; Evergreen is a major carrier and likely available on INTTRA/E2open but could not verify from public sources |
| **BIC (Bureau International des Containers)** | Yes | Container IDs in API examples follow BIC ISO 6346 format (e.g., EISU, EITU, EMCU prefixes) |
| **UN/LOCODE** | Yes | Used throughout APIs — `UNLocationCode` field in TNT events, `placeOfReceipt`/`placeOfDelivery` in CS |
| **SMDG** | Yes | `facilityCodeListProvider: "SMDG"` used throughout TNT events for terminal identification |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | **JWT (JSON Web Token)** — Client ID + Secret exchanged for a JWT token |
| **Auth documentation** | [FAQ page](https://www.shipmentlink.com/_ec/APIPORTAL_FAQ) — FAQ items 1 and 3 describe the process |
| **Registration process** | 1. Fill in API service application form on the API Portal website (company info, requested services, business scope). 2. Evergreen verifies the application. 3. Upon approval, receive service confirmation with Client ID, Secret, Token URL, and Event URL |
| **Registration URL** | Registration link visible on API Portal when logged in (the `APIPORTAL_Register` action is behind authentication) |
| **Partner program required?** | **Yes — for any access**. Registration requires application review and business verification |
| **Partner program URL** | Through the API Portal registration flow |
| **Credential type** | Client ID + Client Secret → exchanged for JWT token |
| **Token refresh supported?** | Yes — JWT tokens have a limited lifetime; new tokens are obtained by re-authenticating with Client ID/Secret |
| **Token lifetime** | Unknown — not documented in FAQ |
| **Access tiers** | Single tier (Track & Trace is free; pricing for other APIs not documented) |
| **IP whitelisting required?** | **Yes** — FAQ item 4 states: "Please make sure your IP address is the same as the one filled in your requirement form" |

### Access Requirements Summary for SSL

SSL will need to submit an application through Evergreen's API Portal, providing company information and specifying which API services they wish to use. This is not self-service — Evergreen's team reviews and approves applications. The approval process timeline is unclear. Upon approval, SSL will receive a Client ID, Client Secret, Token URL, and Event URL. SSL must also provide the IP address(es) from which API calls will be made, as IP whitelisting is enforced. The Track & Trace API is explicitly stated to be free. Pricing for Booking, Shipping Instructions, and Commercial Schedules APIs is not documented.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field must have a row.
> ✅ = Available | ❌ = Not available | ⚠️ = Partial / limited | ❓ = Unknown

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ✅ | `GET /server/sol/mvs1api/commSch/v1/vessel`, `GET /server/sol/mvs1api/commSch/v1/port` | Vessel and port schedule endpoints | DCSA CS v1.0.0 | Full DCSA Commercial Schedules implementation |
| 1.2 | Point-to-Point Route Options | ✅ | `GET /server/sol/route/commercial/v1/point-to-point-routes` | `placeOfReceipt`, `placeOfDelivery`, routing options | DCSA CS v1.0.0 | Supports all DCSA query params: date ranges, carrier service code, max transshipments, receipt/delivery types |
| 1.3 | Booking Lifecycle | ✅ | `POST /dcsa/bookings`, `GET /dcsa/bookings/{ref}`, `PUT /dcsa/bookings/{ref}`, `PATCH /dcsa/bookings/{ref}` | Full CRUD + amendments + cancellations | DCSA BKG v2.0.0 | Full lifecycle: create, retrieve, update, cancel, amend. Includes booking notifications endpoint |
| 1.4 | Shipping Instructions | ✅ | `POST /v3/shipping-instructions`, `GET /v3/shipping-instructions/{ref}` | Full SI lifecycle including eBL | DCSA eDoc v3.0.0 | DCSA-compliant eBL support; covers SI submission, approval, rejection, issuance, surrender |
| 1.5 | Rates | ❌ | N/A | N/A | Not part of DCSA | No rate/quoting API found. Consistent with industry — rates typically handled via direct sales/email |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ✅ | CS point-to-point, Booking confirmation | `cutOffDateTimeCode: "ECP"` | `ECP` | Available in CS `cutOffTimes[]` array |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ✅ | CS point-to-point, Booking confirmation | `cutOffDateTimeCode: "EFC"` | `EFC` | Available in CS `cutOffTimes[]` array |
| 2.3 | Documentation Cutoff | DCO | ✅ | CS point-to-point, Booking confirmation | `cutOffDateTimeCode: "DCO"` | `DCO` | Available in CS `cutOffTimes[]` array |
| 2.4 | VGM Cutoff | VCO | ✅ | CS point-to-point, Booking confirmation | `cutOffDateTimeCode: "VCO"` | `VCO` | Available in CS `cutOffTimes[]` array |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ✅ | CS point-to-point, Booking confirmation | `cutOffDateTimeCode: "FCO"` | `FCO` | Confirmed in booking example: `"cutOffDateTimeCode": "FCO", "cutOffDateTime": "2025-04-05T17:30:00+08:00"` |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ✅ | CS point-to-point | `cutOffDateTimeCode: "LCO"` | `LCO` | Listed in CS spec. Condition: only when receipt type at origin is CFS |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ⚠️ | `GET /tnt/v2/events` | Inferred from first Equipment event with BKG document reference | Inferred from first EquipmentEvent | No explicit "assigned" event, but first equipment event confirms container is linked to booking |
| 3.2 | Empty Container Gate-Out (Pickup) | ✅ | `GET /tnt/v2/events` | `equipmentEventTypeCode: GTOT` + `emptyIndicatorCode: EMPTY` | `GTOT` + `EMPTY` | Confirmed via event examples and event list. Gate-out of empty by truck at port/inland terminal |
| 3.3 | Full Container Gate-In | ✅ | `GET /tnt/v2/events` | `equipmentEventTypeCode: GTIN` + `emptyIndicatorCode: LADEN` | `GTIN` + `LADEN` | Confirmed via event examples. Gate-in of laden by truck/rail at port/inland terminal |
| 3.4 | Container Loaded on Vessel | ✅ | `GET /tnt/v2/events` | `equipmentEventTypeCode: LOAD` + `emptyIndicatorCode: LADEN` | `LOAD` + `LADEN` | Confirmed via event examples. Load onto vessel/barge at port terminal |
| 3.5 | Container Discharged at Transshipment | ⚠️ | `GET /tnt/v2/events` | `equipmentEventTypeCode: DISC` + `emptyIndicatorCode: LADEN` | `DISC` + `LADEN` + transshipment | TNT v2.2 lacks `isTransshipmentMove` field. Transshipment must be inferred by correlating DISC events with the transport plan (intermediate ports). The event itself shows DISC at a port — consumer must determine if it's transshipment or final |
| 3.6 | Container Loaded at Transshipment | ⚠️ | `GET /tnt/v2/events` | `equipmentEventTypeCode: LOAD` + `emptyIndicatorCode: LADEN` | `LOAD` + `LADEN` + transshipment | Same transshipment inference limitation as 3.5 |
| 3.7 | Container Discharged at Destination | ✅ | `GET /tnt/v2/events` | `equipmentEventTypeCode: DISC` + `emptyIndicatorCode: LADEN` | `DISC` + `LADEN` | Confirmed. Discharge from vessel at port terminal. Consumer must match against destination to distinguish from transshipment |
| 3.8 | Full Container Gate-Out (Delivery) | ✅ | `GET /tnt/v2/events` | `equipmentEventTypeCode: GTOT` + `emptyIndicatorCode: LADEN` | `GTOT` + `LADEN` | Confirmed via event examples. Gate-out of laden by truck/rail at port terminal/ramp |
| 3.9 | Empty Container Returned | ✅ | `GET /tnt/v2/events` | `equipmentEventTypeCode: GTIN` + `emptyIndicatorCode: EMPTY` | `GTIN` + `EMPTY` | Confirmed via event examples. Gate-in of empty at port/depot |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ✅ | `GET /tnt/v2/events` + CS endpoints | `transportEventTypeCode: DEPA` + `eventClassifierCode: PLN/EST/ACT` | `DEPA` + classifier | Confirmed in event examples. Full PLN→EST→ACT progression supported. CS endpoints provide schedule-level ETDs |
| 4.2 | Estimated Time of Arrival | ETA | ✅ | `GET /tnt/v2/events` + CS endpoints | `transportEventTypeCode: ARRI` + `eventClassifierCode: PLN/EST/ACT` | `ARRI` + classifier | Confirmed in event examples. Full PLN→EST→ACT progression supported |
| 4.3 | Vessel Arrival at Transshipment | — | ⚠️ | `GET /tnt/v2/events` | `transportEventTypeCode: ARRI` at intermediate port | `ARRI` at intermediate | Available but requires transport plan correlation to identify transshipment ports (no `isTransshipmentMove` in v2.2) |
| 4.4 | Vessel Departure from Transshipment | — | ⚠️ | `GET /tnt/v2/events` | `transportEventTypeCode: DEPA` at intermediate port | `DEPA` at intermediate | Same limitation as 4.3 |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ✅ | `POST /tnt/v2/event-subscriptions` — create subscriptions with `callbackUrl`. Supports filtering by booking ref, equipment ref, carrier service code, event types. Full CRUD on subscriptions (GET/POST/PUT/DELETE) |
| Event Polling with timestamp filter | ✅ | `GET /tnt/v2/events` supports `eventCreatedDateTime` query parameter for incremental polling |
| Event Classifier Progression (PLN→EST→ACT) | ✅ | Events include `eventClassifierCode` with PLN/EST/ACT values. Transport events show progression through schedule lifecycle |
| Retracted Events | ❓ | Not confirmed in the v2.2 spec. DCSA v2 spec includes event retraction concept but unclear if Evergreen implements it |
| Change Remarks | ✅ | TransportEvent model includes `changeRemark` field (free text, for vessel operator schedule change explanations) |
| Delay Reason Codes | ✅ | TransportEvent model includes `delayReasonCode` field using SMDG delay reason codes |

### Coverage Summary

| Category | Fields Available | Fields Unavailable | Fields Partial/Unknown | Coverage % |
|----------|-----------------|-------------------|----------------|-----------|
| API Domains (1.x) | 4/5 | 1/5 | 0/5 | 80% |
| Cutoffs (2.x) | 6/6 | 0/6 | 0/6 | 100% |
| Container Milestones (3.x) | 6/9 | 0/9 | 3/9 | 67% (100% with inference) |
| Transport Events (4.x) | 2/4 | 0/4 | 2/4 | 50% (100% with inference) |
| Change Detection (5.x) | 4/6 | 0/6 | 2/6 | 67% |
| **Total** | **22/30** | **1/30** | **7/30** | **73% (97% with inference)** |

> **Note on "partial" fields**: The 7 partial/unknown fields are all functionally available — the data exists in the API. The limitation is that TNT v2.2 lacks the `isTransshipmentMove` discriminator, requiring the SDK adapter to infer transshipment vs. destination by correlating events with the transport plan. This is a mapping complexity issue, not a data availability issue. With proper inference logic, effective coverage reaches **97%** (only Rates at 1.5 is truly unavailable).

---

## Endpoint Reference

### Track & Trace (TNT v2.2)

| Endpoint | Method | Lookup Params | Pagination | Response Format | Notes |
|----------|--------|--------------|------------|----------------|-------|
| `/tnt/v2/events` | GET | `carrierBookingReference`, `transportDocumentReference` (B/L), `equipmentReference` (container), `carrierServiceCode`, `carrierContract` | Cursor-based (`cursor`, `limit`, `sort`) | JSON | Main tracking endpoint. Also filters by `eventType`, `equipmentEventTypeCode`, `transportEventTypeCode`, `shipmentEventTypeCode`, `documentTypeCode`, `eventCreatedDateTime`, `transportCallID` |
| `/tnt/v2/event-subscriptions` | GET | N/A (returns user's subscriptions) | Cursor-based (`cursor`, `limit`, `sort`) | JSON | List active subscriptions |
| `/tnt/v2/event-subscriptions` | POST | N/A | N/A | JSON | Create subscription with `callbackUrl` and optional filters |
| `/tnt/v2/event-subscriptions/{subscriptionID}` | GET | `subscriptionID` (path) | N/A | JSON | Get specific subscription |
| `/tnt/v2/event-subscriptions/{subscriptionID}` | PUT | `subscriptionID` (path) | N/A | JSON | Update subscription |
| `/tnt/v2/event-subscriptions/{subscriptionID}` | DELETE | `subscriptionID` (path) | N/A | JSON | Delete subscription |

### Booking (BKG v2.0.0)

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| `/dcsa/bookings` | POST | Request body (booking request) | N/A | JSON | Creates new booking. Returns `carrierBookingRequestReference` (e.g., `EGLV_25031700378628`) |
| `/dcsa/bookings/{bookingReference}` | GET | `bookingReference` (path), `amendedContent` (query, boolean) | N/A | JSON | Retrieves booking details. Includes `shipmentCutOffTimes[]`, `transportPlan[]` when confirmed |
| `/dcsa/bookings/{bookingReference}` | PUT | `bookingReference` (path) | N/A | JSON | Updates booking |
| `/dcsa/bookings/{bookingReference}` | PATCH | `bookingReference` (path) | N/A | JSON | Cancels booking or cancels an amendment |
| `/booking-notifications` | POST | N/A | N/A | JSON | Callback endpoint for carrier to push booking status notifications |

### Shipping Instructions (SI v3.0.0)

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| `/v3/shipping-instructions` | POST | Request body (shipping instruction) | N/A | JSON | Create shipping instructions |
| `/v3/shipping-instructions/{documentReference}` | GET | `documentReference` (path), `updatedContent` (query) | N/A | JSON | Retrieve shipping instructions |
| `/v1/events` | GET | Event query params | N/A | JSON | SI-related events (RECE, DRFT, PENA, APPR, ISSU, SURR, etc.) |

### Commercial Schedules (CS v1.0.0)

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| `/server/sol/route/commercial/v1/point-to-point-routes` | GET | `placeOfReceipt` (required), `placeOfDelivery` (required), `departureStartDate`, `departureEndDate`, `arrivalStartDate`, `arrivalEndDate`, `maxTranshipment`, `receiptTypeAtOrigin`, `deliveryTypeAtDestination` | Cursor-based (`cursor`, `limit`) | JSON | Returns routing options with legs, transit times, and cutoff times |
| `/server/sol/mvs1api/commSch/v1/port` | GET | `UNLocationCode` (required), `date`, `startDate`, `endDate`, `carrierServiceCode`, `vesselIMONumber`, `vesselName`, `vesselOperatorCarrierCode`, `facilitySMDGCode` | Cursor-based (`cursor`, `limit`) | JSON | Port schedules: vessels arriving/departing from a port |
| `/server/sol/mvs1api/commSch/v1/vessel` | GET | `vesselIMONumber`, `vesselName`, `carrierVoyageNumber`, `universalVoyageReference`, `carrierServiceCode`, `universalServiceReference` | Cursor-based (`cursor`, `limit`) | JSON | Vessel schedules: timetable for a specific vessel/service |

### Lookup Methods Summary

| Identifier Type | Supported? | Which Endpoints? | Notes |
|----------------|-----------|-----------------|-------|
| **Bill of Lading (B/L) number** | ✅ | TNT: `transportDocumentReference` param | Primary tracking identifier |
| **Booking reference** | ✅ | TNT: `carrierBookingReference` param; BKG: path param | Booking + tracking |
| **Container number** | ✅ | TNT: `equipmentReference` param | Equipment-level tracking |
| **Carrier booking number** | ✅ | BKG: `bookingReference` path param | Format: `EGLV_YYMMDDNNNNNNN` (e.g., `EGLV_25031700378628`). Note from FAQ: "EGLV" prefix is NOT needed in `transportDocumentReference` (B/L) param |
| **Vessel IMO / voyage** | ✅ | CS: `vesselIMONumber`, `carrierVoyageNumber` params | Schedule lookups only |

---

## Rate Limits & Quotas

| Detail | Value | Source |
|--------|-------|--------|
| **Global rate limit** | Unpublished | Unknown — no rate limit documentation found |
| **Per-endpoint limits** | Unpublished | Unknown |
| **Daily/monthly quota** | Unpublished | Unknown |
| **Rate limit response** | Unknown | Unknown — presumably standard HTTP 429 if limits exist |
| **Rate limit by** | Unknown | Unknown — likely per Client ID given JWT auth model |
| **Burst allowance** | Unknown | Unknown |
| **Different tiers** | Single tier — Track & Trace is free ([FAQ](https://www.shipmentlink.com/_ec/APIPORTAL_FAQ) item 9) | Official (FAQ) |

---

## Webhook / Push Support

| Detail | Value |
|--------|-------|
| **Webhooks supported?** | **Yes** — full DCSA subscription/callback model |
| **Subscription endpoint** | `POST /tnt/v2/event-subscriptions` |
| **Subscription management** | Full CRUD: Create (POST), List (GET), Get single (GET /{id}), Update (PUT /{id}), Delete (DELETE /{id}) |
| **Subscribable event types** | All event types: Equipment (GTIN, GTOT, LOAD, DISC, etc.), Transport (ARRI, DEPA), Shipment (RECE, CONF, etc.). Filterable by `equipmentEventTypeCode`, `transportEventTypeCode`, `shipmentEventTypeCode`, `carrierBookingReference`, `equipmentReference`, `carrierServiceCode`, `vesselIMONumber` |
| **Callback format** | DCSA event JSON POSTed to `callbackUrl`. Callback URL can contain query parameters for consumer-side routing |
| **Callback authentication** | Subscription includes a `secret` field — presumably used for callback verification |
| **Retry policy on failure** | Unknown — not documented |
| **Documented reliability** | Unknown — not documented. FAQ references DCSA subscription/callback specification ([DCSA PDF](https://dcsa.org/wp-content/uploads/2021/10/202109_DCSA-Subscription-Callback-API_1.0_Final.pdf)) for consumer-side implementation |

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | [https://ct.shipmentlink.com/servlet/TDB1_CargoTracking.do](https://ct.shipmentlink.com/servlet/TDB1_CargoTracking.do) |
| **Login required?** | No (public cargo tracking). Additional features at [Member Tracking](https://www.shipmentlink.com/servlet/TDB1_MemberTracking.do) (login required) |
| **Data available on portal but NOT in API** | Unknown — API coverage appears comprehensive based on DCSA spec. Portal may show presentation-layer formatting not in API |
| **Scraping feasibility** | Not assessed — API is the recommended access method given its comprehensive coverage |

### Other Web Portal Services

ShipmentLink offers additional web-based services:
- **Booking** — web-based booking submission
- **Container Tare Weight Search** — lookup container tare weights
- **B/L Instruction** — submit B/L instructions online
- **Non-negotiable B/L** / **i-B/L** — electronic B/L services
- **VGM Submission** — submit Verified Gross Mass declarations
- **Schedule search** — by area, point, or vessel
- **Tracking Report** — detailed tracking reports

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | **Yes** |
| **EDI message types** | Not documented on public pages — registration required to access EDI service details |
| **EDI connection method** | Unknown — registration at [EDI Service page](https://www.shipmentlink.com/tam1/jsp/TAM1_EdiRegisterNotice.jsp) required |
| **EDI documentation** | Behind login wall — accessible after EDI registration |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Unknown | Could not confirm from public sources. Evergreen is a major carrier and likely available, but not verified |
| **FourKites** | Unknown | Could not confirm from public sources |
| **Vizion** | Unknown | Could not confirm from public carrier list |
| **INTTRA / E2open** | Unknown | Not confirmed. Evergreen is a top-10 carrier and likely available on INTTRA |
| **CargoSmart** | Unknown | Not confirmed. CargoSmart is OOCL/COSCO-affiliated (Ocean Alliance partners), so integration is plausible |

> **Aggregator note**: Given that Evergreen has a comprehensive direct API (full DCSA suite), a direct integration is strongly recommended over aggregator access. The direct API provides richer data and avoids aggregator intermediary costs and latency.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown — not documented | Unknown |
| **API uptime/reliability** | Unknown — no published SLA | Unknown |
| **Historical data depth** | **Events only after go-live** — FAQ states: "Only events that happen after launch time can be traced." For shipments created before go-live, new events will appear when new activity occurs post go-live | Official (FAQ items 10 & 11) |
| **Timezone handling** | ISO 8601 with timezone offset (e.g., `+08:00`, `-05:00`, `+01:00`). Local port time with explicit offset | Official (event examples) |
| **Character encoding** | UTF-8 (standard JSON) | Official (API specs) |

### Known Issues & Gotchas

- **TNT is DCSA v2.2, not v3**: The Track & Trace API uses an older DCSA version. Key implications: (1) no `isTransshipmentMove` field — transshipment must be inferred, (2) single `/events` endpoint instead of separate event-type endpoints, (3) some event classifier codes may differ (examples show `"PLAN"` where DCSA standard uses `"PLN"`)
- **No historical data before launch**: Events are only available for shipments active after API go-live. No ability to query historical shipment data from before integration launch
- **IP whitelisting required**: API calls must come from pre-registered IP addresses. This affects deployment architecture — cannot use dynamic IPs or serverless functions without a fixed egress IP
- **"EGLV" prefix not needed in B/L lookups**: FAQ item 6 specifically notes that `"EGLV"` should NOT be included in the `transportDocumentReference` parameter. Common error that causes 500 responses
- **Vessel details sometimes empty in examples**: Several event examples show empty strings for `vesselIMONumber`, `vesselName`, `vesselFlag`, `vesselCallSignNumber` — this may occur for inland/intermodal legs or when vessel details are not yet assigned
- **Application approval required**: Cannot get immediate API access — must apply and wait for Evergreen staff verification. Timeline unknown
- **Event classifier "PLAN" vs "PLN"**: Event examples from Evergreen use `"PLAN"` in some cases where DCSA standard specifies `"PLN"`. The SDK adapter must handle both values

### Recently Deprecated or Changed

- No known deprecations documented. The TNT API's use of DCSA v2.2 (last updated 2023-11-15) suggests it may be scheduled for a v3 upgrade, but no timeline is published
- Booking, SI, and CS APIs were all recently updated (March–April 2025), suggesting active development

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | **Yes** — Evergreen has a comprehensive DCSA-compliant API suite. This is one of the most complete carrier API implementations we're likely to find |
| **Implementation effort** | **Medium** (DCSA with deviations) — Booking, SI, and CS follow current DCSA versions closely. TNT uses v2.2 which requires mapping to our v3-based canonical model. The main complexity is transshipment inference |
| **DCSA base adapter usable?** | **Yes with overrides** — Booking, SI, and CS can use a shared DCSA base adapter. TNT needs a v2→v3 translation layer |

### Recommended Approach

The Evergreen adapter should be built on top of a DCSA base adapter class. For Booking (v2.0.0), Commercial Schedules (v1.0.0), and Shipping Instructions (v3.0.0), the implementation should be nearly pass-through — these APIs follow current DCSA standards and response shapes should map directly to the SDK's canonical data model.

For Track & Trace, a **TNT v2.2 → canonical model translation layer** is needed. This layer should: (1) map the single `/events` endpoint response to the SDK's event model, (2) normalize event classifier codes (`"PLAN"` → `"PLN"`), (3) implement transshipment inference by correlating equipment DISC/LOAD events with the transport plan from the booking/schedule endpoints.

The adapter should combine data from multiple API domains — use Booking for cutoff times and transport plan, CS for schedule context, and TNT for real-time events. This "composite view" approach gives the richest shipment state.

### Recommended Lookup Method

**Booking reference** is the recommended primary lookup method. It provides access across all API domains — Booking API for cutoffs and transport plan, TNT for all event types (equipment, transport, shipment). B/L number (`transportDocumentReference`) is the secondary method for tracking shipments after B/L issuance. Container number is useful for equipment-level tracking but provides less context about the overall shipment.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Every 2–4 hours for active shipments (rate limits unknown, so start conservative). Use webhooks as the primary method and polling as backup |
| **Incremental filter** | Use `eventCreatedDateTime` parameter on `GET /tnt/v2/events` to fetch only new events since last poll |
| **Batch tracking** | One call per shipment — the events endpoint filters by individual booking/B/L/container reference. No documented batch endpoint |

### Auth Implementation Notes

Authentication follows a standard JWT flow:
1. POST to Token URL (provided during onboarding) with Client ID and Client Secret in the request body/header
2. Receive JWT token (format per [jwt.io](https://jwt.io))
3. Include JWT token in API request headers (likely `Authorization: Bearer <token>`)
4. Token has limited lifetime — implement automatic refresh when token expires

IP whitelisting means the adapter must make API calls from a known, static IP address. If deploying in a cloud environment, use a NAT gateway or proxy with a fixed egress IP.

The `API-Version` header is required on all TNT API calls. Set to `"2.2"` for Track & Trace.

### Edge Cases to Handle

- **Transshipment detection without `isTransshipmentMove`**: Must correlate DISC/LOAD events at intermediate ports with the transport plan. Strategy: fetch the booking's `transportPlan[]` first, identify intermediate ports, then classify DISC/LOAD events at those ports as transshipment
- **Empty vessel details on inland legs**: Vessel info (IMO, name, flag, call sign) may be empty strings for truck/rail/barge legs. The adapter should handle this gracefully and not fail on empty vessel data
- **"PLAN" vs "PLN" event classifier**: Normalize `"PLAN"` to `"PLN"` in the adapter's mapping layer
- **Multi-modal transport events**: Events cover vessel, barge, truck, rail, and border crossings. The `modeOfTransport` field distinguishes them. Ensure the SDK model can represent non-vessel transport legs
- **B/L prefix handling**: Ensure the adapter does NOT prepend "EGLV" to B/L numbers when querying — this causes 500 errors
- **Booking reference format**: Evergreen uses `EGLV_YYMMDDNNNNNNN` format for carrier booking request references

### Mapping Complexity

**Medium complexity**. The core event structure (equipment events with DCSA event type codes, transport events with ARRI/DEPA, shipment events with document lifecycle codes) maps directly to the canonical model. The main complexities are:

1. **TNT v2→v3 translation**: Single `/events` endpoint response must be decomposed by `eventType` discriminator field (EQUIPMENT/TRANSPORT/SHIPMENT)
2. **Transshipment inference**: Without `isTransshipmentMove`, need transport plan correlation. This is the most complex mapping task
3. **Event classifier normalization**: Handle `"PLAN"` → `"PLN"` mapping
4. **Cutoff aggregation**: Cutoffs come from both CS (point-to-point) and Booking (confirmed booking) endpoints — need to determine which source is authoritative and how to merge

---

## Open Questions

- [ ] Does SSL have an existing business relationship with Evergreen that would expedite API access approval?
- [ ] What is the typical application review timeline for API access?
- [ ] Are rate limits enforced? If so, what are the limits? (FAQ says T&T is free but doesn't mention limits)
- [ ] Is there a sandbox/test environment, or is testing done against production?
- [ ] Is the TNT API being upgraded to DCSA v3? If so, what is the timeline?
- [ ] What test data is available during the onboarding testing phase?
- [ ] Is Evergreen available on project44, FourKites, or Vizion? (Could not confirm from public sources)
- [ ] What is the JWT token lifetime? How frequently must tokens be refreshed?
- [ ] Does the webhook/push delivery have retry logic and what is the SLA?
- [ ] What specific EDI message types does Evergreen support?
- [ ] Are the Booking, SI, and CS APIs also free, or is there a fee for those?
- [ ] Can SSL use a fixed egress IP for API calls (IP whitelisting requirement)?

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | [https://www.evergreen-line.com](https://www.evergreen-line.com) |
| Corporate Website | [https://www.evergreen-marine.com](https://www.evergreen-marine.com) |
| ShipmentLink (e-Commerce Platform) | [https://www.shipmentlink.com](https://www.shipmentlink.com) |
| **Developer Portal** | [https://www.shipmentlink.com/_ec/APIPORTAL_Home](https://www.shipmentlink.com/_ec/APIPORTAL_Home) |
| **API Service Category** | [https://www.shipmentlink.com/_ec/APIPORTAL_APIServiceCategory](https://www.shipmentlink.com/_ec/APIPORTAL_APIServiceCategory) |
| **FAQ (Auth & Registration)** | [https://www.shipmentlink.com/_ec/APIPORTAL_FAQ](https://www.shipmentlink.com/_ec/APIPORTAL_FAQ) |
| Track & Trace Spec (Swagger UI) | [https://www.shipmentlink.com/_ec/APIPORTAL_SpecTrackAndTrace](https://www.shipmentlink.com/_ec/APIPORTAL_SpecTrackAndTrace) |
| Booking Spec (Swagger UI) | [https://www.shipmentlink.com/_ec/APIPORTAL_SpecBK](https://www.shipmentlink.com/_ec/APIPORTAL_SpecBK) |
| Shipping Instructions Spec (Swagger UI) | [https://www.shipmentlink.com/_ec/APIPORTAL_SpecSI](https://www.shipmentlink.com/_ec/APIPORTAL_SpecSI) |
| Commercial Schedules Spec (Swagger UI) | [https://www.shipmentlink.com/_ec/APIPORTAL_SpecCommercialSchedules](https://www.shipmentlink.com/_ec/APIPORTAL_SpecCommercialSchedules) |
| TNT Event List (Excel) | [https://www.shipmentlink.com/_apiportal/spec/doc/EMC_TNT_2.2_Event_List.xlsx](https://www.shipmentlink.com/_apiportal/spec/doc/EMC_TNT_2.2_Event_List.xlsx) |
| Cargo Tracking Portal | [https://ct.shipmentlink.com/servlet/TDB1_CargoTracking.do](https://ct.shipmentlink.com/servlet/TDB1_CargoTracking.do) |
| EDI Service Registration | [https://www.shipmentlink.com/tam1/jsp/TAM1_EdiRegisterNotice.jsp](https://www.shipmentlink.com/tam1/jsp/TAM1_EdiRegisterNotice.jsp) |
| DCSA About (founding members) | [https://dcsa.org/about-us/](https://dcsa.org/about-us/) |
| DCSA Subscription/Callback Spec (PDF) | [https://dcsa.org/wp-content/uploads/2021/10/202109_DCSA-Subscription-Callback-API_1.0_Final.pdf](https://dcsa.org/wp-content/uploads/2021/10/202109_DCSA-Subscription-Callback-API_1.0_Final.pdf) |
