# Grimaldi Lines — API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only — not verified with live API testing. Research based on the GNET WebAPI Help page (publicly accessible endpoint documentation with sample responses), GNET web portal inspection, DCSA membership records, Grimaldi Group corporate sites, and public web presence. No API credentials were obtained or used.
> **Researched by**: Agent (carrier API audit re-audit workflow)
> **Date**: 2026-02-11
> **Last verified**: 2026-02-11

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | Grimaldi Lines (Grimaldi Group S.p.A.) |
| **SCAC Code** | GRIM |
| **Parent Company** | Grimaldi Group (family-owned, Naples, Italy) |
| **Alliance** | Independent (not a member of 2M, THE Alliance, or Ocean Alliance) |
| **Primary Services** | RoRo (Roll-on/Roll-off), container, car carriers, project cargo, passenger ferries |
| **Market Position** | World's largest operator of RoRo vessels; niche but important in Mediterranean, West Africa, South America, and North America trades. Not a top-10 container carrier by TEU volume but significant in specialized cargo |
| **Headquarters** | Naples, Italy |
| **Website** | [https://www.grimaldi-lines.com/en/](https://www.grimaldi-lines.com/en/) |

### Grimaldi Group Corporate Structure (Relevant Entities)

| Entity | SCAC | Role | Digital Infrastructure |
|--------|------|------|----------------------|
| **Grimaldi Lines** | GRIM | Deep-sea and short-sea RoRo/container services | GNET platform at gnet.grimaldi-eservice.com |
| **Atlantic Container Line (ACL)** | ACLU | Transatlantic container/RoRo (US-Europe) | Separate portal at aclcargo.com |
| **Grimaldi Euromed** | — | Short-sea Mediterranean services | Likely shares GNET infrastructure |
| **Finnlines** | — | RoPax services (Baltic/North Sea) | Separate entity, separate digital platform |
| **Minoan Lines** | — | Ferry services (Greece) | Separate entity, passenger-focused |

> **Note on ACL**: Atlantic Container Line is a wholly-owned subsidiary of Grimaldi Group and operates independently with its own SCAC code (ACLU), its own website (aclcargo.com), and likely its own tracking systems. ACL specializes in transatlantic container and RoRo services between North America and Europe. Whether ACL and Grimaldi Lines share any backend digital infrastructure is unknown. ACL has a separate row in `docs/steamship-lines.md` and should receive its own audit if it is a priority for SSL. This inventory covers **Grimaldi Lines (GRIM)** specifically, with notes on ACL where relevant.

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | **Yes** — the GNET platform hosts a WebAPI help page with documented endpoints and sample responses |
| **Developer portal URL** | [https://www.gnet.grimaldi-eservice.com](https://www.gnet.grimaldi-eservice.com) |
| **API documentation URL(s)** | [https://www.gnet.grimaldi-eservice.com/services/Help](https://www.gnet.grimaldi-eservice.com/services/Help) — lists all endpoints with descriptions, parameters, and example JSON/XML responses |
| **Documentation quality** | **Fair** — ASP.NET WebAPI auto-generated help pages are available with endpoint listings, parameter tables, and sample JSON/XML response payloads. Many endpoints have "No documentation available" for their descriptions, though the parameter names and response structures are self-documenting. No usage guides, tutorials, or integration examples beyond the interactive test pages |
| **OpenAPI/Swagger spec available?** | No — documentation is ASP.NET WebAPI Help Pages format, not OpenAPI/Swagger |
| **Sandbox/test environment?** | **Yes (limited)** — the GNET portal includes interactive test pages under `/services/Test/` for most endpoints (Voyage, SOF, Point-to-Point, Container Info, RoRo Tracking, Shipment Info, Tariff, Atlas Tracking, etc.). These appear to execute against the live system and require a Security Token for most operations |
| **Developer registration** | Unknown — likely requires business relationship with Grimaldi. The Security endpoint accepts UserID + UserSecret, but how to obtain these credentials is not publicly documented |
| **Developer support channels** | Not documented — general contact via Grimaldi commercial department. The GNET portal footer indicates "Grimaldi Corporate Software \| London" |
| **Community/third-party libraries** | None found — no GitHub repos, npm packages, or PyPI packages for GNET API integration |
| **API changelog / release notes** | Not published as a standalone page. Footer shows current revision: "Rev.250228A - 2026" |

### GNET Platform Overview

The **GNET (Grimaldi Network)** platform at `gnet.grimaldi-eservice.com` is Grimaldi's e-services portal, developed by Grimaldi Corporate Software (London). It provides:

- **Web Portal**: Container tracking, RoRo tracking, shipment ETA/ETS, container technical data, VGM submission, voyage intake (VSM), point-to-point schedule enquiry
- **REST API**: A documented WebAPI at `/services/` with 30+ endpoints covering security/auth, shipment info, container tracking, RoRo tracking, sailing schedules, vessel data, VGM, tariff/rates, and documents
- **Mobile App**: "Grimaldi Cargo Mobile" available on [Google Play](https://play.google.com/store/apps/details?id=com.grimaldi.cargo.mobile) and [Apple App Store](https://apps.apple.com/us/app/grimaldi-cargo-mobile/id6463798712)
- **Published Schedules**: Static schedule pages for all major trade routes (W. Africa, South America, North America, Mediterranean, Far East, EuroMed, Adriatic, Euro Aegean)

The platform is built on ASP.NET WebForms with jQuery/Bootstrap frontend, backed by the "ATLAS" ERP system (described as "Bridge to ATLAS" in the portal footer).

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | **No** — Grimaldi is not a DCSA member. The 9 founding members (April 2019) are: MSC, Maersk, CMA CGM, Hapag-Lloyd, ONE, Evergreen, Yang Ming, HMM, and ZIM. PIL became the 10th member in 2024. Grimaldi is not among them |
| **DCSA APIs implemented** | None — the GNET API is a proprietary REST API, not DCSA-compliant |
| **DCSA TNT version** | N/A |
| **DCSA Booking version** | N/A |
| **DCSA Schedules version** | N/A |
| **Known DCSA deviations** | N/A — no DCSA implementation. The GNET API uses proprietary data models (e.g., `TShipmentInfo`, `TVoyageSailingSchedule`, `TTrackingCntr`, `TRoroTracking`) that do not follow DCSA conventions |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Likely Yes (unverified) | As a major international carrier, Grimaldi almost certainly supports standard EDI messages for business partners. No public EDI documentation found |
| **INTTRA integration** | Unknown | Could not confirm from public sources |
| **BIC (Bureau International des Containers)** | Yes (confirmed) | Container IDs in API examples use BIC ISO 6346 format (e.g., `GCNU1234567` — the GCNU prefix is Grimaldi's) |
| **UN/LOCODE** | Yes (confirmed) | The sailing schedule and point-to-point APIs return `PORT_CODE`, `PORT_UNCODE`, `pol`, `pod` fields that use UN/LOCODE format. The SOF endpoint returns `PORT_UNCODE` explicitly |
| **IMO vessel numbers** | Yes (confirmed) | The Vessel API returns `IMO_NO` field; the vessel schedule API returns `VesselIMO`; the point-to-point API returns `pol_vsl_imo` and `pot_vsl_imo` |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | **Bearer Token** — UserID + UserSecret exchanged for a Security Token via API call |
| **Auth documentation** | [GET api/Security](https://www.gnet.grimaldi-eservice.com/services/Help/Api/GET-api-Security) — documented on the GNET API Help page |
| **Registration process** | Not publicly documented. Credentials (UserID + UserSecret) likely require a business relationship with Grimaldi |
| **Registration URL** | Not available — no self-service registration found |
| **Partner program required?** | **Likely Yes — for any API access**. The web portal has a Login function, and most API endpoints require a Security Token |
| **Partner program URL** | N/A — contact Grimaldi commercial department |
| **Credential type** | UserID + UserSecret → Security Token (Bearer) |
| **Token refresh supported?** | Yes — token validity can be checked via `GET api/Security?Token={Token}`. New tokens obtained by re-authenticating |
| **Token lifetime** | Unknown — not documented |
| **Access tiers** | Unknown — no published tier structure |
| **IP whitelisting required?** | Unknown |

### Authentication Flow

```
1. GET api/Security
   Headers: UserID={UserID}, UserSecret={UserSecret}
   → Returns: Security Token (string)

2. Subsequent API calls:
   Headers: Authorization: Bearer {SecurityToken}

3. Token validation (optional):
   GET api/Security?Token={Token}
   → Returns: validity status
```

### Additional Auth Endpoints (Undocumented)

The Security controller exposes additional endpoints that suggest multiple authentication modes:

| Endpoint | Purpose |
|----------|---------|
| `GET api/Security?application={application}&email={email}` | Application-level auth or password reset (undocumented) |
| `GET api/Security?application={application}&userid={userid}&pwd={pwd}` | Application-specific login (undocumented) |
| `GET api/Security?platform={platform}&userid={userid}&pwd={pwd}` | Platform-specific login (undocumented) |
| `GET api/Security?platform={platform}` | Platform info or session check (undocumented) |

### Access Requirements Summary for SSL

To get GNET API access, SSL will likely need to:

1. **Establish a business relationship** with Grimaldi Lines — the API does not appear to offer self-service registration
2. **Contact Grimaldi's commercial or IT department** to request API credentials (UserID + UserSecret)
3. **Receive credentials and authenticate** via the `GET api/Security` endpoint to obtain a Bearer token
4. Use the Bearer token in subsequent API calls

The GNET API help page is publicly accessible (no login required to browse documentation), which suggests Grimaldi intends for potential partners to review the API capabilities before requesting access. The container tracking web portal also provides public access to basic tracking without login.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field must have a row.
> ✅ = Available | ❌ = Not available | ⚠️ = Partial / limited | ❓ = Unknown — could not determine without API credentials
>
> **Note**: Grimaldi uses proprietary field names and data models. DCSA mapping shows the closest DCSA equivalent; actual field values must be mapped during adapter implementation. Many assessments are based on documented response schemas — actual data completeness cannot be verified without live API access.

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ✅ | `GET api/Info?VoyageNo={VoyageNo}`, `GET api/Info?VesselCode=...&DtETSFrom=...&DtETSTo=...&PortCode=...&PortOp=...&Closed=...` | `VOYAGE`, `PORT_CODE`, `NAME`, `ETA`, `ETS`, `VesselName`, `VesselIMO`, `Timezone`, `ETA_UTC`, `ETS_UTC`, `LOAD`, `DISCHARGE`, `TerminalCode`, `TerminalName`, `ServiceCode`, `ServiceName`, `CarrierCode`, `CarrierName` | DCSA CS `vessel-schedules` / `port-schedules` | Two schedule query modes: by voyage number (returns port rotation) and by vessel/date/port filter (returns matching schedule entries). Includes UTC timestamps and timezone info. Vessel schedule response also includes `Closed`, `DryDock`, `DryDockCode` fields |
| 1.2 | Point-to-Point Route Options | ✅ | `GET api/Info?POL={POL}&POD={POD}&nDays={nDays}&nDaysPast={nDaysPast}&ShowTS={ShowTS}` | Full routing: `vessel_name`, `pol_vsl_imo`, `pol_carrier_code`, `pol_serv`, `pol_ets`, `pot` (transshipment port), `pot_eta`, `pot_ets`, `pot_gap`, `pod_eta`, `pod_vyg` | DCSA CS `point-to-point-routes` | Rich response includes POL vessel IMO, carrier details, service info, transshipment port details with gap time, and POD ETA. `ShowTS` param likely controls whether transshipment options are included |
| 1.3 | Booking Lifecycle | ❌ | N/A | N/A | DCSA BKG | No booking API endpoints found. Booking likely handled via EDI, email, or web portal |
| 1.4 | Shipping Instructions | ❌ | N/A | N/A | DCSA eDoc | No shipping instructions API endpoints found |
| 1.5 | Rates | ✅ | `GET api/Atlas?POL={POL}&POD={POD}&FACTofPROD={FACTofPROD}&EQSIZE={EQSIZE}&EQTYPE={EQTYPE}&VALID_ON={VALID_ON}`, `GET api/Atlas?strTariff={strTariff}&strPromo={strPromo}` | `RATE`, `CURRENCYCODE`, `RATEBASISCODE`, `CHARGE_FACTOR`, `CHARGE_AMOUNT`, `TARIFFNUMBER`, `EFFECTIVEDATE`, `TARIFF_TYPE`, `PAYMENT_TYPE_CODE` | Not DCSA | Unusually for a carrier, Grimaldi exposes tariff/rate data via API. Includes promotional tariffs, effective/expiration dates, and per-route/equipment pricing. `CONFIDENTIAL_B` flag suggests some rates may be restricted |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❓ | Unknown | Unknown | `ECP` | Not visible in any documented endpoint response. May be communicated via booking confirmation or portal |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❓ | Unknown | Unknown | `EFC` | Same as above |
| 2.3 | Documentation Cutoff | DCO | ❓ | Unknown | Unknown | `DCO` | Not visible in API responses. The `CLOSED` boolean field in sailing schedule endpoints may indicate whether a voyage is closed for booking/documentation, but this is not a specific cutoff timestamp |
| 2.4 | VGM Cutoff | VCO | ❓ | Unknown | Unknown | `VCO` | VGM submission is available via `GET/POST api/VGM`, but no cutoff timestamp field is documented. The `VALIDATION_MSG` field in VGM response may indicate deadline-related validation |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ❓ | Unknown | Unknown | `FCO` | Not visible in documented API responses. May be communicated via portal or booking confirmation |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❓ | Unknown | Unknown | `LCO` | Grimaldi's RoRo focus means LCL is rarely applicable |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ❓ | Unknown | Unknown | Inferred from first EquipmentEvent | Not explicitly visible in API response schemas |
| 3.2 | Empty Container Gate-Out (Pickup) | ⚠️ | `GET api/Atlas?ContNum={ContNum}&bLastShpmtOnly={bLastShpmtOnly}` | `MOVE_STATUS` (free text), `MOVE_DATETIME`, `TO_LOCATION` in `CONT_TRACKING[]` array | `GTOT` + `EMPTY` | Atlas container tracking returns a full event history per container. The `MOVE_STATUS` field is a string that likely contains event descriptions such as gate-out. Actual event codes unknown without live data |
| 3.3 | Full Container Gate-In | ⚠️ | `GET api/Atlas?ContNum={ContNum}&bLastShpmtOnly=...`, `GET api/Info?ShipmentNo={ShipmentNo}&strCntrNo={strCntrNo}` | `Move` (string), `MoveStatus` (datetime), `ToLocation` | `GTIN` + `LADEN` | The `Info` container tracking endpoint returns `Move` as a string and `MoveStatus` as a datetime — the `Move` field likely contains event type descriptions. The Atlas endpoint provides richer data with `REASON`, `SERVICE`, `VESSEL`, `VOYAGE` per event |
| 3.4 | Container Loaded on Vessel | ⚠️ | `GET api/Atlas?ContNum=...`, `GET api/Info?ShipmentNo=...&strCntrNo=...` | `Move`, `Vessel`, `Voyage`, `Service` | `LOAD` + `LADEN` | Container tracking responses include `Vessel` and `Voyage` fields per event, enabling load-on-vessel detection. The `DOCNO` field in Atlas may reference the B/L |
| 3.5 | Container Discharged at Transshipment | ⚠️ | `GET api/Atlas?ContNum=...` | `MOVE_STATUS`, `TO_LOCATION`, `VOYAGE`, `VESSEL` | `DISC` + `LADEN` + transshipment | Would need to compare `TO_LOCATION` against routing to distinguish transshipment from final destination |
| 3.6 | Container Loaded at Transshipment | ⚠️ | `GET api/Atlas?ContNum=...` | `MOVE_STATUS`, `TO_LOCATION`, `VOYAGE`, `VESSEL` | `LOAD` + `LADEN` + transshipment | Same approach as 3.5 — detect change in `VESSEL`/`VOYAGE` between events |
| 3.7 | Container Discharged at Destination | ⚠️ | `GET api/Atlas?ContNum=...`, `GET api/Info?ShipmentNo=...&strCntrNo=...` | `Move`, `MoveStatus`, `ToLocation` | `DISC` + `LADEN` | Core milestone — the tracking event history should include discharge events |
| 3.8 | Full Container Gate-Out (Delivery) | ⚠️ | `GET api/Atlas?ContNum=...` | `MOVE_STATUS`, `TO_LOCATION` | `GTOT` + `LADEN` | Should appear in the Atlas container tracking event history |
| 3.9 | Empty Container Returned | ⚠️ | `GET api/Atlas?ContNum=...` | `MOVE_STATUS`, `TO_LOCATION`, `REASON` | `GTIN` + `EMPTY` | The Atlas endpoint's `REASON` field may distinguish return events. The `bLastShpmtOnly` parameter suggests multi-shipment history is available |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ✅ | `GET api/Info?ShipmentNo={ShipmentNo}` (→ `Departure`), `GET api/Info?VoyageNo=...` (→ `ETS`), vessel schedule (→ `ETS`, `ETS_UTC`) | `ETS` (Estimated Time of Sailing — Grimaldi's term for ETD), `Departure`, `ETS_UTC` | `DEPA` + classifier | Grimaldi uses **ETS** (Estimated Time of Sailing) instead of ETD. Available from shipment info, voyage schedule, and vessel schedule endpoints. UTC variants available in schedule endpoints |
| 4.2 | Estimated Time of Arrival | ETA | ✅ | `GET api/Info?ShipmentNo={ShipmentNo}` (→ `Arrival`), `GET api/Info?VoyageNo=...` (→ `ETA`), P2P (→ `pod_eta`) | `ETA`, `Arrival`, `ETA_UTC`, `pod_eta`, `EstimatedTimeArrivalPod` | `ARRI` + classifier | Available from shipment info, voyage schedule, P2P routing, and DTS endpoints. UTC variants in schedule endpoints. RoRo tracking includes `ETA_POD` |
| 4.3 | Vessel Arrival at Transshipment | — | ⚠️ | `GET api/Info?POL=...&POD=...` (→ `pot_eta`), `GET api/Info?VoyageNo=...` | `pot_eta`, voyage ETA per port | `ARRI` at intermediate | P2P routing explicitly includes transshipment port (`pot`) with its `pot_eta`. Voyage schedule returns ETA for each port in rotation |
| 4.4 | Vessel Departure from Transshipment | — | ⚠️ | `GET api/Info?POL=...&POD=...` (→ `pot_ets`), `GET api/Info?VoyageNo=...` | `pot_ets`, voyage ETS per port | `DEPA` at intermediate | P2P routing includes `pot_ets` for transshipment departure. The `pot_gap` field in P2P may indicate dwell time at transshipment port |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❌ | No webhook/push endpoints found in the API |
| Event Polling with timestamp filter | ❌ | No timestamp-based event filter parameter documented. Full event history is returned per container/shipment |
| Event Classifier Progression (PLN→EST→ACT) | ❌ | No event classifier concept in the API. ETA/ETS values are single fields, not a progression from planned to estimated to actual |
| Retracted Events | ❌ | No retraction mechanism documented |
| Change Remarks | ❌ | The Atlas tracking `TIR_REMARKS` and `REASON` fields may contain change-related information, but this is not a structured change detection mechanism |
| Delay Reason Codes | ❌ | No standardized delay reason codes documented |

### Coverage Summary

| Category | Fields Available | Fields Unavailable | Fields Unknown | Coverage % |
|----------|-----------------|-------------------|----------------|-----------|
| API Domains (1.x) | 3/5 | 2/5 | 0/5 | 60% |
| Cutoffs (2.x) | 0/6 | 0/6 | 6/6 | 0% (unknown) |
| Container Milestones (3.x) | 0/9 | 0/9 | 9/9 | ~67% (partial — see notes) |
| Transport Events (4.x) | 2/4 | 0/4 | 2/4 | 50–100% |
| Change Detection (5.x) | 0/6 | 6/6 | 0/6 | 0% |
| **Total** | **5/30** | **8/30** | **17/30** | **17% confirmed, est. 40–50% with live testing** |

> **Important notes on coverage assessment**:
>
> - **Container milestones (3.x)**: All 9 are rated ⚠️ (partial) rather than ✅ or ❌ because the Atlas container tracking endpoint (`api/Atlas?ContNum=...`) returns a full event history array with `MOVE_STATUS`, `MOVE_DATETIME`, `TO_LOCATION`, `VESSEL`, `VOYAGE` per event. This *should* contain most container milestones, but the `MOVE_STATUS` field values (the actual event codes/descriptions) cannot be verified without live API access. The data structure strongly suggests milestones like load, discharge, gate-in, and gate-out are present.
>
> - **Cutoffs (2.x)**: Rated ❓ because no cutoff-specific fields appear in documented endpoint responses. However, the `CLOSED` boolean in sailing schedule responses may relate to cargo cutoffs, and cutoff data may be returned in booking-related flows not visible in public documentation.
>
> - **Transport events (4.x)**: ETA and ETS (ETD) are clearly available from multiple endpoints. Transshipment port ETA/ETS are available in the P2P routing response but rated ⚠️ because they represent scheduled times, not actual arrival/departure events with PLN→EST→ACT progression.

---

## Endpoint Reference

### Security / Authentication

| Endpoint | Method | Description | Key Params | Auth Required | Response Format | Response Model |
|----------|--------|-------------|-----------|--------------|----------------|---------------|
| `api/Security` | GET | Get Security Token | `UserID`, `UserSecret` (in request header) | No (this IS the auth endpoint) | JSON, XML | String (token) |
| `api/Security?Token={Token}` | GET | Validate Security Token | `Token` | No | JSON, XML | String |
| `api/Security?application={app}&email={email}` | GET | Application auth / reset (undocumented) | `application`, `email` | Unknown | JSON, XML | Unknown |
| `api/Security?application={app}&userid={uid}&pwd={pwd}` | GET | Application login (undocumented) | `application`, `userid`, `pwd` | Unknown | JSON, XML | Unknown |
| `api/Security?platform={platform}&userid={uid}&pwd={pwd}` | GET | Platform login (undocumented) | `platform`, `userid`, `pwd` | Unknown | JSON, XML | Unknown |
| `api/Security?platform={platform}` | GET | Platform info (undocumented) | `platform` | Unknown | JSON, XML | Unknown |

### Shipment Information & Container Tracking

| Endpoint | Method | Description | Key Params | Auth Required | Response Model | Sample Response Fields |
|----------|--------|-------------|-----------|--------------|---------------|----------------------|
| `api/Info?ShipmentNo={ShipmentNo}` | GET | Shipment info (POL/POD/ETS/ETA) | `ShipmentNo` (e.g., "S3-1234567") — **Required** | Yes (Bearer) | `TShipmentInfo` | `Number`, `Departure`, `Arrival` |
| `api/Info?CntrNo={CntrNo}` | GET | Container technical data (ATLAS) | `CntrNo` (e.g., "GCNU1234567") — **Required** | Yes (Bearer) | `TCntrInfo` | `EQUIPMENT_NUMBER`, `EQUIP_SIZE_TYPE`, `TAREWEIGHT_KG`, `PAYLOADWEIGHT_KG`, `EXTERNAL_LxWxH`, `INTERNAL_LxWxH` |
| `api/Info?ShipmentNo={ShipmentNo}&strCntrNo={strCntrNo}` | GET | Container tracking (Atlas) | `ShipmentNo`, `strCntrNo` | Yes (Bearer) | `TTrackingCntr[]` | `EQUIPMENT_NUMBER`, `EQUIP_SIZE_TYPE`, `Shipment`, `Move`, `MoveStatus` (datetime), `ToLocation`, `Service`, `Vessel`, `Voyage` |
| `api/Atlas?ContNum={ContNum}&bLastShpmtOnly={bLastShpmtOnly}` | GET | Container tracking with full event history | `ContNum`, `bLastShpmtOnly` (boolean) | Yes (Bearer) | Nested: `CONT_NUM`, `CONT_TYPE`, `CONT_TRACKING[]` | Per tracking event: `REASON`, `USER_COMPANY`, `MOVE_DATETIME`, `MOVE_STATUS`, `VOYAGE`, `SERVICE`, `VESSEL`, `TO_LOCATION`, `DOCNO`, `TIR_REMARKS` |
| `api/Atlas?strShipment={strShipment}` | GET | Shipment tracking with cargo detail | `strShipment` | Yes (Bearer) | Nested shipment + cargo + tracking | `strShipmentNumber`, `strVyg`, `strPOL`, `ETS`, `strPOD`, `ETA`, `strRouting`, `CargoData[].strCargoID`, `CargoData[].Tracking[].strTrackingInfo`, `.strTrackingLocation`, `.strTrackingTransport`, `.dtTimestamp` |

### RoRo Tracking

| Endpoint | Method | Description | Key Params | Auth Required | Response Model | Sample Response Fields |
|----------|--------|-------------|-----------|--------------|---------------|----------------------|
| `api/Info?ShipmentNo={ShipmentNo}&VehicleID={VehicleID}` | GET | RoRo tracking from Grimaldi ERP | `ShipmentNo`, `VehicleID` — **Required** | Yes (Bearer) | `TTrackingInfo[]` | `location_name`, `move_desc`, `move_date_time` |
| `api/Info?ShipmentNo={ShipmentNo}&VIN={VIN}` | GET | RoRo tracking events (e.g., OnQuay, Loaded) | `ShipmentNo`, `VIN` — **Required** | Yes (Bearer) | `TRoroTracking[]` | `VOYAGE`, `POL`, `POD`, `BLNUM`, `RORO_TYPE`, `RORO_MAKE`, `RORO_MODEL`, `RORO_VIN`, `RORO_CHASSIS`, `RORO_WEIGHT`, `RORO_LxWxH`, `TRACKING_EVENT`, `TRACKING_DATETIME`, `CUSTOMER`, `SHIPPER`, `CONSIGNEE`, `ETA_POD` |
| `api/Atlas?ShipmentNo={ShipmentNo}&VehicleID={VehicleID}` | GET | RoRo tracking from ATLAS ERP | `ShipmentNo`, `VehicleID` — **Required** | Yes (Bearer) | `TTrackingInfo[]` | `location_name`, `move_desc`, `move_date_time` |
| `api/DTS?VIN={VIN}` | GET | Vehicle tracking by VIN | `VIN` | Yes (Bearer) | `TDTSTracking[]` | `Vessel`, `Voyage`, `VesselCode`, `POLIDOrigin`, `POLOrigin`, `PODIDFinal`, `PODFinal`, `POL`, `POLID`, `POD`, `PODID`, `Make`, `Model`, `VIN`, `Length`, `Width`, `Height`, `ShipperName`, `ShippingNumber`, `IsLoadedOnVessel`, `IsDischargedFromVessel`, `LoadedOnVessel` (datetime), `DischargedFromVessel` (datetime), `EstimatedTimeArrivalPod`, `EstimatedTimeSailingPol` |
| `api/DTS?ShipmentNumber={ShipmentNumber}` | GET | Vehicle tracking by shipment | `ShipmentNumber` | Yes (Bearer) | `TDTSTracking[]` | Same as above |
| `api/DTS?ChassisNo={ChassisNo}` | GET | Vehicle tracking by chassis number | `ChassisNo` | Yes (Bearer) | `TDTSTracking[]` | Same as above |
| `POST api/Atlas` | POST | Register multiple vehicle tracking events | Request body (structure undocumented) | Yes (Bearer) | Unknown | Used for event registration, likely terminal/operations use |

### Sailing Schedules

| Endpoint | Method | Description | Key Params | Auth Required | Response Model | Sample Response Fields |
|----------|--------|-------------|-----------|--------------|---------------|----------------------|
| `api/Info?VoyageNo={VoyageNo}` | GET | Sailing schedule by voyage | `VoyageNo` (e.g., "GHA0321") — **Required** | Yes (Bearer) | `TVoyageSailingSchedule[]` | `VOYAGE`, `PORT_CODE`, `NAME`, `ETA`, `ETS`, `CLOSED`, `SchedulePK`, `VoyagePrefix`, `VesselName`, `LOAD`, `DISCHARGE`, `Timezone`, `ETA_UTC`, `ETS_UTC` |
| `api/Info?VesselCode={VC}&DtETSFrom={From}&DtETSTo={To}&PortCode={PC}&PortOp={PO}&Closed={C}` | GET | Sailing schedule by vessel/date/port filter | `VesselCode`, `DtETSFrom`, `DtETSTo`, `PortCode`, `PortOp`, `Closed` | Yes (Bearer) | Schedule entries with `SchedulePK`, `VoyageCode`, `VesselCode`, `VesselName`, `VesselIMO`, `ETA`, `ETS`, `PortCode`, `PortName`, `DigiformName`, `TerminalCode`, `TerminalName`, `Load`, `Discharge`, `ETA_UTC`, `ETS_UTC`, `ServiceCode`, `ServiceName`, `CarrierGroup`, `CarrierCode`, `CarrierName`, `Closed`, `DryDock`, `DryDockCode`, `DryDockName` | Rich schedule data including terminal details, carrier info, and service codes |
| `api/Info?POL={POL}&POD={POD}&nDays={nDays}&nDaysPast={nDaysPast}&ShowTS={ShowTS}` | GET | Point-to-point schedule enquiry | `POL`, `POD`, `nDays`, `nDaysPast`, `ShowTS` | Yes (Bearer) | P2P routing entries | `pk`, `vessel_name`, `pol_vsl_imo`, `pol_carrier_code`, `pol_carrier_name`, `pol_carrier_group`, `pol_serv`, `pol_serv_name`, `pol`, `pol_call_id`, `pol_vyg`, `pol_ets`, `pot_vessel_name`, `pot_vsl_imo`, `pot_carrier_code`, `pot_carrier_name`, `pot`, `pot_eta`, `pot_gap`, `pot_vyg`, `pot_ets`, `pod`, `pod_vyg`, `pod_eta` |
| `api/Info?VoyageForSOF={VoyageForSOF}` | GET | Statement of Facts (SOF) by voyage | `VoyageForSOF` — **Required** | Yes (Bearer) | `TSOF[]` | Extremely detailed: `VESSEL_NAME`, `VOYAGE`, `SERVICE_NAME`, `CARRIER_NAME`, `PORT_NAME`, `PORT_UNCODE`, `TERMINAL_NAME`, `CALL_ID`, `CLOSED`, `ETA`, `ETS`, `DIST_PREVIOUS_CALL`, `STOPPAGES`, wind/swell data, pilot times, lock times, berthing times, ops times, draft readings, bunker ROB, and more (60+ fields per call) |
| `POST api/EVoyage?EVoyage={EVoyage}&EVoyage_TS={EVoyage_TS}` | POST | EVoyage schedule update | `EVoyage`, `EVoyage_TS` | Yes (Bearer) | Unknown | For schedule update operations — likely an operational/admin endpoint |

### Vessel Reference Data

| Endpoint | Method | Description | Key Params | Auth Required | Response Model |
|----------|--------|-------------|-----------|--------------|---------------|
| `api/Vessel?UnRestricted={UnRestricted}` | GET | Vessel list | `UnRestricted` (boolean) | Yes (Bearer) | `TVessel[]`: `Code`, `Name`, `IMO_NO` |
| `api/Info?codeType={codeType}&UnRestricted={UnRestricted}` | GET | Reference code lookup (undocumented) | `codeType`, `UnRestricted` | Yes (Bearer) | Unknown — likely returns lookup tables for port codes, equipment types, etc. |

### VGM (Verified Gross Mass)

| Endpoint | Method | Description | Key Params | Auth Required | Response Model |
|----------|--------|-------------|-----------|--------------|---------------|
| `GET api/VGM?ShpmtNum={ShpmtNum}&ContNum={ContNum}&VygNum={VygNum}` | GET | Retrieve VGM data | `ShpmtNum`, `ContNum`, `VygNum` | Yes (Bearer) | `TVGM[]`: `SHIPMENT_NO`, `EQUIP_NO`, `EQUIP_TYPE`, `TARE_WEIGHT`, `VGM_WEIGHT`, `UOM`, `METHOD`, `VGM_DATE`, `RESP_PARTY_SIGN`, `RESP_PARTY_NAME`, `SEAL1`–`SEAL4`, `ERROR_B`, `VALIDATION_MSG`, `UPDATE_ALLOWED_B` |
| `POST api/VGM` | POST | Submit VGM data | Request body (VGM submission) | Yes (Bearer) | Same structure as GET |

### Tariff / Rates

| Endpoint | Method | Description | Key Params | Auth Required | Response Model |
|----------|--------|-------------|-----------|--------------|---------------|
| `api/Atlas?POL={POL}&POD={POD}&FACTofPROD={FP}&EQSIZE={ES}&EQTYPE={ET}&VALID_ON={VO}` | GET | Tariff rate enquiry | `POL`, `POD`, `FACTofPROD`, `EQSIZE`, `EQTYPE`, `VALID_ON` | Yes (Bearer) | `RATE`, `CURRENCYCODE`, `RATEBASISCODE`, `CHARGE_FACTOR`, `CHARGE_AMOUNT`, `TARIFFNUMBER`, `EFFECTIVEDATE`, `TARIFF_TYPE`, `CONFIDENTIAL_B`, `PAYMENT_TYPE_CODE` |
| `api/Atlas?strTariff={strTariff}&strPromo={strPromo}` | GET | Tariff promo lookup | `strTariff`, `strPromo` | Yes (Bearer) | `tariff_number`, `tariff_desc`, `promo_code`, `effective_date`, `expiration_date`, `pol`, `pol_uncode`, `pod`, `pod_uncode`, `equip_type`, `equip_size` |

### Documents & Verification

| Endpoint | Method | Description | Key Params | Auth Required |
|----------|--------|-------------|-----------|--------------|
| `GET api/Document?DocumentID={DocumentID}` | GET | Retrieve document | `DocumentID` | Yes (Bearer) |
| `POST api/Document?DocumentIDforUpdate={DocumentIDforUpdate}` | POST | Update document | `DocumentIDforUpdate` | Yes (Bearer) |
| `GET api/AtlasVerification?ShipmentNo={SN}&WAFreleasePIN={PIN}` | GET | WAF release PIN verification | `ShipmentNo`, `WAFreleasePIN` | Yes (Bearer) |
| `GET api/AtlasVerification?strTestMsg={strTestMsg}` | GET | Test/ping endpoint | `strTestMsg` | Unknown |

### Mobile App Support

| Endpoint | Method | Description | Key Params | Auth Required |
|----------|--------|-------------|-----------|--------------|
| `api/Info?store={store}&appname={appname}` | GET | App version check | `store`, `appname` | Unknown |

Response: `LATEST_VERS` — used by the Grimaldi Cargo Mobile app to check for updates.

### Lookup Methods Summary

| Identifier Type | Supported? | Which Endpoints? | Notes |
|----------------|-----------|-----------------|-------|
| **Shipment Number** | ✅ | `api/Info?ShipmentNo=...`, `api/Info?ShipmentNo=...&strCntrNo=...`, `api/Info?ShipmentNo=...&VehicleID=...`, `api/Info?ShipmentNo=...&VIN=...`, `api/Atlas?strShipment=...`, `api/DTS?ShipmentNumber=...` | **Primary identifier** — Grimaldi shipment numbers follow format "S3-1234567". Used across all tracking endpoints |
| **Container Number** | ✅ | `api/Info?CntrNo=...` (technical data), `api/Info?ShipmentNo=...&strCntrNo=...` (tracking), `api/Atlas?ContNum=...&bLastShpmtOnly=...` (full history) | Requires container number in BIC ISO 6346 format (e.g., "GCNU1234567") |
| **Bill of Lading (B/L) number** | ⚠️ | Not a direct lookup parameter, but `BLNUM` appears in RoRo tracking response (`api/Info?ShipmentNo=...&VIN=...`) and `DOCNO` in Atlas container tracking | B/L number is returned in responses but not used as a primary lookup key |
| **VIN (Vehicle Identification Number)** | ✅ | `api/DTS?VIN=...`, `api/Info?ShipmentNo=...&VIN=...` | RoRo-specific. Rich tracking data with vehicle make/model/dimensions |
| **Chassis Number** | ✅ | `api/DTS?ChassisNo=...` | RoRo-specific |
| **Vehicle ID** | ✅ | `api/Info?ShipmentNo=...&VehicleID=...`, `api/Atlas?ShipmentNo=...&VehicleID=...` | Grimaldi internal vehicle identifier (distinct from VIN) |
| **Voyage Number** | ✅ | `api/Info?VoyageNo=...`, `api/Info?VoyageForSOF=...` | For schedule lookups. Format: "GHA0321" |
| **Vessel Code** | ✅ | `api/Info?VesselCode=...&DtETSFrom=...&DtETSTo=...` | Used in vessel schedule queries combined with date range |
| **POL / POD** | ✅ | `api/Info?POL=...&POD=...&nDays=...` | For point-to-point schedule enquiry |

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

> No rate limit documentation was found. Rate limits would need to be determined empirically after obtaining API credentials, or by asking Grimaldi directly.

---

<!-- Webhook / Push Support section: carrier does not support webhooks -->

## Webhook / Push Support

| Detail | Value |
|--------|-------|
| **Webhooks supported?** | **No** — no webhook or event subscription endpoints found in the API |
| **Alternative** | Polling-based approach required. Use the tracking endpoints periodically and diff results against stored state |

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Container Tracking URL** | [https://www.gnet.grimaldi-eservice.com/GNET/Pages_GAtlas/WFContainerTracking](https://www.gnet.grimaldi-eservice.com/GNET/Pages_GAtlas/WFContainerTracking) |
| **Login required for basic tracking?** | **No** — the container tracking page is publicly accessible. Supports lookup by Equipment # (container number) or Shipment # |
| **RoRo Tracking URL** | `https://www.gnet.grimaldi-eservice.com/GNET/Pages_RoroTracking/WFRoroTracking` |
| **Shipment ETA/ETS URL** | `https://www.gnet.grimaldi-eservice.com/GNET/INFO/ShipmentInfo` |
| **Container Technical Data URL** | `https://www.gnet.grimaldi-eservice.com/GNET/Pages_Cntr/WFCntrTechData` |
| **VGM Submission URL** | `https://www.gnet.grimaldi-eservice.com/GNET/Pages_VGM/ATLAS_VGM` |
| **Point-to-Point Schedule URL** | `https://www.gnet.grimaldi-eservice.com/GNET/Pages_ScheduleInfo/WFSchedule` |
| **Data available on portal but NOT in API** | Published sailing schedules (static HTML/PDF pages) for specific trade routes, fleet position data, notice board, Tilbury Delivery Note service, WAF Proforma Invoice |
| **Scraping feasibility** | Moderate — portal uses ASP.NET WebForms with ViewState, which complicates scraping. However, the REST API provides the same data programmatically, making scraping unnecessary for most use cases |
| **Portal technology** | ASP.NET WebForms, jQuery 3.6.4, Bootstrap, AJAX |

### Additional Web Portals

| Portal | URL | Purpose |
|--------|-----|---------|
| **cargo.grimaldi-lines.com** | [https://cargo.grimaldi-lines.com](https://cargo.grimaldi-lines.com) | Short-sea RoRo/ferry cargo services — driver cards, schedules, freight rates. Focuses on European short-sea services |
| **booking.grimaldi-lines.com** | [https://booking.grimaldi-lines.com](https://booking.grimaldi-lines.com) | Online booking portal for Grimaldi services |
| **grimaldi.napoli.it/container/** | [https://www.grimaldi.napoli.it/container/](https://www.grimaldi.napoli.it/container/) | Grimaldi Group Container Department — container types, specifications, links to GNET tracking and equipment location |
| **container.grimaldi-app.com** | [https://container.grimaldi-app.com](https://container.grimaldi-app.com) | Container department reports (linked from grimaldi.napoli.it) |

### ACL (Atlantic Container Line) Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | [https://www.aclcargo.com](https://www.aclcargo.com) — ACL has its own cargo tracking portal |
| **Login required?** | Likely Yes for detailed tracking |
| **Relationship to Grimaldi** | ACL is a wholly-owned Grimaldi Group subsidiary but operates independently with SCAC code ACLU |
| **Separate audit needed?** | Yes — if SSL ships via ACL, a dedicated audit of ACL's digital capabilities is recommended |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Likely Yes (unverified) — EDI is standard for carriers of Grimaldi's scale |
| **Expected EDI message types** | IFTMIN (booking), COPARN (container release), BAPLIE (bay plan), IFTSTA (shipment status), COPINO (container pre-notification) |
| **EDI connection method** | Unknown — likely AS2 or SFTP |
| **EDI documentation** | Not publicly available — would require contacting Grimaldi's IT/commercial department |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Confidence | Notes |
|-----------|-------------------|------------|-------|
| **project44** | ❓ Unknown | Low | project44 claims broad ocean coverage but Grimaldi as a niche carrier may not be included |
| **FourKites** | ❓ Unknown | Low | Primarily trucking-focused |
| **Vizion** | Likely Yes | Medium | Claims 99% ocean freight coverage. Pricing: ~$5/container, 15 free for testing |
| **INTTRA / E2open** | Likely Yes | Medium | Largest ocean shipping B2B platform with 70+ carrier connections |
| **CargoSmart** | ❓ Unknown | Low | Focuses on major container carriers |
| **Terminal49** | ❓ Unknown | Medium | Claims 98% global coverage. Free tier (100 containers) available for testing |
| **Shipsgo** | Likely Yes | Medium | Supports 160+ carriers with broad coverage |

> **Aggregator note**: Given that Grimaldi now has a **direct REST API**, aggregator integration is less critical than initially assessed. The direct API is the recommended primary integration path. Aggregators remain useful as a fallback or for comparison/validation purposes.

### Mobile Application

| Detail | Value |
|--------|-------|
| **App name** | Grimaldi Cargo Mobile |
| **iOS** | [App Store](https://apps.apple.com/us/app/grimaldi-cargo-mobile/id6463798712) |
| **Android** | [Google Play](https://play.google.com/store/apps/details?id=com.grimaldi.cargo.mobile) |
| **Capabilities** | Sailing schedule consultation and tracking on mobile devices |
| **Relevance** | The mobile app likely consumes the same GNET API, confirming the API is actively maintained and used in production |

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown — cannot assess without live API access. The ATLAS ERP system appears to be the source of truth for tracking data | Unknown |
| **API uptime/reliability** | Unknown — no published SLA. The GNET platform footer shows "Rev.250228A - 2026" indicating recent updates | Unknown |
| **Historical data depth** | The `bLastShpmtOnly` parameter on Atlas container tracking suggests multi-shipment history is available. Depth unknown | API documentation |
| **Timezone handling** | **Both local and UTC** — sailing schedule endpoints return `ETA`, `ETS` (local) AND `ETA_UTC`, `ETS_UTC` (UTC) plus a `Timezone` field. This is good design | API documentation (confirmed) |
| **Character encoding** | UTF-8 (standard ASP.NET WebAPI) | API documentation |
| **Response format** | JSON and XML both supported for all endpoints | API documentation (confirmed) |

### Known Issues & Gotchas

- **Proprietary data model** — Grimaldi does not use DCSA event codes. The `Move`, `MOVE_STATUS`, `TRACKING_EVENT`, `move_desc` fields are free-text strings whose values are unknown without live data. Adapter development will require obtaining sample data to build the mapping table.
- **ETS not ETD** — Grimaldi uses "ETS" (Estimated Time of Sailing) where the industry standard is "ETD" (Estimated Time of Departure). This is a cosmetic difference but must be handled in field mapping.
- **Multiple tracking endpoints** — Container tracking is split across `api/Info?ShipmentNo=...&strCntrNo=...` (simpler response) and `api/Atlas?ContNum=...&bLastShpmtOnly=...` (richer response with full event history). The adapter should prefer the Atlas endpoint for completeness.
- **RoRo vs. container tracking** — Different endpoints and response models for RoRo (vehicles/rolling cargo) vs. containerized freight. The adapter may need to detect cargo type and use the appropriate endpoint.
- **Transshipment port in P2P** — The point-to-point schedule response uses the prefix `pot_` for "Port of Transshipment" — not a standard abbreviation. Fields: `pot`, `pot_eta`, `pot_ets`, `pot_gap`, `pot_vyg`.
- **Shipment number format** — Grimaldi shipment numbers follow the pattern "S3-1234567" (alphanumeric prefix + hyphen + digits). Input validation should account for this format.
- **`CLOSED` field semantics** — The `CLOSED` boolean in schedule responses may indicate cargo cutoff (voyage closed for new bookings) or that the vessel has departed. Semantics need verification.
- **SOF endpoint verbosity** — The `VoyageForSOF` endpoint returns 60+ fields per port call including weather data, pilot times, draft readings, bunker ROB, etc. Most of this data is irrelevant for tracking but may be useful for operational analysis.
- **Language/localization** — Port names and descriptions may use Italian naming conventions in some responses.

### Recently Deprecated or Changed

- API revision `Rev.250228A - 2026` is the latest as of research date, indicating active maintenance.
- No publicly documented deprecations.

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | **Yes** — a direct Grimaldi adapter is feasible. The GNET API provides shipment info (POL/POD/ETS/ETA), container tracking (event history with move status, vessel, voyage, location), sailing schedules (vessel, port, and P2P), and vessel reference data |
| **Implementation effort** | **High** — fully proprietary API, no DCSA compliance. Every field requires manual mapping. The biggest risk is the unknown `MOVE_STATUS` / `move_desc` / `TRACKING_EVENT` event code values — these need to be mapped from Grimaldi's proprietary codes to DCSA equivalents. Recommend obtaining sample API responses early |
| **DCSA base adapter usable?** | **No** — fully custom adapter required. Grimaldi's API uses entirely proprietary data models (`TShipmentInfo`, `TTrackingCntr`, `TVoyageSailingSchedule`, `TRoroTracking`, `TDTSTracking`) that bear no resemblance to DCSA event structures |

### Recommended Approach

**Direct API integration via GNET WebAPI.**

The adapter should target the following priority endpoints:

1. **`api/Info?ShipmentNo={ShipmentNo}`** — primary shipment lookup for ETS/ETA
2. **`api/Atlas?ContNum={ContNum}&bLastShpmtOnly=false`** — rich container event history with full tracking chain
3. **`api/Info?ShipmentNo={ShipmentNo}&strCntrNo={strCntrNo}`** — alternative container tracking with simpler response
4. **`api/Info?VoyageNo={VoyageNo}`** — voyage schedule with port rotation and ETA/ETS per port
5. **`api/Info?POL={POL}&POD={POD}&nDays={nDays}&nDaysPast={nDaysPast}&ShowTS=true`** — point-to-point routing with transshipment options

**Architecture:**

```
SDK CarrierAdapter (Grimaldi / GRIM)
    │
    ├── Auth: GET api/Security (UserID+UserSecret → Bearer Token)
    │   └── Token caching + validity check via api/Security?Token=...
    │
    ├── Tracking
    │   ├── Container: api/Atlas?ContNum=... (primary — rich event history)
    │   ├── Container: api/Info?ShipmentNo=...&strCntrNo=... (fallback — simpler)
    │   ├── Shipment: api/Info?ShipmentNo=... (ETD/ETA summary)
    │   └── RoRo: api/DTS?VIN=... / api/Info?ShipmentNo=...&VIN=... (if RoRo)
    │
    ├── Schedules
    │   ├── Voyage: api/Info?VoyageNo=...
    │   ├── Vessel/Port: api/Info?VesselCode=...&DtETSFrom=...&DtETSTo=...
    │   └── Point-to-Point: api/Info?POL=...&POD=...
    │
    └── Reference Data
        └── Vessels: api/Vessel?UnRestricted=true
```

**Key mapping challenge:** The proprietary `MOVE_STATUS`, `Move`, `move_desc`, and `TRACKING_EVENT` fields need to be reverse-engineered from live data to build an event code mapping table. Recommend requesting sample API responses from Grimaldi covering a complete shipment lifecycle (empty pickup → load → discharge → delivery → empty return).

### Recommended Lookup Method

**Shipment Number** is the primary identifier for the GNET API. Most endpoints accept `ShipmentNo` as the primary key (format: "S3-1234567"). For container-level tracking with full history, `ContNum` (container number) via the Atlas endpoint provides the richest data.

For SSL's use case, the recommended lookup flow is:
1. Look up shipment by `ShipmentNo` → get ETS/ETA summary
2. Look up container events by `ContNum` via Atlas → get full milestone history
3. Use shipment + container combo for consolidated view

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Every 4–6 hours (conservative, pending rate limit discovery). Increase to every 2 hours for shipments nearing key milestones (loading, arrival) |
| **Incremental filter** | **Not available** — no timestamp-based filter on tracking endpoints. Each poll returns the full event history. Adapter must diff locally against stored events |
| **Batch tracking** | **Not supported** — one API call per shipment/container. No bulk tracking endpoint found |

### Auth Implementation Notes

```
1. Store UserID + UserSecret securely (env vars or secret manager)
2. On first request: GET api/Security with UserID/UserSecret in headers → cache token
3. Before each API call: optionally validate token via GET api/Security?Token={token}
4. On 401/403 response: re-authenticate and retry
5. Token lifetime is unknown — implement proactive refresh (e.g., every 30 min or on failure)
```

Both JSON and XML response formats are supported. Recommend using JSON (`Accept: application/json` header).

### Edge Cases to Handle

- **RoRo cargo detection**: Grimaldi ships significant RoRo cargo. If a shipment contains rolling cargo (vehicles, heavy equipment), the container tracking endpoints may return no data — the adapter should fall back to DTS/RoRo tracking endpoints.
- **Mixed ConRo vessels**: Grimaldi operates ConRo vessels carrying both containers and RoRo cargo on the same voyage. A single voyage lookup returns port calls for all cargo types.
- **ACL vs. Grimaldi routing**: A booking may use both Grimaldi and ACL vessels on different legs. The point-to-point response includes `pol_carrier_code`, `pot_carrier_code` to identify which carrier operates each leg.
- **`bLastShpmtOnly` parameter**: The Atlas container tracking endpoint's boolean parameter controls whether only the most recent shipment's events are returned or the full history. Set to `false` for complete lifecycle visibility; `true` for current shipment only.
- **Transshipment detection**: No explicit transshipment flag. Must be inferred by comparing `TO_LOCATION` changes and vessel/voyage changes between consecutive tracking events.
- **West Africa port infrastructure**: Some Grimaldi destination ports in West Africa may have limited terminal digitalization, potentially leading to delayed or missing terminal events.
- **Tariff confidentiality**: The `CONFIDENTIAL_B` flag in tariff responses indicates that some rate data may be restricted. The adapter should respect this flag.

### Mapping Complexity

**High complexity** for the tracking adapter. The core challenge is mapping Grimaldi's proprietary event descriptions (`MOVE_STATUS`, `Move`, `move_desc`, `TRACKING_EVENT` fields — all free-text strings) to the canonical data model's event types (DCSA-style `LOAD`, `DISC`, `GTIN`, `GTOT` codes).

**Medium complexity** for schedules. The schedule response fields map reasonably well to the canonical model: `ETS` → ETD, `ETA` → ETA, `PORT_CODE` → port, `VesselName`/`VesselIMO` → vessel. The P2P response is particularly rich, with IMO numbers, carrier codes, and transshipment details.

**Low complexity** for shipment info. The `TShipmentInfo` response has only 3 fields (`Number`, `Departure`, `Arrival`) that map directly to the canonical shipment summary.

---

## Open Questions

- [ ] **Q1: How to obtain GNET API credentials?** — The API documentation is public, but the process for obtaining UserID + UserSecret is not documented. SSL should contact Grimaldi's commercial or IT department to request API access.
- [ ] **Q2: What are the actual `MOVE_STATUS` / `Move` / `TRACKING_EVENT` values?** — These free-text event fields are critical for milestone mapping. Sample API responses from a complete shipment lifecycle are needed to build the mapping table.
- [ ] **Q3: Is there a rate limit?** — No rate limiting documentation exists. This should be discussed during credential onboarding or discovered empirically.
- [ ] **Q4: Does SSL currently ship with Grimaldi Lines?** — Need to confirm actual volume. Is it Grimaldi Lines (GRIM), ACL (ACLU), or both?
- [ ] **Q5: What cargo types does SSL ship via Grimaldi?** — Containers, RoRo vehicles, or both? This determines which tracking endpoints to prioritize.
- [ ] **Q6: Token lifetime?** — The Security Token's expiration time is not documented. Needs empirical testing after obtaining credentials.
- [ ] **Q7: Are cutoff timestamps available anywhere?** — The documented API responses don't include specific cutoff times (DCO, VCO, FCO). These may be available in booking-related flows or additional undocumented endpoints accessible after authentication.
- [ ] **Q8: What does `CLOSED` mean in schedule responses?** — Could indicate cargo cutoff (voyage closed for booking), vessel departure, or operational completion. Semantics need verification.
- [ ] **Q9: Does the `PortOp` parameter in vessel schedule queries accept UN/LOCODE?** — Or does it use Grimaldi-internal port codes?
- [ ] **Q10: ACL audit needed?** — If SSL uses ACL (transatlantic), ACL should receive its own separate audit. ACL may or may not share the GNET API infrastructure.

---

## Source Links

| Resource | URL | Status |
|----------|-----|--------|
| GNET Platform (main portal) | [https://www.gnet.grimaldi-eservice.com](https://www.gnet.grimaldi-eservice.com) | ✅ Active (HTTP 200) |
| GNET WebAPI Help (API documentation) | [https://www.gnet.grimaldi-eservice.com/services/Help](https://www.gnet.grimaldi-eservice.com/services/Help) | ✅ Active (HTTP 200) |
| GNET Container Tracking (public) | [https://www.gnet.grimaldi-eservice.com/GNET/Pages_GAtlas/WFContainerTracking](https://www.gnet.grimaldi-eservice.com/GNET/Pages_GAtlas/WFContainerTracking) | ✅ Active — no login required |
| Grimaldi Lines Website (English) | [https://www.grimaldi-lines.com/en/](https://www.grimaldi-lines.com/en/) | ✅ Active — primarily passenger ferry site |
| Grimaldi Group Corporate | [https://www.grimaldi.napoli.it](https://www.grimaldi.napoli.it) | ✅ Active |
| Grimaldi Container Department | [https://www.grimaldi.napoli.it/container/](https://www.grimaldi.napoli.it/container/) | ✅ Active |
| Cargo Portal (short-sea) | [https://cargo.grimaldi-lines.com](https://cargo.grimaldi-lines.com) | ✅ Active (HTTP 200) |
| Booking Portal | [https://booking.grimaldi-lines.com](https://booking.grimaldi-lines.com) | ✅ Active (HTTP 200) |
| ACL Cargo Website | [https://www.aclcargo.com](https://www.aclcargo.com) | ✅ Active |
| DCSA Member List | [https://dcsa.org/about-us/](https://dcsa.org/about-us/) | Grimaldi NOT listed as member |
| Grimaldi Cargo Mobile (Android) | [Google Play](https://play.google.com/store/apps/details?id=com.grimaldi.cargo.mobile) | ✅ Active |
| Grimaldi Cargo Mobile (iOS) | [App Store](https://apps.apple.com/us/app/grimaldi-cargo-mobile/id6463798712) | ✅ Active |

---

## Appendix: GNET API Response Model Reference

The GNET API uses ASP.NET WebAPI with .NET data contract serialization. All models are in the `GNetAPI.Models` namespace. Below are the confirmed response model types from the API Help pages:

| Model Type | Endpoint(s) | Key Fields |
|-----------|------------|-----------|
| `TShipmentInfo` (GNetShipment) | `api/Info?ShipmentNo=...` | `Number`, `Departure`, `Arrival` |
| `TVoyageSailingSchedule` | `api/Info?VoyageNo=...` | `VOYAGE`, `PORT_CODE`, `NAME`, `ETA`, `ETS`, `CLOSED`, `VesselName`, `Timezone`, `ETA_UTC`, `ETS_UTC`, `LOAD`, `DISCHARGE` |
| `TTrackingCntr` | `api/Info?ShipmentNo=...&strCntrNo=...` | `EQUIPMENT_NUMBER`, `EQUIP_SIZE_TYPE`, `Shipment`, `Move`, `MoveStatus` (datetime), `ToLocation`, `Service`, `Vessel`, `Voyage` |
| `TTrackingInfo` | `api/Info?ShipmentNo=...&VehicleID=...`, `api/Atlas?ShipmentNo=...&VehicleID=...` | `location_name`, `move_desc`, `move_date_time` |
| `TRoroTracking` | `api/Info?ShipmentNo=...&VIN=...` | `VOYAGE`, `POL`, `POD`, `BLNUM`, `RORO_TYPE`, `RORO_MAKE`, `RORO_MODEL`, `RORO_VIN`, `RORO_CHASSIS`, `TRACKING_EVENT`, `TRACKING_DATETIME`, `CUSTOMER`, `SHIPPER`, `CONSIGNEE`, `ETA_POD` |
| `TDTSTracking` | `api/DTS?VIN=...` / `api/DTS?ShipmentNumber=...` / `api/DTS?ChassisNo=...` | `Vessel`, `Voyage`, `VesselCode`, `POL`, `POD`, `Make`, `Model`, `VIN`, `IsLoadedOnVessel`, `IsDischargedFromVessel`, `LoadedOnVessel` (datetime), `DischargedFromVessel` (datetime), `EstimatedTimeArrivalPod`, `EstimatedTimeSailingPol` |
| `TVessel` | `api/Vessel?UnRestricted=...` | `Code`, `Name`, `IMO_NO` |
| `TVGM` | `api/VGM?ShpmtNum=...&ContNum=...&VygNum=...` | `SHIPMENT_NO`, `EQUIP_NO`, `EQUIP_TYPE`, `TARE_WEIGHT`, `VGM_WEIGHT`, `UOM`, `METHOD`, `VGM_DATE`, `SEAL1`–`SEAL4` |
| `TSOF` | `api/Info?VoyageForSOF=...` | 60+ fields per port call (vessel operations data) |
| Vessel schedule (filtered) | `api/Info?VesselCode=...&DtETSFrom=...` | `VoyageCode`, `VesselCode`, `VesselName`, `VesselIMO`, `ETA`, `ETS`, `PortCode`, `PortName`, `TerminalCode`, `TerminalName`, `ServiceCode`, `ServiceName`, `CarrierCode`, `CarrierName`, `ETA_UTC`, `ETS_UTC` |
| P2P routing | `api/Info?POL=...&POD=...` | `vessel_name`, `pol_vsl_imo`, `pol_carrier_code`, `pol_ets`, `pot`, `pot_eta`, `pot_gap`, `pot_ets`, `pod`, `pod_eta` |
| Atlas container tracking | `api/Atlas?ContNum=...` | `CONT_NUM`, `CONT_TYPE`, nested `CONT_TRACKING[]`: `REASON`, `MOVE_DATETIME`, `MOVE_STATUS`, `VOYAGE`, `SERVICE`, `VESSEL`, `TO_LOCATION`, `DOCNO`, `TIR_REMARKS` |
| Atlas shipment tracking | `api/Atlas?strShipment=...` | `strShipmentNumber`, `strVyg`, `strPOL`, `ETS`, `strPOD`, `ETA`, `strRouting`, nested `CargoData[]` with `Tracking[]` |
| Tariff rate | `api/Atlas?POL=...&POD=...&EQSIZE=...` | `RATE`, `CURRENCYCODE`, `CHARGE_AMOUNT`, `TARIFFNUMBER`, `EFFECTIVEDATE`, `TARIFF_TYPE`, `CONFIDENTIAL_B` |
| Tariff promo | `api/Atlas?strTariff=...&strPromo=...` | `tariff_number`, `tariff_desc`, `promo_code`, `effective_date`, `expiration_date`, `pol_uncode`, `pod_uncode` |

## Appendix: Grimaldi Group Fleet & Services Overview

Understanding Grimaldi's business helps contextualize their digital infrastructure.

### Fleet Composition
- ~130 vessels (one of the largest privately-owned fleets)
- Primarily RoRo and ConRo (container + RoRo) vessels
- Also operates pure car/truck carriers (PCTC)
- Some pure container vessels

### Key Trade Routes
| Route | Service Type | Notes |
|-------|-------------|-------|
| Mediterranean short-sea | RoRo, container | High frequency, numerous ports |
| Mediterranean – West Africa | RoRo, container | Key market for Grimaldi |
| Mediterranean – South America (East Coast) | RoRo, container | Brazil, Argentina, Uruguay |
| Mediterranean – North America | RoRo, container | Often via ACL for transatlantic |
| Northern Europe – West Africa | RoRo, container | Via Mediterranean hub |
| Northern Europe – South America | RoRo, container | |
| Mediterranean – Far East | Container (deep-sea) | |
| EuroMed, Adriatic, Euro Aegean, Euro-Shuttle | Short-sea RoRo | European short-sea services |
