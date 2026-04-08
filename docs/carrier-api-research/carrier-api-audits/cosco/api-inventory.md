# COSCO Container Lines -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing
> **Researched by**: Agent
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | COSCO Shipping Lines Co., Ltd (commonly "COSCO") |
| **SCAC Code** | COSU |
| **Parent Company** | COSCO Shipping Holdings / China COSCO Shipping Corporation |
| **Alliance** | Ocean Alliance (with CMA CGM, Evergreen, OOCL -- extended to 2032) |
| **Primary Services** | Container shipping, logistics, terminal operations |
| **Market Position** | Fourth-largest container shipping line globally |
| **Headquarters** | Shanghai, China |
| **Website** | https://lines.coscoshipping.com |

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | Yes |
| **Developer portal URL** | https://cop.lines.coscoshipping.com/ |
| **API documentation URL(s)** | https://github.com/cop-cos/COP (primary); https://cop.lines.coscoshipping.com/ (portal) |
| **Documentation quality** | Fair -- English docs exist on GitHub but are sparse; Chinese docs more comprehensive. No interactive API explorer |
| **OpenAPI/Swagger spec available?** | No |
| **Sandbox/test environment?** | Yes (`https://api-pp.lines.coscoshipping.com/service`) |
| **Developer registration** | Requires approval -- submit application via COP portal, 15-business-day review, partnership agreement required |
| **Developer support channels** | COP portal contact; no public developer forum or Slack found |
| **Community/third-party libraries** | Official: Java, PHP, Python HMAC examples on GitHub (https://github.com/cop-cos/COP). No published npm/PyPI packages. Third-party: TrackingMore and Tracktry offer multi-carrier SDKs covering COSCO |
| **API changelog / release notes** | Not published separately; updates reflected in GitHub repo commits |

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | No -- COSCO has been courted by DCSA but has not joined as of latest available information (Source: https://www.seatrade-maritime.com/middle-east-africa/digital-container-shipping-association-courts-cosco-10th-member) |
| **DCSA APIs implemented** | None |
| **DCSA TNT version** | N/A |
| **DCSA Booking version** | N/A |
| **DCSA Schedules version** | N/A |
| **Known DCSA deviations** | N/A -- COSCO does not implement DCSA APIs. API platform is fully proprietary |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Yes | IFTMIN (Shipping Instructions), COPARN, IFTSTA (Status), VERMAS (VGM) via INTTRA/E2open |
| **INTTRA integration** | Yes | Established partnership for booking, SI, VGM. COSCO joined INTTRA eVGM network (Source: https://www.inttra.com/newsroom/press-releases/coscon-extends-relationship-with-inttra/) |
| **BIC (Bureau International des Containers)** | Yes | Standard container ID format used in tracking API |
| **UN/LOCODE** | Unknown | Schedule API uses COSCO-internal port UUIDs; UN/LOCODE usage not confirmed |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | HMAC-SHA1 (API Key + Secret Key) |
| **Auth documentation** | https://github.com/cop-cos/COP/blob/master/README_en.md |
| **Registration process** | 1. Visit COP portal (https://cop.lines.coscoshipping.com/) 2. Submit residency application with documentation 3. 15-business-day review period 4. ApiKey and SecretKey sent via email upon approval |
| **Registration URL** | https://cop.lines.coscoshipping.com/ |
| **Partner program required?** | Yes -- for any access. Partnership agreement covering development, application security, and platform operations required |
| **Partner program URL** | https://cop.lines.coscoshipping.com/ |
| **Credential type** | API Key + Secret Key pair (used for HMAC signature generation) |
| **Token refresh supported?** | N/A -- HMAC auth uses per-request signature, not bearer tokens |
| **Token lifetime** | N/A -- each request is independently signed |
| **Access tiers** | Single tier during trial operation (free). Future paid tiers unknown |
| **IP whitelisting required?** | Unknown |

### HMAC Authentication Details

Each API request requires the following headers computed from the ApiKey and SecretKey:

```
X-Coscon-Date: EEE, dd MMM yyyy HH:mm:ss z (GMT, +/- 2 min tolerance)
X-Coscon-Content-Md5: MD5(random UUID)
X-Coscon-Digest: SHA-256=Base64(SHA256(request body))  [POST/PUT only]
X-Coscon-Authorization: HMAC-SHA1 signature
X-Coscon-Hmac: Content MD5 value
```

Source: https://github.com/cop-cos/COP/blob/master/README_en.md

### Access Requirements Summary for SSL

COSCO requires a formal application and partnership agreement to access the COP API, with a 15-business-day review period. This is more restrictive than carriers like Maersk (self-service) or CMA CGM (2-3 day approval). SSL will need to submit documentation and sign agreements before receiving credentials. The COP platform is currently in "trial operation" with free access, but long-term pricing and tier structure are not published.

The HMAC-SHA1 authentication is unusual among ocean carrier APIs (most use OAuth2 or simple API keys). SSL's adapter will need a custom auth handler that computes HMAC signatures per-request, including SHA-256 body digests and timestamp headers. Reference implementations in Java, PHP, and Python are available on GitHub.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field has a row.
> Availablity legend: check = Available | x = Not available | warning = Partial / limited | question = Unknown

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ✅ | `POST /info/schedule` | Vessel name, voyage, ETD/ETA, port facility codes | N/A (proprietary) | Returns sailing schedules with vessel details, cutoff times, transit times. Uses COSCO-internal port UUIDs |
| 1.2 | Point-to-Point Route Options | ✅ | `POST /info/schedule` | Route options with transit time, transshipment info | N/A (proprietary) | Schedule API supports origin-destination queries with CY/Door transport terms. Includes `shortestTransitTime` |
| 1.3 | Booking Lifecycle | ✅ | SynConHub APIs: Spot Rate v2, Booking v2, Cross Booking, Long Term, Reefer, SME | Booking creation, confirmation download | N/A (proprietary) | Multiple booking channels via SynConHub. Also: Booking Confirmation Download, Waybill Management, Order Change History APIs on COP |
| 1.4 | Shipping Instructions | ⚠️ | Waybill Management API (COP); INTTRA/E2open EDI (IFTMIN) | Waybill download, order information queries | N/A (proprietary) | COP has waybill management APIs. Full SI submission likely via INTTRA EDI rather than REST API |
| 1.5 | Rates | ✅ | SynConHub Spot Rate v1/v2 API | Spot rates, long-term contract rates | N/A (proprietary) | Rates available through SynConHub platform APIs |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❓ | Unknown | Unknown | `ECP` | Not explicitly documented in available COP API materials. May be available in schedule or booking response |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❓ | Unknown | Unknown | `EFC` | Not explicitly documented. May be in schedule or booking response |
| 2.3 | Documentation Cutoff | DCO | ⚠️ | `POST /info/schedule` (cutoff times in response); `GET /info/tracking` (cargo cutoff times) | Cutoff timestamps in schedule/tracking response | `DCO` | Schedule API response includes "cutoff times." Tracking API response includes "cargo cutoff times." Specific field names for documentation cutoff require live testing |
| 2.4 | VGM Cutoff | VCO | ⚠️ | `POST /info/schedule` (cutoff times in response) | Cutoff timestamp | `VCO` | Schedule response includes cutoff times. COSCO supports VGM via INTTRA eVGM. Specific VGM cutoff field requires live testing |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ⚠️ | `POST /info/schedule` (cutoff times in response); `GET /info/tracking` (cargo cutoff times) | Cutoff timestamp | `FCO` | Cutoff times documented in both schedule and tracking responses. Specific FCL cutoff field mapping requires live testing |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❓ | Unknown | Unknown | `LCO` | Not explicitly documented. May be conditional on shipment type |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ❓ | `GET /info/tracking/{number}` | Unknown | Inferred from first EquipmentEvent | No explicit assignment event documented in COP tracking API. Presence of container data in tracking response may indicate assignment |
| 3.2 | Empty Container Gate-Out (Pickup) | ⚠️ | `GET /info/tracking/{number}` | Container status updates with timestamps | `GTOT` + `EMPTY` | Tracking API returns dynamic status updates. Specific event codes for gate-out not documented in English materials; requires live testing to confirm event granularity |
| 3.3 | Full Container Gate-In | ⚠️ | `GET /info/tracking/{number}` | Container status updates with timestamps | `GTIN` + `LADEN` | Same as 3.2 -- status updates available but specific event code mapping requires live testing |
| 3.4 | Container Loaded on Vessel | ✅ | `GET /info/tracking/{number}` | Container loaded status with vessel/voyage | `LOAD` + `LADEN` | Tracking response includes vessel name, voyage, and loading status. Web portal shows "Loaded" milestone |
| 3.5 | Container Discharged at Transshipment | ⚠️ | `GET /info/tracking/{number}` | Discharge event at transshipment port | `DISC` + `LADEN` + transshipment | Tracking shows port-level events. Transshipment discharge distinguishable by port context but specific event coding requires live testing |
| 3.6 | Container Loaded at Transshipment | ⚠️ | `GET /info/tracking/{number}` | Loading event at transshipment port | `LOAD` + `LADEN` + transshipment | Same as 3.5 for loading at transshipment |
| 3.7 | Container Discharged at Destination | ✅ | `GET /info/tracking/{number}` | Discharge event at destination port | `DISC` + `LADEN` | Tracking response includes discharge status at destination |
| 3.8 | Full Container Gate-Out (Delivery) | ⚠️ | `GET /info/tracking/{number}` | Container delivery/gate-out status | `GTOT` + `LADEN` | Status updates available. Specific gate-out delivery event code mapping requires live testing |
| 3.9 | Empty Container Returned | ⚠️ | `GET /info/tracking/{number}` | Empty return status | `GTIN` + `EMPTY` | Status updates available. Specific event code mapping requires live testing |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ✅ | `POST /info/schedule`; `GET /info/tracking/{number}` | Estimated departure date in schedule; actual/estimated departure in tracking | `DEPA` + classifier | Both schedule and tracking APIs return departure timestamps |
| 4.2 | Estimated Time of Arrival | ETA | ✅ | `POST /info/schedule`; `GET /info/tracking/{number}` | Estimated arrival date in schedule; actual/estimated arrival in tracking | `ARRI` + classifier | Both schedule and tracking APIs return arrival timestamps |
| 4.3 | Vessel Arrival at Transshipment | -- | ⚠️ | `GET /info/tracking/{number}` | Vessel arrival events at intermediate ports | `ARRI` at intermediate | Tracking shows port-level events. Transshipment arrival distinguishable by port context |
| 4.4 | Vessel Departure from Transshipment | -- | ⚠️ | `GET /info/tracking/{number}` | Vessel departure events at intermediate ports | `DEPA` at intermediate | Same as 4.3 for departures |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❌ | No webhook/push notification system found in COP API documentation. Third-party aggregators (TrackingMore, Tracktry) offer webhook functionality for COSCO tracking as a workaround |
| Event Polling with timestamp filter | ⚠️ | Tracking API supports polling by B/L, booking, or container number. No documented timestamp-based incremental filtering -- full re-fetch appears required on each poll |
| Event Classifier Progression (PLN->EST->ACT) | ⚠️ | Schedule API returns estimated dates; tracking API returns actual dates. No explicit PLN/EST/ACT classifier system documented -- progression must be inferred from data changes between polls |
| Retracted Events | ❌ | No retraction mechanism documented |
| Change Remarks | ❌ | No change remark field documented |
| Delay Reason Codes | ❌ | No delay reason codes documented |

### Coverage Summary

| Category | Fields Available | Fields Partial | Fields Unavailable | Fields Unknown | Coverage % |
|----------|-----------------|---------------|-------------------|----------------|-----------|
| API Domains (1.x) | 4/5 | 1/5 | 0/5 | 0/5 | 80% (+ 1 partial) |
| Cutoffs (2.x) | 0/6 | 3/6 | 0/6 | 3/6 | 0% confirmed (3 partial) |
| Container Milestones (3.x) | 2/9 | 6/9 | 0/9 | 1/9 | 22% (+ 6 partial) |
| Transport Events (4.x) | 2/4 | 2/4 | 0/4 | 0/4 | 50% (+ 2 partial) |
| Change Detection (5.x) | 0/6 | 2/6 | 4/6 | 0/6 | 0% (+ 2 partial) |
| **Total** | **8/30** | **14/30** | **4/30** | **4/30** | **27% confirmed (47% partial, 13% unknown)** |

> **Notes on Coverage:**
> - COSCO's proprietary API exposes a reasonable amount of data, but the English documentation is too sparse to confirm specific field-level coverage for most container milestones and cutoffs.
> - The tracking API returns "dynamic status updates with timestamps" and "cargo cutoff times" according to the GitHub documentation, suggesting that much more data is available than can be confirmed from desk research alone.
> - Container milestone coverage is rated "partial" for most items because the tracking API clearly returns container status events, but the specific event codes and granularity cannot be confirmed without live testing.
> - Cutoffs are similarly "partial" because the schedule and tracking APIs include cutoff data, but the mapping to specific cutoff types (DCO, VCO, FCO, etc.) is not documented in English.
> - Change detection is weak: no webhooks, no timestamp filtering, no event classifier system, and no retraction/remark mechanism documented.
> - The true coverage is likely higher than 23% once live testing reveals the actual event codes and response fields. Estimated real coverage: 50-70% based on the breadth of data mentioned in documentation.

---

## Endpoint Reference

### Tracking / Events

| Endpoint | Method | Lookup Params | Pagination | Response Format | Notes |
|----------|--------|--------------|------------|----------------|-------|
| `/info/tracking/{number}?numberType=bl` | GET | B/L number | None documented | JSON | Cargo tracking by Bill of Lading |
| `/info/tracking/{number}?numberType=bkg` | GET | Booking number | None documented | JSON | Cargo tracking by booking reference |
| `/info/tracking/{number}?numberType=cntr` | GET | Container number | None documented | JSON | Cargo tracking by container number |

### Schedules

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| `/info/schedule` | POST | originCity, destinationCity, fromDate, toDate, pickup, delivery, estimateDate | None documented | JSON | Point-to-point schedule inquiry. Uses COSCO-internal port UUIDs |

### Booking

| Endpoint | Method | Key Params | Pagination | Response Format | Notes |
|----------|--------|-----------|------------|----------------|-------|
| SynConHub Spot Rate v2 | Various | Route, container type, dates | Unknown | JSON | Spot rate inquiry. Documented in `docs/SynConHubApi/EN/Spot Rate v2/` |
| SynConHub Booking v2 | Various | Rate reference, cargo details | Unknown | JSON | Place bookings. Documented in `docs/SynConHubApi/EN/Spot Rate v2/Booking v2.md` |
| SynConHub Cross Booking | Various | Cross-carrier booking params | Unknown | JSON | Cross-carrier bookings. Documented in `docs/SynConHubApi/EN/Cross Booking/` |
| Booking Confirmation Download | GET | Booking reference | None | PDF/Document | Download booking confirmation documents |
| Waybill Download | GET | Order reference | None | Document | Download waybill documents |

### Other Endpoints

| Endpoint | Method | Purpose | Key Params | Notes |
|----------|--------|---------|-----------|-------|
| Order Information Query | GET | Retrieve order/waybill information | Order reference | COP public query group |
| Order Change Query | GET | Track order modifications | Order reference | COP public query group |
| Cargo Receipt Link | GET | Retrieve signature proof | Reference number | COP public query group |
| Pickup Item Verification | GET | Container check codes | Container reference | Domestic trade service only |
| Truck Event Reception | POST | Receive truck/trailer events | Truck/trailer identifiers | Domestic trade service only |

### Lookup Methods Summary

| Identifier Type | Supported? | Which Endpoints? | Notes |
|----------------|-----------|-----------------|-------|
| **Bill of Lading (B/L) number** | ✅ | Tracking API (`numberType=bl`) | Primary lookup method |
| **Booking reference** | ✅ | Tracking API (`numberType=bkg`), SynConHub APIs | Available for both tracking and booking management |
| **Container number** | ✅ | Tracking API (`numberType=cntr`) | Per-container tracking |
| **Carrier booking number** | ✅ | Same as booking reference | Used interchangeably |
| **Vessel IMO / voyage** | ❌ | Not supported as lookup param | Vessel/voyage info returned in responses but not usable as a lookup key |

---

## Rate Limits & Quotas

| Detail | Value | Source |
|--------|-------|--------|
| **Global rate limit** | 1,000 requests/day per API, 30,000 requests/month per API | Official (https://github.com/cop-cos/COP/blob/master/README_en.md) |
| **Per-endpoint limits** | Same account-level limits apply to each API independently | Official |
| **Daily/monthly quota** | 1,000/day and 30,000/month per API | Official |
| **Rate limit response** | Unknown -- likely HTTP 401 or 500 based on general error handling | Estimated |
| **Rate limit by** | Per account (ApiKey) | Official |
| **Burst allowance** | Unknown | Unknown |
| **Different tiers** | Single tier (trial -- free). Future pricing not published | Official |
| **Max request body** | 1 MB | Official |

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | https://elines.coscoshipping.com/ebusiness/cargoTracking |
| **Login required?** | No -- basic tracking available without login |
| **Data available on portal but NOT in API** | Map visualization of container position. Portal may show more event detail than the English API documentation suggests -- needs confirmation |
| **Scraping feasibility** | Not assessed -- API access preferred. Portal is web-based |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Yes |
| **EDI message types** | IFTMIN (Shipping Instructions), COPARN, IFTSTA (Status/Tracking), VERMAS (VGM) -- via INTTRA/E2open |
| **EDI connection method** | Via INTTRA/E2open platform (EDI, XML, web, mobile channels supported) |
| **EDI documentation** | Contact COSCO or INTTRA/E2open directly. Partnership press releases at https://www.inttra.com/newsroom/press-releases/coscon-extends-relationship-with-inttra/ |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Yes | COSCO explicitly listed. B/L and container number lookup supported. Source: https://www.project44.com/container-tracking/ |
| **FourKites** | Yes (reported) | FourKites covers 85+ ocean carriers; COSCO likely covered given market position. Explicit confirmation not found |
| **Vizion** | Yes (reported) | Vizion covers 99% of ocean freight. COSCO covered given #4 global ranking. Explicit confirmation not found |
| **INTTRA / E2open** | Yes | Confirmed partnership for booking, shipping instructions, VGM. Source: https://investors.e2open.com/news/news-details/2021/E2open-and-COSCO-Extend-Global-Partnership-Through-2023/ |
| **CargoSmart** | Yes | COSCO is a founding participant in GSBN (CargoSmart-led consortium). Direct EDI connectivity confirmed. Source: https://www.globenewswire.com/news-release/2019/07/12/1881816/0/en/ |

> **Aggregator note:** Given COSCO's limited English API documentation and proprietary HMAC auth, aggregator integration (particularly project44 or Vizion) may offer a faster path to production for tracking-only use cases. Aggregators provide normalized data without needing to reverse-engineer COSCO's proprietary event codes. For booking and rate functionality, direct COP/SynConHub integration or INTTRA EDI would be required.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown -- not published | Unknown |
| **API uptime/reliability** | Unknown -- no published SLA. COP is in "trial operation" status | Unknown |
| **Historical data depth** | Unknown -- not documented | Unknown |
| **Timezone handling** | Unknown -- not documented in English materials. Likely China Standard Time (CST/UTC+8) given carrier headquarters, but may vary | Estimated |
| **Character encoding** | Unknown -- likely UTF-8 but Chinese character handling may require attention | Estimated |

### Known Issues & Gotchas

- **HMAC-SHA1 authentication complexity**: Unlike OAuth2 or API key auth used by most carriers, COSCO's HMAC auth requires computing signatures per-request with 5 custom headers. The 2-minute timestamp tolerance means system clocks must be accurate. Reference implementations exist in Java, PHP, and Python on GitHub.

- **15-business-day onboarding**: The approval process is among the slowest of major carriers. Plan for 3+ weeks from application to first API call.

- **"Trial operation" status**: The COP platform is still labeled as trial. This raises questions about long-term stability, pricing, and SLA commitments. APIs may change without notice.

- **COSCO-internal port identifiers**: The schedule API uses COSCO-specific port UUIDs (`originCityUuid`, `destinationCityUuid`) rather than standard UN/LOCODEs. A port code translation mechanism will be needed.

- **Sparse English documentation**: Chinese documentation is more comprehensive. The adapter team may need to reference Chinese docs or use live testing to fully understand response schemas and event codes.

- **Modest rate limits**: 1,000 calls/day per API is quite restrictive for production polling across many shipments. At 1 poll per shipment per hour, this supports roughly 40 active shipments. Polling strategy must account for this.

- **No webhooks**: The lack of push notifications means polling is the only option for change detection, which compounds the rate limit constraint.

- **No pagination documented**: The tracking and schedule APIs do not document pagination. Large result sets may be truncated.

### Recently Deprecated or Changed

- No deprecation notices found. The COP platform is relatively new and still in trial.

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | Yes -- COSCO exposes tracking, schedules, booking, and rates through proprietary APIs. The tracking API returns comprehensive shipment data including vessel details, container status, and cutoffs |
| **Implementation effort** | High (proprietary) -- fully proprietary API with no DCSA alignment, custom HMAC auth, COSCO-specific port codes, underdocumented event codes, and modest rate limits |
| **DCSA base adapter usable?** | No -- fully custom. COSCO is not a DCSA member and implements no DCSA standards. The entire response parsing, event mapping, and auth handling must be built from scratch |

### Recommended Approach

The COSCO adapter must be built as a fully custom implementation since COSCO does not implement any DCSA standards. The adapter architecture should focus on three layers:

1. **Auth Layer**: Implement HMAC-SHA1 signature generation per-request, computing the 5 required custom headers (X-Coscon-Date, X-Coscon-Content-Md5, X-Coscon-Digest, X-Coscon-Authorization, X-Coscon-Hmac). Use the reference implementations from the COP GitHub repository as a starting point.

2. **Data Layer**: Map COSCO's proprietary tracking response fields to the canonical data model. The tracking API returns vessel name, voyage, port of loading/discharge, departure/arrival times, container status, and cutoffs -- but the specific field names and event codes need to be discovered through live API testing. A field-mapping configuration should be externalized for easy adjustment.

3. **Polling Layer**: Given no webhook support and a 1,000 calls/day rate limit, implement a smart polling strategy that prioritizes active shipments (in-transit) over inactive ones (delivered, pre-booking). Consider using project44 or Vizion as a tracking data source with COSCO COP for booking/rate operations only.

Alternatively, for a tracking-only integration, using project44 or Vizion as an intermediary would significantly reduce implementation effort and avoid the HMAC auth complexity, rate limit constraints, and event code mapping challenges.

### Recommended Lookup Method

**Bill of Lading (B/L) number** is the recommended primary lookup for tracking, as it is the most common identifier in the shipping workflow and supported by the tracking API (`numberType=bl`).

**Booking reference** as secondary -- useful pre-B/L issuance and supported by both tracking and booking APIs.

**Container number** as supplementary -- for per-container tracking in multi-container shipments.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Every 4-6 hours for in-transit shipments; every 12-24 hours for pre-departure or delivered. Constrained by 1,000 calls/day limit |
| **Incremental filter** | Full re-fetch required -- no timestamp-based filtering documented. Compare against local state to detect changes |
| **Batch tracking** | One API call per shipment. No batch endpoint documented. At 1,000 calls/day, supports ~40-160 active shipments depending on polling frequency |

### Auth Implementation Notes

The HMAC-SHA1 auth handler must:
1. Generate a GMT-formatted timestamp (`EEE, dd MMM yyyy HH:mm:ss z`) within 2 minutes of server time
2. Generate a random UUID and compute its MD5 hash
3. For POST/PUT requests, compute SHA-256 of the request body and Base64-encode with "SHA-256=" prefix
4. Compute the HMAC-SHA1 signature using the SecretKey over the canonical request string
5. Set all 5 `X-Coscon-*` headers on every request

Reference implementations available at:
- Java: https://github.com/cop-cos/COP (HttpClient and pure Java examples)
- PHP: https://github.com/cop-cos/COP
- Python: https://github.com/cop-cos/COP

### Edge Cases to Handle

- **COSCO-internal port UUIDs**: Schedule API requires COSCO-specific `originCityUuid` and `destinationCityUuid` values, not standard UN/LOCODEs. A port code mapping/lookup mechanism is needed, possibly requiring a separate API call or static mapping table.

- **Chinese character data**: Response fields may contain Chinese characters (port names, vessel names, status descriptions). Ensure UTF-8 handling throughout the adapter pipeline.

- **Rate limit exhaustion**: With only 1,000 calls/day per API, exceeding limits could block all tracking for the remainder of the day. Implement strict rate limit accounting and backoff.

- **Undocumented event codes**: Container milestone event codes are not fully documented in English. The adapter will need a discovery phase during live testing to catalog all possible status codes and map them to canonical milestones.

- **Trial platform instability**: COP is in "trial operation" -- APIs may change, experience downtime, or be deprecated without standard notice periods.

### Mapping Complexity

**High complexity.** COSCO's API is fully proprietary with no DCSA alignment, meaning every field must be custom-mapped:

1. **Event code discovery**: The tracking API's event/status codes are not documented in the English materials. A live testing phase is required to catalog all possible status values and map them to canonical container milestones (GTOT, GTIN, LOAD, DISC, etc.).

2. **Cutoff field extraction**: Cutoff data is mentioned in schedule and tracking responses but specific field names and structure are undocumented in English. Requires live testing.

3. **Port code translation**: COSCO uses proprietary port identifiers instead of UN/LOCODEs. Bidirectional mapping needed.

4. **Schedule response parsing**: The schedule API response structure (array of sailings with nested vessel/port/cutoff data) needs full schema discovery via live testing.

5. **No event classifier system**: Unlike DCSA carriers that use PLN/EST/ACT classifiers, COSCO's event progression model is unknown. Change detection requires comparing timestamps and status values between polls.

---

## Open Questions

- [ ] What are the complete event/status codes returned by the tracking API? -- Critical for mapping container milestones
- [ ] What is the full JSON response schema for the tracking endpoint? -- English documentation only describes fields at a high level
- [ ] What specific cutoff fields are included in the schedule and tracking responses? -- Need to map to DCO, VCO, FCO, etc.
- [ ] Does the schedule API accept UN/LOCODEs or only COSCO-internal port UUIDs? -- Important for port code mapping
- [ ] What happens when the daily rate limit (1,000 calls) is exceeded? -- HTTP status code and retry behavior
- [ ] Is the COP platform planned to exit "trial" status? -- Affects long-term reliability assessment
- [ ] Does SSL have an existing business relationship with COSCO? -- Would accelerate the 15-business-day onboarding
- [ ] Are there undocumented API endpoints beyond what is listed on GitHub? -- COP portal (behind login) may reveal additional APIs
- [ ] Does the tracking API support any form of timestamp-based filtering? -- Would improve polling efficiency
- [ ] What is the data freshness of tracking events? -- How quickly do physical events appear in the API?

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | https://lines.coscoshipping.com |
| COP Developer Portal | https://cop.lines.coscoshipping.com/ |
| COP GitHub Repository | https://github.com/cop-cos/COP |
| COP README (English) | https://github.com/cop-cos/COP/blob/master/README_en.md |
| Cargo Tracking Documentation | https://github.com/cop-cos/COP/blob/master/docs/info-cargotracking-en.md |
| Schedule API Documentation | https://github.com/cop-cos/COP/blob/master/docs/info-schedule.md |
| SynConHub API Documentation | https://github.com/cop-cos/COP/tree/master/docs/SynConHubApi/EN |
| SynConHub Platform | https://synconhub.coscoshipping.com/ |
| Web Portal Tracking | https://elines.coscoshipping.com/ebusiness/cargoTracking |
| API Production Endpoint | https://api.lines.coscoshipping.com/service |
| API Test Endpoint | https://api-pp.lines.coscoshipping.com/service |
| COSCO-INTTRA Partnership | https://www.inttra.com/newsroom/press-releases/coscon-extends-relationship-with-inttra/ |
| COSCO-E2open Partnership | https://investors.e2open.com/news/news-details/2021/E2open-and-COSCO-Extend-Global-Partnership-Through-2023/ |
| GSBN Consortium | https://www.globenewswire.com/news-release/2019/07/12/1881816/0/en/ |
| DCSA Courts COSCO | https://www.seatrade-maritime.com/middle-east-africa/digital-container-shipping-association-courts-cosco-10th-member |
| project44 COSCO Tracking | https://www.project44.com/container-tracking/ |
| project44 COSCO Sailing Schedule | https://www.project44.com/ocean-visibility/cosco-shipping-lines |
