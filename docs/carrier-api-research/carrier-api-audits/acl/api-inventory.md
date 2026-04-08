# Atlantic Container Line (ACL) -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing. Research based on ACL's public website (aclcargo.com), MyACL portal inspection, ACL EDI documentation, Grimaldi GNET WebAPI documentation, third-party aggregator coverage listings, and public web presence. No API credentials were obtained or used.
> **Researched by**: Agent (carrier API audit workflow)
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | Atlantic Container Line AB (ACL) |
| **SCAC Code** | ACLU |
| **Parent Company** | Grimaldi Group (wholly-owned subsidiary) |
| **Alliance** | Independent (not a member of 2M, THE Alliance, or Ocean Alliance) |
| **Primary Services** | ConRo (container + RoRo hybrid), containers, oversized/breakbulk, vehicles, project cargo |
| **Market Position** | Oldest continuously operating container line (since 1967). Specialized transatlantic ConRo carrier operating 5 G4-class vessels on fixed weekly North Atlantic schedule. Niche but important for oversized and RoRo cargo between North America and Europe. Claims zero containers lost in 40+ years |
| **Headquarters** | Westfield, New Jersey, USA (Swedish-registered company) |
| **Website** | [https://www.aclcargo.com](https://www.aclcargo.com) |

### Relationship to Grimaldi Group

ACL is a wholly-owned subsidiary of Grimaldi Group (Naples, Italy) but operates with significant independence:

| Aspect | ACL | Grimaldi Lines |
|--------|-----|---------------|
| **SCAC** | ACLU | GRIM |
| **Website** | aclcargo.com | grimaldi-lines.com |
| **Customer portal** | MyACL (myacl.aclcargo.com) | GNET (gnet.grimaldi-eservice.com) |
| **Tracking technology** | ASP.NET/DevExpress (MyACL) | ASP.NET WebForms/jQuery (GNET) |
| **Trade focus** | North Atlantic (US/Canada -- Northern Europe) | Mediterranean, West Africa, South America |
| **Vessel type** | G4-class ConRo | Various RoRo, ConRo, container |

**Key finding**: ACL operates its own separate digital infrastructure. The MyACL portal at `myacl.aclcargo.com` is a distinct application from Grimaldi's GNET platform. ACL's tracking endpoint (`/MyACLView/ShipmentTracking/SearchByShipmentNumber`) is a proprietary ASP.NET backend, not the GNET WebAPI. There is **no evidence** that ACL shipments can be tracked through Grimaldi's GNET API, nor that ACL exposes a public REST API for programmatic access.

### G4-Class ConRo Fleet

ACL operates 5 G4-class ConRo vessels on a fixed weekly North Atlantic schedule:

| Vessel | IMO | Capacity |
|--------|-----|----------|
| Atlantic Star | 9670585 | 3,807 TEU + 28,900 m2 RoRo |
| Atlantic Sail | 9670597 | 3,807 TEU + 28,900 m2 RoRo |
| Atlantic Sea | 9670602 | 3,807 TEU + 28,900 m2 RoRo |
| Atlantic Sky | 9670614 | 3,807 TEU + 28,900 m2 RoRo |
| Atlantic Sun | 9670626 | 3,807 TEU + 28,900 m2 RoRo |

Key ports: Halifax, New York, Baltimore, Liverpool, Antwerp, Hamburg.

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | **No** -- ACL does not have a public developer portal or API documentation |
| **Developer portal URL** | N/A |
| **API documentation URL(s)** | N/A -- no public API documentation found |
| **Documentation quality** | None -- no API documentation exists |
| **OpenAPI/Swagger spec available?** | No |
| **Sandbox/test environment?** | No |
| **Developer registration** | N/A |
| **Developer support channels** | General contact via aclcargo.com; EDI partnership inquiries to Loren Paul (North America, Westfield NJ) or Daniel Hunter (Europe, Liverpool) |
| **Community/third-party libraries** | None found -- no GitHub repos, npm packages, or PyPI packages for ACL API integration |
| **API changelog / release notes** | N/A |

### MyACL Portal Overview

The **MyACL** portal at `myacl.aclcargo.com` is ACL's customer-facing web application providing:

- **Shipment tracking** -- search by shipment number or container number (not case-sensitive, supports multiple entries separated by comma/semicolon/space)
- **Invoice access** -- view and download invoices
- **Bill of Lading** -- access B/L documents
- **VGM submission** -- submit Verified Gross Mass declarations
- **Account management** -- customer registration and login

The portal is built on ASP.NET with DevExpress components (dxDataGrid) and jQuery UI. The tracking backend endpoint is `POST /MyACLView/ShipmentTracking/SearchByShipmentNumber` which accepts JSON parameters. This is an internal web endpoint, not a documented public API.

A separate legacy portal exists at `myaclt.aclcargo.com` with EDI information.

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | **No** -- ACL is not a DCSA member. Neither ACL nor its parent Grimaldi Group are DCSA members |
| **DCSA APIs implemented** | None |
| **DCSA TNT version** | N/A |
| **DCSA Booking version** | N/A |
| **DCSA Schedules version** | N/A |
| **Known DCSA deviations** | N/A -- no DCSA implementation |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | **Yes (confirmed)** | ACL supports ANSI X12 and EDIFACT message types for booking, B/L, manifest, tracking, gate activity, invoicing. Requires Trading Partner Agreement |
| **INTTRA integration** | Unknown | Not confirmed from public sources |
| **BIC (Bureau International des Containers)** | Yes (confirmed) | Container IDs use BIC ISO 6346 format with ACLU prefix |
| **UN/LOCODE** | Yes (likely) | Standard port codes used in shipping operations |

### EDI Message Types (Confirmed)

ACL supports a comprehensive set of EDI message types:

| Function | ANSI X12 | EDIFACT |
|----------|----------|---------|
| Booking Request | 300 | IFTMBF |
| Booking Confirmation | 301 | IFTMBC |
| B/L Instructions | 304 | IFTMIN |
| Ocean Manifest | 309 | IFTMCS |
| Export B/L Invoice | 310 | INVOIC |
| Import Arrival Notice | 312 | IFTMAN |
| Shipment Status Updates | **315** | **IFTSTA** |
| Gate Activity | **322** | **CODECO** |
| Electronic Funds Transfer | 820 | N/A |

The **IFTSTA (315)** and **CODECO (322)** message types are particularly relevant for SSL's tracking needs -- they provide shipment status updates and gate activity events respectively.

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | N/A -- no public API. MyACL portal uses session-based web authentication (username/password login) |
| **Auth documentation** | N/A |
| **Registration process** | MyACL registration available at myacl.aclcargo.com; requires a customer relationship with ACL |
| **Registration URL** | [https://myacl.aclcargo.com](https://myacl.aclcargo.com) |
| **Partner program required?** | Yes -- for EDI integration, a Trading Partner Agreement is required |
| **Partner program URL** | [https://www.aclcargo.com/electronic-data-interchange/](https://www.aclcargo.com/electronic-data-interchange/) |
| **Credential type** | Username + Password (MyACL portal); EDI requires formal Trading Partner Agreement |
| **Token refresh supported?** | N/A |
| **Token lifetime** | N/A |
| **Access tiers** | Single tier -- MyACL customer access |
| **IP whitelisting required?** | Unknown |

### Access Requirements Summary for SSL

ACL does not expose a public REST API. There are two programmatic access paths:

1. **EDI (IFTSTA/CODECO)**: SSL can establish an EDI Trading Partner Agreement with ACL to receive shipment status updates (IFTSTA/315) and gate activity (CODECO/322) messages. This requires an internal system capable of processing EDIFACT or ANSI X12 messages and likely an AS2 or SFTP connection. Contacts: Loren Paul (North America), Daniel Hunter (Europe).

2. **Third-party aggregator**: SSL can access ACL tracking data through aggregators like Terminal49, Shipsgo, Portcast, or Vizion, which have ACL (ACLU) carrier coverage. This is the fastest path to integration but adds a dependency and per-container cost.

There is no self-service API registration process.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field must have a row.
> Availability assessment is based on: (a) what the MyACL web portal displays, (b) what EDI messages can carry, and (c) what third-party aggregators provide.
> Since ACL has no public API, "Carrier Endpoint" refers to the access method (EDI, portal, or aggregator).

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ⚠️ | MyACL portal (web only), aclcargo.com/schedules | Schedule search on portal; no API | DCSA CS `vessel-schedules` | Vessel schedules viewable on website and MyACL portal. No programmatic access. Fixed weekly schedule simplifies this (5 vessels, known rotation) |
| 1.2 | Point-to-Point Route Options | ⚠️ | MyACL portal (web only) | Schedule enquiry on portal | DCSA CS `point-to-point-routes` | Limited relevance -- ACL operates a fixed weekly rotation with minimal route variation. P2P routing is essentially the fixed schedule |
| 1.3 | Booking Lifecycle | ⚠️ | EDI (IFTMBF/300 → IFTMBC/301) | ANSI X12 300/301, EDIFACT IFTMBF/IFTMBC | DCSA BKG | Booking request and confirmation available via EDI. No REST API |
| 1.4 | Shipping Instructions | ⚠️ | EDI (IFTMIN/304) | ANSI X12 304, EDIFACT IFTMIN | DCSA eDoc | B/L instructions via EDI. No REST API |
| 1.5 | Rates | ❌ | N/A | N/A | Not DCSA | No rate API. Rates obtained through ACL sales representatives |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❓ | Unknown | Unknown | `ECP` | Not visible in public documentation. May be communicated in booking confirmation (EDI 301/IFTMBC) |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❓ | Unknown | Unknown | `EFC` | Same as above |
| 2.3 | Documentation Cutoff | DCO | ❓ | Unknown | Unknown | `DCO` | Likely communicated via booking confirmation or MyACL portal but not confirmed |
| 2.4 | VGM Cutoff | VCO | ❓ | Unknown | Unknown | `VCO` | VGM submission available on MyACL portal; cutoff timestamp not confirmed as a data field |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ❓ | Unknown | Unknown | `FCO` | Standard cutoff for any container carrier; likely communicated but not confirmed in digital format |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❓ | Unknown | Unknown | `LCO` | ACL handles some LCL/groupage but cutoff data not confirmed |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ❓ | Unknown | Unknown | Inferred from first EquipmentEvent | Not visible in public documentation |
| 3.2 | Empty Container Gate-Out (Pickup) | ⚠️ | EDI (CODECO/322), MyACL portal, Aggregators | EDI CODECO gate-out event; portal tracking event | `GTOT` + `EMPTY` | Gate activity available via EDI (322/CODECO). Also visible on MyACL tracking portal and through aggregators like Terminal49 |
| 3.3 | Full Container Gate-In | ⚠️ | EDI (CODECO/322), MyACL portal, Aggregators | EDI CODECO gate-in event; portal tracking event | `GTIN` + `LADEN` | Same as 3.2 -- gate activity covered by EDI and portal |
| 3.4 | Container Loaded on Vessel | ⚠️ | EDI (IFTSTA/315), MyACL portal, Aggregators | EDI IFTSTA load event; portal "Vessel Loaded" | `LOAD` + `LADEN` | Shipment status update via EDI (315/IFTSTA). Terminal49 confirms "Vessel Loaded" milestone |
| 3.5 | Container Discharged at Transshipment | ❌ | N/A | N/A | `DISC` + `LADEN` + transshipment | ACL operates direct services with minimal transshipment on its own vessels. Transshipment events are rare/not applicable for most ACL shipments |
| 3.6 | Container Loaded at Transshipment | ❌ | N/A | N/A | `LOAD` + `LADEN` + transshipment | Same as 3.5 -- direct service, minimal transshipment |
| 3.7 | Container Discharged at Destination | ⚠️ | EDI (IFTSTA/315), MyACL portal, Aggregators | EDI IFTSTA discharge event; portal "Vessel Discharged" | `DISC` + `LADEN` | Terminal49 confirms "Vessel Discharged" milestone |
| 3.8 | Full Container Gate-Out (Delivery) | ⚠️ | EDI (CODECO/322), MyACL portal, Aggregators | EDI CODECO gate-out event | `GTOT` + `LADEN` | Gate activity via EDI and portal |
| 3.9 | Empty Container Returned | ⚠️ | EDI (CODECO/322), MyACL portal, Aggregators | EDI CODECO gate-in empty event | `GTIN` + `EMPTY` | Gate activity via EDI and portal |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ⚠️ | MyACL portal, Aggregators | Portal tracking field; aggregator ETD field | `DEPA` + classifier | Available on MyACL portal and through aggregators. Terminal49 provides ETD data. No API access |
| 4.2 | Estimated Time of Arrival | ETA | ⚠️ | EDI (IFTMAN/312), MyACL portal, Aggregators | EDI arrival notice; portal ETA field | `ARRI` + classifier | Import Arrival Notice (312/IFTMAN) provides ETA. Also on portal and aggregators |
| 4.3 | Vessel Arrival at Transshipment | -- | ❌ | N/A | N/A | `ARRI` at intermediate | Not applicable -- ACL operates direct services with fixed weekly rotation. Minimal transshipment |
| 4.4 | Vessel Departure from Transshipment | -- | ❌ | N/A | N/A | `DEPA` at intermediate | Same as 4.3 |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❌ | No webhook/push capability. No API |
| Event Polling with timestamp filter | ❌ | No API to poll |
| Event Classifier Progression (PLN->EST->ACT) | ❌ | No DCSA event model |
| Retracted Events | ❌ | No event retraction mechanism |
| Change Remarks | ❌ | No structured change detection |
| Delay Reason Codes | ❌ | No standardized delay codes |

### Coverage Summary

| Category | Fields Available | Fields Unavailable | Fields Unknown | Coverage % |
|----------|-----------------|-------------------|----------------|-----------|
| API Domains (1.x) | 0/5 | 1/5 | 0/5 | 0% (direct API); ~60% via EDI |
| Cutoffs (2.x) | 0/6 | 0/6 | 6/6 | 0% (unknown) |
| Container Milestones (3.x) | 0/9 | 2/9 | 1/9 | 0% (direct API); ~67% via EDI/aggregator |
| Transport Events (4.x) | 0/4 | 2/4 | 0/4 | 0% (direct API); ~50% via EDI/aggregator |
| Change Detection (5.x) | 0/6 | 6/6 | 0/6 | 0% |
| **Total** | **0/30** | **11/30** | **7/30** | **0% direct API; est. 40-50% via EDI+aggregator** |

> **Important notes on coverage assessment**:
>
> - ACL has **no public REST API** -- all availability ratings reflect access via EDI, the MyACL web portal, or third-party aggregators, not direct API calls.
>
> - **Container milestones (3.x)**: Rated ⚠️ for 6 of 9 fields because they are accessible through EDI (IFTSTA/CODECO) and the MyACL portal, but not via a programmatic API. Transshipment events (3.5, 3.6) are marked ❌ because ACL operates direct services with minimal transshipment.
>
> - **EDI as primary data channel**: ACL's EDI support (IFTSTA for status, CODECO for gate activity, IFTMAN for arrival notice) is the most data-rich programmatic path. However, EDI requires a Trading Partner Agreement and infrastructure for message processing.
>
> - **Aggregator coverage**: Terminal49, Shipsgo, Portcast, and Vizion all list ACL (ACLU) as a supported carrier, providing an alternative programmatic path for tracking data.

---

## Endpoint Reference

ACL does not expose a public REST API. The following documents the internal web endpoint discovered during research and the EDI access methods.

### MyACL Internal Web Endpoints (Not Public API)

| Endpoint | Method | Description | Key Params | Auth Required | Notes |
|----------|--------|-------------|-----------|--------------|-------|
| `/MyACLView/ShipmentTracking/SearchByShipmentNumber` | POST | Shipment/container tracking search | JSON body with shipment numbers, captcha settings | Yes (session cookie) | Internal web endpoint used by MyACL portal. Not a documented public API. Uses DevExpress data grid for display |

### EDI Access (Primary Programmatic Path)

| EDI Type | Direction | ANSI X12 | EDIFACT | Data Available |
|----------|-----------|----------|---------|---------------|
| Shipment Status | ACL -> Customer | 315 | IFTSTA | Container milestones, load/discharge events, vessel info |
| Gate Activity | ACL -> Customer | 322 | CODECO | Gate-in, gate-out events at terminals |
| Arrival Notice | ACL -> Customer | 312 | IFTMAN | Import arrival details, ETA |
| Booking Request | Customer -> ACL | 300 | IFTMBF | Booking creation |
| Booking Confirmation | ACL -> Customer | 301 | IFTMBC | Booking confirmed with details |
| B/L Instructions | Customer -> ACL | 304 | IFTMIN | Shipping instruction submission |
| Ocean Manifest | ACL -> Customer | 309 | IFTMCS | Manifest data |
| Invoice | ACL -> Customer | 310 | INVOIC | Freight invoice |

### Lookup Methods Summary

| Identifier Type | Supported? | Which Methods? | Notes |
|----------------|-----------|----------------|-------|
| **Shipment Number** | ⚠️ | MyACL portal, EDI | Primary identifier on MyACL portal. Format unknown (ACL-specific) |
| **Container Number** | ⚠️ | MyACL portal, Aggregators | Supported on portal and via aggregators. BIC ISO 6346 format with ACLU prefix |
| **Bill of Lading (B/L) number** | ⚠️ | MyACL portal (likely), Aggregators | Terminal49 confirms B/L tracking. B/L prefix: ACLU |
| **Booking reference** | ⚠️ | EDI (IFTMBF/IFTMBC), MyACL portal | Via EDI booking messages and portal |
| **Vessel IMO / voyage** | ⚠️ | MyACL portal (schedule search) | Schedule search on portal. No API access |

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

## Webhook / Push Support

| Detail | Value |
|--------|-------|
| **Webhooks supported?** | **No** -- ACL has no API and no webhook capability |
| **Alternative** | EDI push (IFTSTA/CODECO messages sent by ACL to trading partners) or aggregator webhooks (Terminal49 offers webhook push) |

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | [https://myacl.aclcargo.com/MyACLView/ShipmentTracking/Search/Search](https://myacl.aclcargo.com/MyACLView/ShipmentTracking/Search/Search) |
| **Alternative URL** | [https://www.aclcargo.com/track-cargo/](https://www.aclcargo.com/track-cargo/) (redirects to MyACL) |
| **Login required?** | The tracking page appears accessible, but detailed tracking likely requires MyACL login |
| **Data available on portal** | Shipment/container numbers, equipment info, tracking status, location, timestamps, voyage details, POL/POD, terminal info, ETA |
| **Scraping feasibility** | Difficult -- ASP.NET with DevExpress components, session-based auth, CAPTCHA protection on search endpoint. ToS likely prohibits |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | **Yes (confirmed)** -- ACL has been a pioneer in EDI and supports comprehensive message types |
| **EDI message types** | IFTMBF/300 (booking request), IFTMBC/301 (booking confirm), IFTMIN/304 (B/L instructions), IFTMCS/309 (manifest), INVOIC/310 (invoice), IFTMAN/312 (arrival notice), **IFTSTA/315 (shipment status)**, **CODECO/322 (gate activity)**, 820 (EFT) |
| **EDI standards** | ANSI X12 Version 3030 and UN/EDIFACT |
| **EDI connection method** | Unknown -- likely AS2 or VAN (Value Added Network) |
| **EDI documentation** | [https://www.aclcargo.com/electronic-data-interchange/](https://www.aclcargo.com/electronic-data-interchange/) |
| **EDI contacts** | North America: Loren Paul (Westfield, NJ); Europe: Daniel Hunter (Liverpool) |
| **Trading Partner Agreement** | Required -- extends B/L Terms & Conditions to EDI transactions |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Confidence | Notes |
|-----------|-------------------|------------|-------|
| **Terminal49** | **Yes (confirmed)** | High | Lists ACLU as supported carrier. Provides B/L and booking number tracking. Webhook push available. Data freshness: "within minutes". 99.5% uptime SLA |
| **Shipsgo** | **Yes (confirmed)** | High | Offers ACL Tracking API with unlimited API calls. Live map feature |
| **Portcast** | **Yes (confirmed)** | High | Lists ACL in carrier coverage. Provides predictive visibility and API access |
| **Vizion** | Likely Yes | Medium | Claims 99% ocean freight coverage. ACL likely included but not explicitly confirmed |
| **FourKites** | Unknown | Low | Primarily trucking-focused |
| **INTTRA / E2open** | Unknown | Medium | Large ocean B2B platform; ACL may be connected |
| **CargoSmart** | Unknown | Low | Focuses on major container carriers; ACL is niche |
| **GoComet** | **Yes (confirmed)** | High | Lists ACL in carrier tracking coverage |

> **Aggregator note**: Since ACL has no public API, aggregators represent the most practical path for programmatic tracking integration. Terminal49 and Shipsgo both provide confirmed API access to ACL tracking data. Terminal49 in particular offers webhook push notifications, B/L tracking support, and standardized milestone data -- capabilities that ACL's own infrastructure lacks.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown for direct ACL data. Terminal49 reports data "within minutes" via aggregation | Terminal49 documentation (reported) |
| **API uptime/reliability** | N/A -- no API. MyACL portal uptime unknown | N/A |
| **Historical data depth** | Unknown -- MyACL portal tracking history depth not confirmed | Unknown |
| **Timezone handling** | Unknown -- not documented. Likely local port time for portal, UTC for EDI | Unknown |
| **Character encoding** | Unknown -- likely UTF-8 (standard ASP.NET) | Estimated |

### Known Issues & Gotchas

- **No public API** -- ACL is one of the few carriers in the SSL priority list without any form of public REST/SOAP API. All programmatic access must go through EDI or third-party aggregators.
- **Separate from Grimaldi GNET** -- Despite being a Grimaldi subsidiary, ACL's MyACL portal is a completely separate system from Grimaldi's GNET WebAPI. ACL shipments cannot be tracked via GNET API endpoints (confirmed by the distinct technology stacks and URL structures).
- **ConRo vessel specifics** -- ACL's G4-class ConRo vessels carry both containers and RoRo cargo. Container tracking and RoRo tracking may use different mechanisms on the MyACL portal. The adapter needs to handle containerized cargo specifically.
- **Fixed route simplification** -- ACL operates a fixed weekly rotation (Halifax-New York-Baltimore-Liverpool-Antwerp-Hamburg and reverse). This means vessel schedule data is highly predictable and could be partially hardcoded or inferred from the known rotation.
- **CAPTCHA on tracking** -- The MyACL tracking search endpoint includes CAPTCHA parameters, indicating anti-bot protection that would prevent direct web scraping.
- **Limited transshipment** -- ACL's direct service means transshipment events (3.5, 3.6, 4.3, 4.4) are rarely applicable. When they occur, they may involve Grimaldi vessels on connecting services (e.g., ACL to US, then Grimaldi to West Africa).
- **B/L prefix** -- ACL Bills of Lading and container numbers use the ACLU prefix.

### Recently Deprecated or Changed

- ACL's portal has migrated from `myacl.aclcargo.com` (legacy PHP-based) to `my.aclcargo.com/myacl` (newer ASP.NET). The legacy PHP site at `myaclt.aclcargo.com` still hosts EDI documentation.
- No other publicly documented deprecations.

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | **Partial** -- a direct ACL adapter requires either EDI infrastructure or aggregator integration. There is no REST API to wrap. The aggregator path (Terminal49 or Shipsgo) provides the fastest time-to-value |
| **Implementation effort** | **Very High (no API)** for direct integration; **Low-Medium** for aggregator-based adapter |
| **DCSA base adapter usable?** | **No** -- ACL has no DCSA implementation. If using an aggregator, the aggregator's data model would be the mapping source |

### Recommended Approach

**Primary: Third-party aggregator integration (Terminal49 recommended).**

Since ACL has no public REST API, the recommended approach is to integrate through a third-party aggregator. Terminal49 is the strongest candidate because:

1. **Confirmed ACLU support** with B/L and booking number tracking
2. **Webhook push notifications** -- eliminates the need for polling
3. **Standardized milestone data** -- Terminal49 normalizes carrier data into a consistent format
4. **99.5% uptime SLA** and data freshness "within minutes"
5. **Free tier available** (100 containers) for testing and development

The adapter architecture would be:

```
SDK CarrierAdapter (ACL / ACLU)
    |
    +-- Terminal49 API (or Shipsgo API)
        |
        +-- Track by B/L: GET /containers?bl_number=ACLU...
        +-- Track by booking: GET /containers?booking_number=...
        +-- Webhooks: POST callback for milestone updates
        +-- Milestones: vessel loaded, discharged, gate-in/out, ETA/ETD
```

**Secondary: EDI integration (for deeper data access).**

If SSL establishes an EDI Trading Partner Agreement with ACL, the adapter could process IFTSTA (shipment status) and CODECO (gate activity) messages for richer milestone data. This requires EDI infrastructure (AS2/SFTP, message parsing) but provides the most complete data coverage. EDI would be the only path to booking lifecycle data (IFTMBF/IFTMBC) and B/L instructions (IFTMIN).

**Not recommended: Web scraping.** The MyACL portal uses CAPTCHA protection, ASP.NET session state, and DevExpress components that make scraping fragile and likely ToS-violating.

### Recommended Lookup Method

**Bill of Lading number** is the recommended primary lookup method when using aggregators (Terminal49 confirms B/L support for ACLU). **Shipment number** is primary for the MyACL portal and EDI.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | N/A if using Terminal49 webhooks (push-based). If using a polling aggregator, every 4-6 hours is sufficient given ACL's weekly sailing frequency |
| **Incremental filter** | Depends on aggregator API -- Terminal49 provides webhook push eliminating need for polling |
| **Batch tracking** | Aggregator-dependent. Terminal49 supports bulk container tracking |

### Auth Implementation Notes

For aggregator integration (Terminal49):
- Register for Terminal49 API key (free tier: 100 containers)
- Use API key in requests to Terminal49's REST API
- Configure webhook callback URL for push notifications

For EDI integration:
- Establish Trading Partner Agreement with ACL
- Configure AS2/SFTP connection
- Implement EDIFACT/ANSI X12 message parser for IFTSTA and CODECO

### Edge Cases to Handle

- **ConRo mixed cargo**: A single ACL voyage carries both containers and RoRo cargo. Ensure the adapter filters for containerized cargo only (unless RoRo tracking is also needed).
- **Grimaldi connecting services**: Some ACL shipments may connect to Grimaldi Lines vessels for onward transport (e.g., US to West Africa via ACL transatlantic + Grimaldi south). In these cases, tracking may need to span both carriers.
- **Fixed schedule predictability**: ACL's weekly rotation is highly predictable. If real-time ETD/ETA data is unavailable, the published schedule can serve as a reliable baseline with known port call sequences.
- **Limited fleet**: With only 5 vessels on a fixed rotation, vessel identification is simplified. AIS data can supplement tracking if API/EDI data is sparse.
- **Port coverage**: ACL serves a small number of ports (Halifax, New York, Baltimore, Liverpool, Antwerp, Hamburg). This limited scope simplifies both tracking and testing.

### Mapping Complexity

**Low-Medium complexity** if using an aggregator (Terminal49/Shipsgo normalize data into standard formats).

**High complexity** if using EDI directly -- EDIFACT IFTSTA and CODECO messages require specialized parsing and mapping to the canonical data model. Each EDI segment (BGM, DTM, LOC, EQD, RFF, etc.) needs to be mapped to the corresponding DCSA-style event fields.

---

## Open Questions

- [ ] **Q1: Does SSL currently ship with ACL?** -- Need to confirm ACL volume and whether SSL uses ACL for transatlantic shipments, Grimaldi connecting services, or both.
- [ ] **Q2: EDI feasibility?** -- Does SSL have existing EDI infrastructure (AS2/SFTP, message parser)? If not, the aggregator path is strongly preferred.
- [ ] **Q3: Aggregator budget?** -- Terminal49 charges per container after the free tier. What is the acceptable per-shipment cost for ACL tracking?
- [ ] **Q4: Is the MyACL tracking available without login?** -- Could not fully confirm whether the shipment tracking search requires authentication or is publicly accessible.
- [ ] **Q5: Does ACL share any backend data with Grimaldi?** -- While the web portals are separate, the backend ERP systems may share data. If SSL already has GNET API credentials for Grimaldi, it is worth testing whether ACL shipment numbers or container numbers return data from the GNET API.
- [ ] **Q6: RoRo tracking needed?** -- Does SSL ship rolling cargo via ACL, or only containers? This affects which tracking mechanisms are relevant.
- [ ] **Q7: Cutoff data availability** -- Are cutoff timestamps (DCO, VCO, FCO) communicated in ACL's booking confirmation EDI (301/IFTMBC)? This is the most likely source but not confirmed.

---

## Source Links

| Resource | URL | Status |
|----------|-----|--------|
| ACL Website | [https://www.aclcargo.com](https://www.aclcargo.com) | Active |
| MyACL Portal | [https://myacl.aclcargo.com](https://myacl.aclcargo.com) | Active |
| MyACL Tracking | [https://myacl.aclcargo.com/MyACLView/ShipmentTracking/Search/Search](https://myacl.aclcargo.com/MyACLView/ShipmentTracking/Search/Search) | Active |
| ACL Track & Trace Page | [https://www.aclcargo.com/track-trace/](https://www.aclcargo.com/track-trace/) | Active |
| ACL Track Cargo Page | [https://www.aclcargo.com/track-cargo/](https://www.aclcargo.com/track-cargo/) | Active |
| ACL EDI Documentation | [https://www.aclcargo.com/electronic-data-interchange/](https://www.aclcargo.com/electronic-data-interchange/) | Active |
| ACL History | [https://www.aclcargo.com/history/](https://www.aclcargo.com/history/) | Active |
| ACL Fleet (Atlantic Sea) | [https://www.aclcargo.com/about/our-fleet/atlantic-sea/](https://www.aclcargo.com/about/our-fleet/atlantic-sea/) | Active |
| MyACL Legacy (EDI) | [https://myaclt.aclcargo.com/EDI.php](https://myaclt.aclcargo.com/EDI.php) | Active |
| Grimaldi GNET (parent) | [https://www.gnet.grimaldi-eservice.com](https://www.gnet.grimaldi-eservice.com) | Active |
| Terminal49 ACL Coverage | [https://terminal49.com/shipping-lines/aclu-atlantic-container-line-container-tracking](https://terminal49.com/shipping-lines/aclu-atlantic-container-line-container-tracking) | Active |
| Shipsgo ACL Tracking | [https://shipsgo.com/ocean/carriers/acl/container-tracking](https://shipsgo.com/ocean/carriers/acl/container-tracking) | Active |
| Portcast ACL Coverage | [https://www.portcast.io/carrier-coverage/acl-atlantic-container-line-tracking](https://www.portcast.io/carrier-coverage/acl-atlantic-container-line-tracking) | Active |
| Grimaldi Group Corporate | [https://www.grimaldi.napoli.it](https://www.grimaldi.napoli.it) | Active |
| DCSA Member List | [https://dcsa.org/about-us/](https://dcsa.org/about-us/) | ACL NOT listed as member |
