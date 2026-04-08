# Mediterranean Shipping Company (MSC) — API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only — not verified with live API testing. Information gathered from MSC's public developer portal, DCSA specifications, MSC's Direct Integrations page (via Wayback Machine cache), and industry resources. No production API credentials were available.
> **Researched by**: Agent (automated research)
> **Date**: 2026-02-11
> **Last verified**: 2026-02-11

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | Mediterranean Shipping Company S.A. (MSC) |
| **SCAC Code** | MSCU |
| **Parent Company** | MSC Group (private, family-owned, Aponte family) |
| **Alliance** | None (formerly 2M with Maersk, ended January 2025) |
| **Primary Services** | Container shipping (primary), logistics, terminal operations, cruises (via MSC Cruises) |
| **Market Position** | Largest container carrier globally by TEU capacity (surpassed Maersk in January 2022) |
| **Headquarters** | Geneva, Switzerland |
| **Website** | [https://www.msc.com](https://www.msc.com) |

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | Yes |
| **Developer portal URL** | [https://developerportal.msc.com/](https://developerportal.msc.com/) |
| **API documentation URL(s)** | [API Catalogue](https://developerportal.msc.com/api-catalogue), [Subscription Guidelines](https://developerportal.msc.com/subscription), [EDI Guidelines](https://developerportal.msc.com/edi-guideline) |
| **Documentation quality** | Fair — Developer portal is publicly accessible with sandbox and "Try it Out" functionality, but API catalogue content loads dynamically via embedded iframes making offline review difficult. Production API details require onboarding. No public OpenAPI spec file found. |
| **OpenAPI/Swagger spec available?** | Sandbox Swagger appears to be available within the developer portal's API Catalogue (embedded), but no standalone downloadable OpenAPI spec file was found publicly. MSC's APIs follow DCSA TNT v2.2, so the [DCSA OpenAPI spec](https://app.swaggerhub.com/apis/dcsaorg/DCSA_TNT/2.2.0) serves as the reference. |
| **Sandbox/test environment?** | Yes — the developer portal provides a sandbox with predefined production-like mock data. "Try it Out" functionality available directly in the API Catalogue. |
| **Developer registration** | Requires formal request — submit the [Direct Integration Request Form](https://forms.office.com/Pages/ResponsePage.aspx?id=AJuOCND_jkW_oaz0xZbTy3IqSmARn5lCgJs0UnRRCHtUN1laQ1NNQUFNU0tNMkxJNFdWOVoxQ1c0Vy4u) for production access. Sandbox appears publicly accessible. |
| **Developer support channels** | MSC provides 24/7 support for direct integrations. Contact via the Direct Integration Request Form or local MSC representatives. |
| **Community/third-party libraries** | None found — no MSC-specific client libraries on GitHub or npm. DCSA reference implementations available at [github.com/dcsaorg](https://github.com/dcsaorg). |
| **API changelog / release notes** | Not published as a standalone changelog. Updates noted on developer portal pages (e.g., subscription and EDI guideline pages include date annotations). |

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | Yes — **founding member** (April 2019, alongside Maersk, CMA CGM, Hapag-Lloyd, ONE, Evergreen, Yang Ming, HMM, and ZIM) ([source](https://dcsa.org/about-us)) |
| **DCSA APIs implemented** | TNT (Track & Trace), CS (Commercial Schedules). Booking (BKG) was listed as "in development — planned for release by end of 2025" as of Oct 2025 page capture. |
| **DCSA TNT version** | **v2.2.0** (confirmed on MSC's Direct Integrations page: "DCSA T&T v2.2") |
| **DCSA Booking version** | **v2.0** — listed as "DCSA Booking 2.0 - In development - planned for release by end of 2025" (status as of Feb 2026 unknown — may now be live) |
| **DCSA Schedules version** | **v1.0** — confirmed on MSC Direct Integrations page as "DCSA Commercial Schedules 1.0" |
| **Known DCSA deviations** | None documented. MSC states their solutions are "designed to be compliant with industry standards." Per their FAQ, MSC uses SMDG terminal codes and BIC depot codes which align with DCSA recommendations. Internal codes may also be used — MSC states "our specialists will provide you with all the needed information during the onboarding process." |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Yes | IFTMBF (Booking Request), IFTMBC (Booking Confirmation), IFTMIN (Shipping Instruction), VERMAS (VGM), IFTMCS (Bill of Lading), IFTSAI (Routing/Sailing), IFTSTA (Track and Trace), APERAK (Functional Acknowledge). MSC states "EDIFact is used for the majority of MSC's data exchange processes" with 20+ years of experience. |
| **ANSI X12 (EDI)** | Yes | 300 (Booking Request), 301 (Booking Confirmation), 315 (Track and Trace — SCAC reference "N9*SCA" added Sep 2024), 323 (Routing/Sailing). |
| **INTTRA integration** | Yes | Confirmed on MSC Direct Integrations page as a connection partner. |
| **SMDG** | Yes | MSC follows SMDG recommendations and codifications including TCL (Terminal Code List). |
| **BIC (Bureau International des Containers)** | Yes | MSC follows BIC standards for container owner prefixes and supports BFC (BIC Facility Codes) for depot identification. |
| **UN/LOCODE** | Yes (implied) | Required by DCSA TNT compliance for port/location identification. |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | Not publicly documented. Given Azure Service Bus infrastructure for subscriptions, likely **OAuth2** or **API key** with Azure-based identity management. Specific credentials provided during onboarding. |
| **Auth documentation** | Not publicly available — provided during onboarding process. |
| **Registration process** | 1. Submit [Direct Integration Request Form](https://forms.office.com/Pages/ResponsePage.aspx?id=AJuOCND_jkW_oaz0xZbTy3IqSmARn5lCgJs0UnRRCHtUN1laQ1NNQUFNU0tNMkxJNFdWOVoxQ1c0Vy4u). 2. MSC specialists contact you to start onboarding. 3. Timeline defined jointly (APIs generally quicker than EDI). 4. Access to API definitions and sandbox provided. 5. Production credentials issued after testing. |
| **Registration URL** | [Direct Integration Request Form](https://forms.office.com/Pages/ResponsePage.aspx?id=AJuOCND_jkW_oaz0xZbTy3IqSmARn5lCgJs0UnRRCHtUN1laQ1NNQUFNU0tNMkxJNFdWOVoxQ1c0Vy4u) |
| **Partner program required?** | Yes — for production access. Direct Integration onboarding required. |
| **Partner program URL** | [MSC Direct Integrations](https://www.msc.com/en/solutions/digital-solutions/direct-integrations) |
| **Credential type** | Unknown — provided during onboarding |
| **Token refresh supported?** | Unknown |
| **Token lifetime** | Unknown |
| **Access tiers** | Not publicly documented. FAQ states "Depending on your requirements, setup and maintenance fees may apply." |
| **IP whitelisting required?** | Unknown |

### Access Requirements Summary for SSL

MSC does **not** offer self-service API registration. To get production API access, SSL must submit the Direct Integration Request Form and go through MSC's onboarding process. This involves contact with MSC's digital solutions team, defining integration scope, receiving API definitions and sandbox access, testing, and then production credential issuance.

**Key considerations:**
- Fees may apply for both setup and ongoing maintenance
- The sandbox with mock data is available through the developer portal for initial evaluation
- SSL should indicate they are interested in Track and Trace API access and Commercial Schedules
- If SSL has an existing MSC business relationship (which they likely do as an NVOCC), this should be mentioned in the request
- Former RSS Feed (web services) customers should mention their current URL for migration assistance

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field must have a row.
> ✅ = Available | ❌ = Not available | ⚠️ = Partial / limited | ❓ = Unknown
>
> **Note**: MSC implements DCSA TNT v2.2 and Commercial Schedules. Coverage assessments below are based on what the DCSA v2.2 specification mandates and what MSC's published API catalogue confirms. Actual field availability in production may vary.

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ✅ | DCSA Commercial Schedules API | vessel-schedules, port-schedules | DCSA CS v1.0 | Listed on MSC Direct Integrations page as "Commercial Vessel Schedules — DCSA Commercial" |
| 1.2 | Point-to-Point Route Options | ✅ | DCSA Commercial Schedules API | point-to-point-routes | DCSA CS v1.0 | Also available via EDI: IFTSAI (EDIFACT), 323 (X12) |
| 1.3 | Booking Lifecycle | ⚠️ | DCSA Booking API (in development) | bookings | DCSA BKG v2.0 | Listed as "DCSA Booking 2.0 - In development - planned for release by end of 2025." Status as of Feb 2026 is unknown — may now be live. Available via EDI: IFTMBF/IFTMBC (EDIFACT), 300/301 (X12). |
| 1.4 | Shipping Instructions | ⚠️ | DCSA BL/eDoc API (in development) | shipping-instructions | DCSA BL v3.0 | Listed as "DCSA BL 3.0 - In development - planned for release by end of 2025." Available via EDI: IFTMIN (EDIFACT). SI status tracked via DCSA ShipmentEvents in TNT. |
| 1.5 | Rates | ⚠️ | Rate Integration API v1 | `dpo-rateintegration-api-v1` | Not part of DCSA | MSC has a Rate Integration API v1 on the developer portal and listed "Contract Rates & Spot Rates — MSC Contract Rates (pilot)" on the Direct Integrations page (Oct 2025). Details require onboarding. Instant Quotes also available via myMSC web portal. |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ✅ | DCSA Commercial Schedules / Booking confirmation | `cutOffDateTimeCode: "ECP"` | `ECP` | Available in DCSA booking confirmation `shipmentCutOffTimes[]` and Commercial Schedules `cutOffTimes[]` |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ✅ | DCSA Commercial Schedules / Booking confirmation | `cutOffDateTimeCode: "EFC"` | `EFC` | Same delivery mechanism as ERD |
| 2.3 | Documentation Cutoff | DCO | ✅ | DCSA Commercial Schedules / Booking confirmation | `cutOffDateTimeCode: "DCO"` | `DCO` | Critical cutoff — expected in DCSA-compliant responses |
| 2.4 | VGM Cutoff | VCO | ✅ | DCSA Commercial Schedules / Booking confirmation | `cutOffDateTimeCode: "VCO"` | `VCO` | SOLAS requirement. MSC also supports VGM submission via VERMAS EDI. |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ✅ | DCSA Commercial Schedules / Booking confirmation | `cutOffDateTimeCode: "FCO"` | `FCO` | Critical cutoff for full container loads |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ✅ | DCSA Commercial Schedules / Booking confirmation | `cutOffDateTimeCode: "LCO"` | `LCO` | Conditional: only when `receiptTypeAtOrigin = "CFS"` |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ✅ | `GET /v2/events?eventType=EQUIPMENT` | Inferred from first EquipmentEvent with matching `relatedDocumentReferences[].type=BKG` | Inferred from first EquipmentEvent | Standard DCSA inference pattern |
| 3.2 | Empty Container Gate-Out (Pickup) | ✅ | `GET /v2/events?eventType=EQUIPMENT` | `equipmentEventTypeCode: GTOT` + `emptyIndicatorCode: EMPTY` | `GTOT` + `EMPTY` | May also appear as `PICK` at some facilities |
| 3.3 | Full Container Gate-In | ✅ | `GET /v2/events?eventType=EQUIPMENT` | `equipmentEventTypeCode: GTIN` + `emptyIndicatorCode: LADEN` | `GTIN` + `LADEN` | At origin terminal |
| 3.4 | Container Loaded on Vessel | ✅ | `GET /v2/events?eventType=EQUIPMENT` | `equipmentEventTypeCode: LOAD` + `emptyIndicatorCode: LADEN` | `LOAD` + `LADEN` | Critical milestone |
| 3.5 | Container Discharged at Transshipment | ✅ | `GET /v2/events?eventType=EQUIPMENT` | `equipmentEventTypeCode: DISC` + `emptyIndicatorCode: LADEN` + transshipment context | `DISC` + `LADEN` + transshipment | Identified by intermediate port in transport plan |
| 3.6 | Container Loaded at Transshipment | ✅ | `GET /v2/events?eventType=EQUIPMENT` | `equipmentEventTypeCode: LOAD` + `emptyIndicatorCode: LADEN` + transshipment context | `LOAD` + `LADEN` + transshipment | New vessel appears in `transportCall.vessel` |
| 3.7 | Container Discharged at Destination | ✅ | `GET /v2/events?eventType=EQUIPMENT` | `equipmentEventTypeCode: DISC` + `emptyIndicatorCode: LADEN` at destination | `DISC` + `LADEN` | Critical milestone |
| 3.8 | Full Container Gate-Out (Delivery) | ✅ | `GET /v2/events?eventType=EQUIPMENT` | `equipmentEventTypeCode: GTOT` + `emptyIndicatorCode: LADEN` | `GTOT` + `LADEN` | May be preceded by `AVPU` (Available for Pick-up) |
| 3.9 | Empty Container Returned | ✅ | `GET /v2/events?eventType=EQUIPMENT` | `equipmentEventTypeCode: GTIN` + `emptyIndicatorCode: EMPTY` | `GTIN` + `EMPTY` | At return depot. Uses BIC Facility Codes per MSC's standards. |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ✅ | `GET /v2/events?eventType=TRANSPORT` | `transportEventTypeCode: DEPA` + `eventClassifierCode: EST` (or `PLN`, `ACT`) | `DEPA` + classifier | PLN→EST→ACT progression supported in DCSA v2.2 |
| 4.2 | Estimated Time of Arrival | ETA | ✅ | `GET /v2/events?eventType=TRANSPORT` | `transportEventTypeCode: ARRI` + `eventClassifierCode: EST` (or `PLN`, `ACT`) | `ARRI` + classifier | PLN→EST→ACT progression supported |
| 4.3 | Vessel Arrival at Transshipment | — | ✅ | `GET /v2/events?eventType=TRANSPORT` | `transportEventTypeCode: ARRI` at intermediate port | `ARRI` at intermediate | Identified by port matching transport plan leg sequence |
| 4.4 | Vessel Departure from Transshipment | — | ✅ | `GET /v2/events?eventType=TRANSPORT` | `transportEventTypeCode: DEPA` at intermediate port | `DEPA` at intermediate | On connecting vessel |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ✅ (via Azure Service Bus) | DCSA TNT v2.2 subscription endpoints (`POST /v2/event-subscriptions`). MSC uses **Azure Service Bus** for push delivery rather than standard REST webhooks. Subscription guidelines available on developer portal (dated March 2025). |
| Event Polling with timestamp filter | ✅ | DCSA TNT v2.2 mandates `GET /v2/events` with `eventCreatedDateTime` filter parameter. This is the universal fallback. |
| Event Classifier Progression (PLN→EST→ACT) | ✅ | Standard DCSA pattern — events carry `eventClassifierCode` field showing progression. |
| Retracted Events | ✅ | DCSA TNT v2.2 supports `metadata.retractedEventID` for voiding prior events. |
| Change Remarks | ✅ | DCSA TNT v2.2 includes `changeRemark` field on TransportEvents (free text, max 250 chars). |
| Delay Reason Codes | ✅ | DCSA TNT v2.2 includes `delayReasonCode` with standardized codes. |

### Coverage Summary

| Category | Fields Available | Fields Unavailable | Fields Partial/Unknown | Coverage % |
|----------|-----------------|-------------------|----------------------|-----------|
| API Domains (1.x) | 2/5 | 0/5 | 3/5 | 40% (100% with EDI/partial) |
| Cutoffs (2.x) | 6/6 | 0/6 | 0/6 | 100% |
| Container Milestones (3.x) | 9/9 | 0/9 | 0/9 | 100% |
| Transport Events (4.x) | 4/4 | 0/4 | 0/4 | 100% |
| Change Detection (5.x) | 6/6 | 0/6 | 0/6 | 100% |
| **Total** | **27/30** | **0/30** | **3/30** | **90%** |

> **Note on API Domains**: The 2 "partial/unknown" fields (1.3 Booking, 1.4 Shipping Instructions) were listed as "in development — planned for end of 2025" on MSC's page as of Oct 2025. They may now be live (Feb 2026). Both are available via EDI regardless. Field 1.5 (Rates) was updated from ❌ to ⚠️ after discovering a Rate Integration API v1 (`dpo-rateintegration-api-v1`) in the developer portal API catalogue and "Contract Rates & Spot Rates (pilot)" on the Direct Integrations page. No API domain is fully unavailable — all 5 have at least partial or EDI coverage.

---

## Endpoint Reference

### Tracking / Events (DCSA TNT v2.2)

| Endpoint | Method | Lookup Params | Pagination | Response Format | Notes |
|----------|--------|--------------|------------|----------------|-------|
| `/v2/events` | GET | `eventType` (SHIPMENT/TRANSPORT/EQUIPMENT), `shipmentEventTypeCode`, `carrierBookingReference`, `transportDocumentReference` (B/L), `equipmentReference` (container), `eventCreatedDateTime:gte`, `eventCreatedDateTime:lte` | Cursor-based (DCSA standard) | JSON | Primary tracking endpoint. Supports filtering by event type, document type, and date range. |
| `/v2/events/{eventID}` | GET | `eventID` (path) | N/A | JSON | Get a single event by ID. |

### Event Subscriptions (DCSA TNT v2.2)

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| `/v2/event-subscriptions` | POST | `callbackUrl`, `eventType[]`, `carrierBookingReference`, `transportDocumentReference`, `equipmentReference` | N/A | JSON | Create subscription. **MSC delivers via Azure Service Bus** rather than standard HTTP callbacks. |
| `/v2/event-subscriptions` | GET | N/A | Cursor-based | JSON | List active subscriptions. |
| `/v2/event-subscriptions/{subscriptionID}` | GET | `subscriptionID` (path) | N/A | JSON | Get subscription details. |
| `/v2/event-subscriptions/{subscriptionID}` | PUT | `subscriptionID` (path) + updated fields | N/A | JSON | Update subscription. |
| `/v2/event-subscriptions/{subscriptionID}` | DELETE | `subscriptionID` (path) | N/A | N/A | Delete subscription. |
| `/v2/event-subscriptions/{subscriptionID}/secret` | PUT | `subscriptionID` (path) | N/A | JSON | Reset subscription secret. |

### Schedules (DCSA Commercial Schedules)

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| Vessel Schedules | GET | vessel, port, date range | ❓ | JSON | Exact path not confirmed from public docs; follows DCSA CS standard pattern (`/v1/vessel-schedules`). |
| Port Schedules | GET | port, date range | ❓ | JSON | Follows DCSA CS standard pattern (`/v1/port-schedules`). |
| Point-to-Point Routes | GET | origin, destination, date range | ❓ | JSON | Follows DCSA CS standard pattern (`/v1/point-to-point-routes`). Also available via IFTSAI/323 EDI. |

### Booking (DCSA Booking v2.0) — Status: Was "In Development" as of Oct 2025

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| `/v2/bookings` | POST/GET | booking reference | ❓ | JSON | "DCSA Booking 2.0 - In development - planned for release by end of 2025." Available via EDI: IFTMBF/300 (request), IFTMBC/301 (confirmation). |

### Other Endpoints

| Endpoint | Method | Purpose | Key Params | Notes |
|----------|--------|---------|-----------|-------|
| iReefer Ultimate API | ❓ | Smart container telemetry — real-time location, temperature, humidity | Container reference | Added Aug 2025. For refrigerated containers. "Contact local MSC representatives" for access. |


### Additional APIs (Developer Portal Catalogue)

> **Note**: The following APIs were identified in the MSC developer portal API catalogue but were not documented in the original inventory. Details beyond the API ID and inferred purpose require onboarding access. Discovered during review audit (Feb 2026).

| API ID | Name | Inferred Purpose | Status | Notes |
|--------|------|-----------------|--------|-------|
| `dpo-rateintegration-api-v1` | Rate Integration API v1 | Contract rates and spot rates | Pilot/Partial | Listed in developer portal API catalogue. Direct Integrations page (Oct 2025) showed "Contract Rates & Spot Rates — MSC Contract Rates (pilot)". Details require onboarding. |
| `DPO-MSCReporting-API-V1` | MSC Reporting API v1 | Reporting (unknown specifics) | Unknown | Listed in developer portal API catalogue. No public documentation found on purpose or endpoints. Requires onboarding to investigate. |
| `dpo-referential-api-v1` | Referential API v1 | Reference/master data (inferred) | Unknown | Listed in developer portal API catalogue. Likely provides reference data (ports, terminals, vessel codes, etc.). Requires onboarding to confirm. |
| `dpo-mscroutingsailings-api-v1` | MSC Routing/Sailings API v1 | Routing and sailing schedules | Unknown | Listed in developer portal API catalogue as a distinct API from the DCSA Commercial Schedules API. May be an MSC-specific (non-DCSA) routing endpoint. Relationship to Commercial Schedules API unclear. Requires onboarding to investigate. |

> **Developer portal lists 6 APIs total**: DPO-DCSATrackAndTrace-API-V2, DPO-Commercial-Schedules-API-V1, plus the 4 above. Only TNT and Commercial Schedules were fully documented in the original inventory.

### Lookup Methods Summary

| Identifier Type | Supported? | Which Endpoints? | Notes |
|----------------|-----------|-----------------|-------|
| **Bill of Lading (B/L) number** | ✅ | `/v2/events` via `transportDocumentReference` | DCSA standard lookup parameter |
| **Booking reference** | ✅ | `/v2/events` via `carrierBookingReference` | DCSA standard lookup parameter |
| **Container number** | ✅ | `/v2/events` via `equipmentReference` | DCSA standard lookup parameter |
| **Carrier booking number** | ✅ | `/v2/events` via `carrierBookingReference` | Same as booking reference in DCSA |
| **Vessel IMO / voyage** | ✅ | Schedules API + `/v2/events` filtering | Vessel filtering available in event queries |

---

## Rate Limits & Quotas

| Detail | Value | Source |
|--------|-------|--------|
| **Global rate limit** | Unpublished | Unknown |
| **Per-endpoint limits** | Unpublished | Unknown |
| **Daily/monthly quota** | Unpublished | Unknown |
| **Rate limit response** | Unknown — likely 429 with Retry-After header per DCSA standard practice | Estimated (unverified) |
| **Rate limit by** | Unknown | Unknown |
| **Burst allowance** | Unknown | Unknown |
| **Different tiers** | Likely — MSC mentions "Depending on your requirements, setup and maintenance fees may apply" suggesting tiered access | Reported (from MSC FAQ) |

> **Note**: Rate limit details are not publicly documented. They are likely communicated during the onboarding process and may vary by customer agreement.

---

## Webhook / Push Support

| Detail | Value |
|--------|-------|
| **Webhooks supported?** | Yes — via **Azure Service Bus** (not standard REST webhooks) |
| **Subscription endpoint** | `POST /v2/event-subscriptions` (DCSA standard) |
| **Subscription management** | Create/list/get/update/delete via DCSA subscription API endpoints |
| **Subscribable event types** | SHIPMENT, TRANSPORT, EQUIPMENT events — filterable by booking ref, B/L, container number |
| **Callback format** | Azure Service Bus messages containing DCSA event JSON. **Not standard HTTP POST to callbackUrl** — MSC uses Azure Service Bus as the delivery mechanism. |
| **Callback authentication** | Subscription secret (resettable via `PUT /v2/event-subscriptions/{id}/secret`) + Azure Service Bus connection credentials |
| **Retry policy on failure** | Unknown — Azure Service Bus has built-in message retry/dead-letter capabilities |
| **Documented reliability** | Unknown |

> **Critical note for SDK implementation**: MSC's push notification system uses Azure Service Bus, not standard HTTP webhook callbacks. This means the SDK's subscription consumer would need an Azure Service Bus client library rather than a simple HTTP server. This is a significant architectural consideration.

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | [https://www.msc.com/en/track-a-shipment](https://www.msc.com/en/track-a-shipment) |
| **Login required?** | No login required for basic container tracking; myMSC login required for full shipment management |
| **myMSC platform** | [https://mymsc.com](https://mymsc.com) — full shipment management portal (booking, tracking, documents, quotes) |
| **Data available on portal but NOT in API** | Instant Quotes (rates), some document downloads, customer-specific reporting. Portal may also show more human-readable descriptions. |
| **Scraping feasibility** | Difficult — MSC's website uses Akamai CDN with aggressive bot protection (all automated requests return 403). |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Yes — comprehensive EDI support, MSC's longest-running integration method (20+ years) |
| **EDI message types — EDIFACT** | IFTMBF (Booking Request), IFTMBC (Booking Confirmation), IFTMIN (Shipping Instruction), VERMAS (VGM), IFTMCS (Bill of Lading), IFTSAI (Routing/Sailing), IFTSTA (Track and Trace), APERAK (Functional Acknowledge) |
| **EDI message types — ANSI X12** | 300 (Booking Request), 301 (Booking Confirmation), 315 (Track and Trace), 323 (Routing/Sailing) |
| **EDI connection method** | SFTP, AS2 (confirmed on MSC Direct Integrations page) |
| **EDI documentation** | [EDI Guidelines on Developer Portal](https://developerportal.msc.com/edi-guideline) — implementation guidelines for each message type |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Yes (likely) | MSC is the largest carrier globally; project44 covers all major carriers. Not explicitly confirmed from MSC's pages but near-certain given market position. |
| **FourKites** | Yes (likely) | Same reasoning as project44 — FourKites covers major ocean carriers. |
| **Vizion** | Yes (likely) | Vizion states they "standardize messages across all carriers" and covers major ocean lines. |
| **INTTRA / E2open** | ✅ Yes | **Confirmed** on MSC Direct Integrations page as a connection partner. |
| **CargoSmart** | ✅ Yes | **Confirmed** on MSC Direct Integrations page as a connection partner. |
| **InforNexus** | ✅ Yes | **Confirmed** on MSC Direct Integrations page as a connection partner. |

> **Aggregator note**: MSC explicitly lists INTTRA, InforNexus, and CargoSmart as connection partners on their Direct Integrations page, stating they "design and tailor technology solutions" including "developing direct integration solutions" for these platforms. For SSL, using an aggregator may be simpler than direct MSC API onboarding if the aggregator relationship already exists.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | APIs support "near real-time" data exchange (MSC's wording). Actual latency unknown. | Reported (MSC Direct Integrations page) |
| **API uptime/reliability** | Unknown — no public SLA published. MSC offers 24/7 support for direct integrations. | Unknown |
| **Historical data depth** | Unknown — not documented publicly. | Unknown |
| **Timezone handling** | UTC (DCSA standard mandates ISO 8601 with UTC offset for all timestamps) | Official (DCSA TNT v2.2 specification) |
| **Character encoding** | UTF-8 (DCSA standard) | Official (DCSA specification) |

### Known Issues & Gotchas

- **No self-service API access**: Production credentials require formal onboarding through MSC's Direct Integration Request Form. This process involves MSC specialists and may include fees.
- **Azure Service Bus for push**: MSC uses Azure Service Bus instead of standard HTTP webhooks for event subscriptions. This requires Azure-specific client libraries for consuming push notifications.
- **Website blocks automation**: MSC's main website (www.msc.com) uses Akamai CDN with aggressive bot protection — all curl/automated requests return 403. This affects any web scraping fallback strategy.
- **Booking API status uncertain**: The DCSA Booking 2.0 API was listed as "planned for end of 2025" on the page captured Oct 2025. Its current status (Feb 2026) is unknown — it may now be live.
- **Internal codes**: MSC uses a mix of standard codes (SMDG, BIC) and internal codes. MSC states coded values will be explained during onboarding.
- **DCSA TNT v2.2 vs. v3.0**: MSC implements v2.2, not the latest v3.0. The event model differs between versions (v2 uses combined event types, v3 has separated Equipment, Transport, and Shipment event models). The SDK adapter must account for v2.2 specifics.
- **No public OpenAPI spec**: While the developer portal has embedded API documentation, no standalone downloadable OpenAPI/Swagger spec was found. The DCSA TNT v2.2 spec should serve as the reference.

### Recently Deprecated or Changed

- **TradeLens**: MSC previously participated in TradeLens (IBM/Maersk blockchain platform). TradeLens was shut down in 2023. MSC's page for it returned 404 by late 2023, then 301 redirect by 2024.
- **RSS Feed (Web Services)**: MSC's FAQ mentions "current RSS Feed (web services) customer" migration to the new API, suggesting an older RSS-based tracking service existed and is being sunset.
- **EDI Track & Trace 315**: The N9*CA reference identifier was replaced with N9*SCA (Carrier SCAC Reference Identification Qualifier) in September 2024.

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | Yes — MSC implements DCSA TNT v2.2 and Commercial Schedules, providing comprehensive tracking and schedule data. |
| **Implementation effort** | **Medium** (DCSA with minor deviations) — MSC follows DCSA TNT v2.2, but the Azure Service Bus subscription model adds complexity. Polling via `GET /v2/events` is straightforward. |
| **DCSA base adapter usable?** | Yes with overrides — the TNT v2.2 polling endpoints follow the standard closely. Subscription/push handling needs MSC-specific Azure Service Bus implementation. |

### Recommended Approach

MSC's Track and Trace API follows DCSA TNT v2.2, making it a strong candidate for a DCSA base adapter. The adapter should:

1. **Use the DCSA base adapter** for event polling (`GET /v2/events`), event parsing, and field mapping. Since MSC claims full DCSA compliance, the standard DCSA event model should map directly.

2. **Override the subscription/push mechanism** to handle Azure Service Bus instead of standard HTTP webhooks. This is the most significant MSC-specific deviation.

3. **Add a Commercial Schedules module** for cutoff data and route information, following the DCSA Commercial Schedules API pattern.

4. **Fall back to polling** for the initial implementation, as polling is simpler, universally supported by DCSA carriers, and doesn't require Azure Service Bus infrastructure. Push via Azure Service Bus can be added as a v2 enhancement.

5. **Handle DCSA TNT v2.2 specifics**: The adapter must account for v2.2 event model differences from v3.0 (combined vs. separated event types).

### Recommended Lookup Method

**Bill of Lading (transportDocumentReference)** is recommended as the primary lookup method. B/L numbers are the most universal identifier in ocean shipping, work across transshipments, and return the complete shipment event history. Container number (`equipmentReference`) is a good secondary lookup for FCL shipments. Booking reference (`carrierBookingReference`) is useful for pre-sailing tracking before a B/L is issued.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Every 2–4 hours for active shipments. Rate limits are unpublished, so start conservative. |
| **Incremental filter** | Use `eventCreatedDateTime:gte={lastPollTime}` to retrieve only new events since last poll. DCSA TNT v2.2 supports this parameter. |
| **Batch tracking** | One API call per shipment (DCSA events endpoint filters by individual document/equipment reference). No batch multi-shipment endpoint in DCSA v2.2. Consider parallelizing calls with rate limiting. |

### Auth Implementation Notes

Authentication details are not publicly documented. During onboarding, MSC will provide:
- Credential type and format (likely OAuth2 client credentials or API key)
- Token endpoint (if OAuth2)
- Token lifetime and refresh mechanism
- Any required headers or query parameters

The adapter's auth module should be designed to accept configurable credentials with a pluggable auth strategy pattern, allowing the specific mechanism to be implemented once MSC provides the details during onboarding.

### Edge Cases to Handle

- **Azure Service Bus push**: If push is implemented, the adapter needs Azure Service Bus client library (`@azure/service-bus`) for consuming messages. This is non-standard for a DCSA adapter.
- **DCSA v2.2 vs v3.0 event model**: v2.2 uses combined event types with `eventType` field (SHIPMENT/TRANSPORT/EQUIPMENT). If the SDK's canonical model is based on v3.0 (which separates these), a mapping layer is needed.
- **Internal codes alongside standard codes**: MSC uses some internal codes alongside SMDG/BIC standards. The adapter should pass through unknown codes and log them for investigation.
- **Transshipment identification**: In DCSA v2.2, transshipment events must be inferred from port sequence in the transport plan, not from explicit flags.
- **Booking API availability uncertainty**: The adapter should gracefully handle 404 or unavailable booking endpoints if DCSA Booking 2.0 is not yet live.
- **Akamai protection**: Any fallback web scraping strategy for MSC is not viable due to aggressive CDN protection.

### Mapping Complexity

**Low to Medium**. MSC implements DCSA TNT v2.2, which closely matches our canonical data model (since the model is based on DCSA). The main mapping work is:

1. **v2.2 → v3.0 event model translation** (if our canonical model uses v3.0 structure)
2. **Internal code handling** for facility/terminal codes not in SMDG/BIC
3. **Cutoff data extraction** from Commercial Schedules response into our cutoff model
4. **Azure Service Bus message parsing** for push notifications (if implemented)

---

## Open Questions

- [ ] **Does SSL have an existing MSC business relationship?** This would simplify the Direct Integration onboarding process.
- [ ] **Is MSC's DCSA Booking 2.0 API now live?** It was planned for end of 2025 — need to verify current status during onboarding.
- [ ] **What is MSC's authentication mechanism?** OAuth2, API key, or something else? Only determinable during onboarding.
- [ ] **What are MSC's actual rate limits?** Unpublished — need to discover during onboarding or empirically during testing.
- [ ] **Does MSC's TNT v2.2 implementation deviate from the DCSA spec?** Their FAQ mentions internal codes. Full deviation list only available after API access.
- [ ] **Is Azure Service Bus the only push delivery option?** Or does MSC also support standard HTTP webhooks? The developer portal only mentions Service Bus.
- [ ] **What test data is available in the sandbox?** The FAQ says "predefined set of production-like mock data" — need to evaluate coverage.
- [ ] **Is the iReefer Ultimate API relevant for SSL?** Only applicable if SSL ships refrigerated cargo via MSC.
- [ ] **Does MSC charge per-API-call or flat-rate?** The FAQ mentions "fees may apply" but no pricing model is published.
- [ ] **Has MSC's TradeLens data been migrated to DCSA APIs?** TradeLens was shut down in 2023 — any historical data may only be in MSC's own systems.

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | [https://www.msc.com](https://www.msc.com) |
| Developer Portal | [https://developerportal.msc.com/](https://developerportal.msc.com/) |
| API Catalogue | [https://developerportal.msc.com/api-catalogue](https://developerportal.msc.com/api-catalogue) |
| Subscription Guidelines | [https://developerportal.msc.com/subscription](https://developerportal.msc.com/subscription) |
| EDI Guidelines | [https://developerportal.msc.com/edi-guideline](https://developerportal.msc.com/edi-guideline) |
| FAQ | [https://developerportal.msc.com/faq](https://developerportal.msc.com/faq) |
| Direct Integration Request Form | [https://forms.office.com/Pages/ResponsePage.aspx?id=AJuOCND_jkW_oaz0xZbTy3IqSmARn5lCgJs0UnRRCHtUN1laQ1NNQUFNU0tNMkxJNFdWOVoxQ1c0Vy4u](https://forms.office.com/Pages/ResponsePage.aspx?id=AJuOCND_jkW_oaz0xZbTy3IqSmARn5lCgJs0UnRRCHtUN1laQ1NNQUFNU0tNMkxJNFdWOVoxQ1c0Vy4u) |
| Direct Integrations Page | [https://www.msc.com/en/solutions/digital-solutions/direct-integrations](https://www.msc.com/en/solutions/digital-solutions/direct-integrations) |
| Digital Solutions Page | [https://www.msc.com/en/solutions/digital-solutions](https://www.msc.com/en/solutions/digital-solutions) |
| Data Protection Notice | [https://developerportal.msc.com/content/Data_Protection_Notice_Direct_Integration.pdf](https://developerportal.msc.com/content/Data_Protection_Notice_Direct_Integration.pdf) |
| DCSA About / Members | [https://dcsa.org/about-us](https://dcsa.org/about-us) |
| DCSA TNT v2.2 OpenAPI Spec | [https://app.swaggerhub.com/apis/dcsaorg/DCSA_TNT/2.2.0](https://app.swaggerhub.com/apis/dcsaorg/DCSA_TNT/2.2.0) ⚠️ May redirect/timeout; check [DCSA GitHub](https://github.com/dcsaorg/DCSA-OpenAPI/tree/master/tnt) for current spec |
| DCSA GitHub | [https://github.com/dcsaorg](https://github.com/dcsaorg) |
| myMSC Platform | [https://mymsc.com](https://mymsc.com) |
| Web Tracking | [https://www.msc.com/en/track-a-shipment](https://www.msc.com/en/track-a-shipment) |
| INTTRA (E2open) | [https://www.inttra.com/](https://www.inttra.com/) |
| CargoSmart | [https://www.cargosmart.com/](https://www.cargosmart.com/) |
| Wayback Machine: Direct Integrations (Oct 2025) | [https://web.archive.org/web/20251008011304/https://www.msc.com/en/solutions/digital-solutions/direct-integrations](https://web.archive.org/web/20251008011304/https://www.msc.com/en/solutions/digital-solutions/direct-integrations) |
| Wayback Machine: Digital Solutions (Sep 2025) | [https://web.archive.org/web/20250906202408/https://www.msc.com/en/solutions/digital-solutions](https://web.archive.org/web/20250906202408/https://www.msc.com/en/solutions/digital-solutions) |
