# Required Data Fields for Carrier API Integrations

These are the fields SSL needs to fetch programmatically from carrier APIs for shipment tracking and operational visibility. Fields are organized by category with canonical names chosen for clarity across carrier APIs.

> **Reference implementation: Maersk**
> Maersk follows the [DCSA (Digital Container Shipping Association)](https://dcsa.org) open standards. The Maersk API mappings below are sourced from the DCSA OpenAPI specs (TNT v3, Booking v2, Commercial Schedules v1) which Maersk implements at `developer.maersk.com`. Other DCSA-adopting carriers (CMA CGM, MSC, Hapag-Lloyd, ONE, etc.) use the same field names. For carriers that don't implement DCSA, these canonical names still serve as the "what to look for" when searching their proprietary APIs.

---

## 1. API Domains

These represent the top-level API capabilities SSL needs from each carrier. Each carrier may expose these through different endpoints.

| # | Canonical Field Name | Description | Maersk / DCSA API Equivalent | Change Detection |
|---|---|---|---|---|
| 1.1 | **Vessel & Port Schedules** | Sailing schedules: vessel rotations, port calls, ETAs/ETDs for planned services | DCSA Commercial Schedules API (`GET /v1/vessel-schedules`, `GET /v1/port-schedules`). Maersk: Schedules API at `api.maersk.com/schedules` | Yes — schedule changes affect all downstream planning |
| 1.2 | **Point-to-Point Route Options** | End-to-end routing options for a shipment including all transport legs, transit times, and transshipment points | DCSA Commercial Schedules API (`GET /v1/point-to-point-routes`). Returns `PointToPoint` objects with `legs[]`, `transitTime`, `cutOffTimes[]` | No — queried on demand during booking |
| 1.3 | **Booking Lifecycle** | Create, confirm, amend, and cancel bookings; retrieve booking status and details | DCSA Booking API v2 (`GET/POST /v2/bookings`). Confirmed booking returns `transportPlan[]`, `shipmentCutOffTimes[]`, `carrierClauses[]`. Maersk: Booking API | Yes — booking status changes (confirmed → amended → cancelled) |
| 1.4 | **Shipping Instructions** | Submit and manage shipping instructions (the data needed to issue a Bill of Lading) | DCSA eDocumentation API. Tracked via ShipmentEvent with `documentTypeCode=SHI` and `shipmentEventTypeCode` (RECE → DRFT → PENA → CONF → ISSU etc.) | Yes — SI status progression and rejections |
| 1.5 | **Rates** | Carrier freight rates / spot quotes | **Not part of DCSA standard** — proprietary per carrier. Maersk: Spot Rate API at `developer.maersk.com`. Most carriers don't expose rate APIs (rates typically sent as PDFs/spreadsheets) | Yes — rate expiration and updates |

---

## 2. Document & Cargo Cutoffs

Deadline timestamps provided by the carrier, usually in the booking confirmation or schedule response. Missing a cutoff means the container may be rolled to the next sailing.

| # | Canonical Field Name | Abbreviation | Description | Maersk / DCSA API Equivalent | Change Detection |
|---|---|---|---|---|---|
| 2.1 | **Earliest Container Release Date** | ERD | The earliest date/time a shipper can pick up an empty container from the depot to stuff it. Marks the start of the container availability window for export shipments | DCSA cutoff code `ECP` (Empty Container Pick-up date). Found in `shipmentCutOffTimes[]` on confirmed booking, or `cutOffTimes[]` in Commercial Schedules point-to-point response | Yes — if pushed later, compresses shipper's stuffing window |
| 2.2 | **Earliest Full-Container Delivery Date** | EFC | The earliest date/time a loaded (full) container can be delivered to the terminal. The terminal won't accept containers before this date | DCSA cutoff code `EFC` (Earliest Full-Container delivery date). Found in same locations as ERD | Yes — if pushed later, compresses delivery window |
| 2.3 | **Documentation Cutoff** | DCO | Deadline for submitting all required shipping documentation (shipping instructions, commercial invoice, packing list, etc.) | DCSA cutoff code `DCO` (Documentation Cut-Off). Field: `cutOffDateTimeCode: "DCO"` with `cutOffDateTime` in `shipmentCutOffTimes[]` | **Yes — critical** — missed DCO can result in cargo being rolled |
| 2.4 | **VGM Cutoff** | VCO | Deadline for submitting the Verified Gross Mass declaration (SOLAS requirement — mandatory for all export containers) | DCSA cutoff code `VCO` (VGM Cut-Off). Field: `cutOffDateTimeCode: "VCO"` | **Yes — critical** — SOLAS regulatory requirement |
| 2.5 | **Container/Cargo Cutoff (FCL)** | FCO | Deadline for physically delivering a full container load to the terminal/port. Also called "port cutoff" or "terminal receiving deadline" | DCSA cutoff code `FCO` (FCL Delivery Cut-Off). Some carriers also use `PCO` (Port Cut-Off) for the same concept | **Yes — critical** — most common cause of containers being rolled |
| 2.6 | **Container/Cargo Cutoff (LCL)** | LCO | Deadline for delivering less-than-container-load cargo to a Container Freight Station. Only applicable when receipt type at origin is CFS | DCSA cutoff code `LCO` (LCL Delivery Cut-Off). Conditional: only present when `receiptTypeAtOrigin = "CFS"` | Yes — same criticality as FCO for LCL shipments |

> **Additional cutoff codes available in DCSA** (may be relevant for specific shipment types):
> - `RCO` — Reefer cutoff (refrigerated containers)
> - `DGC` — Dangerous goods cutoff
> - `OBC` — Out-of-gauge / breakbulk cutoff
> - `TCO` — Transshipment cutoff
> - `AFC` — Advanced manifest filing cutoff
> - `CUA` — Customs acceptance cutoff

---

## 3. Container Milestones (Equipment Events)

Physical container movement events tracked via the DCSA Track & Trace API. In Maersk's implementation, these are `EQUIPMENT` type events retrieved from:
- **Poll**: `GET /v3/events?eventTypes=EQUIPMENT&documentTypeCodes=BKG&documentReference={bookingRef}`
- **Push**: Subscribe via `POST /v3/event-subscriptions` with `equipmentEventTypeCodes` filter

Each milestone is an `EquipmentEvent` with a specific `equipmentEventTypeCode` + `emptyIndicatorCode` combination.

| # | Canonical Field Name | Description | Maersk / DCSA Event Signature | Change Detection |
|---|---|---|---|---|
| 3.1 | **Container Assigned to Booking** | Whether a physical container has been assigned to and associated with the booking. Indicates physical movement has started or is imminent | Inferred: presence of any `EquipmentEvent` with `relatedDocumentReferences[].type=BKG` matching the booking reference. First event (typically `PICK` or `GTOT`) confirms attachment | Yes — confirms booking is progressing to physical execution |
| 3.2 | **Empty Container Gate-Out (Pickup)** | Empty container released from depot/terminal — shipper or trucker has picked it up for stuffing | `equipmentEventTypeCode: GTOT` + `emptyIndicatorCode: EMPTY`. May also appear as `PICK` (Pick-up) at some carriers. Location: depot (`facilityTypeCode: DEPO`) or terminal (`POTE`) | Yes — confirms container is in shipper's possession |
| 3.3 | **Full Container Gate-In** | Loaded (stuffed) container delivered to the origin terminal for export | `equipmentEventTypeCode: GTIN` + `emptyIndicatorCode: LADEN`. Location: port terminal (`facilityTypeCode: POTE`) | Yes — confirms cargo received at terminal |
| 3.4 | **Container Loaded on Vessel** | Container physically loaded onto the vessel at port of loading | `equipmentEventTypeCode: LOAD` + `emptyIndicatorCode: LADEN` + `isTransshipmentMove: false`. Location: port terminal, with `transportCall.vessel` identifying the ship | **Yes — critical** — confirms on-board; triggers Bill of Lading issuance |
| 3.5 | **Container Discharged at Transshipment Port** | Container unloaded from vessel at an intermediate transshipment port (not final destination) | `equipmentEventTypeCode: DISC` + `emptyIndicatorCode: LADEN` + `isTransshipmentMove: true`. The `transportCall.location.UNLocationCode` gives the transshipment port | Yes — monitors transshipment progress |
| 3.6 | **Container Loaded at Transshipment Port** | Container loaded onto a connecting vessel at the transshipment port | `equipmentEventTypeCode: LOAD` + `emptyIndicatorCode: LADEN` + `isTransshipmentMove: true`. The new vessel appears in `transportCall.vessel` | Yes — confirms transshipment completed successfully |
| 3.7 | **Container Discharged at Destination** | Container unloaded from vessel at the final destination port | `equipmentEventTypeCode: DISC` + `emptyIndicatorCode: LADEN` + `isTransshipmentMove: false` at destination port. Also derivable from TransportEvent `ARRI` at final port | **Yes — critical** — triggers arrival notification to consignee |
| 3.8 | **Full Container Gate-Out (Delivery)** | Loaded container released from destination terminal — consignee or trucker has picked it up | `equipmentEventTypeCode: GTOT` + `emptyIndicatorCode: LADEN`. May appear as `AVPU` (Available for Pick-up) first, then `PICK` on actual collection. Location: destination terminal | Yes — confirms cargo delivered out of port |
| 3.9 | **Empty Container Returned** | Empty container returned to a depot after consignee has unloaded it. Completes the container lifecycle | `equipmentEventTypeCode: GTIN` + `emptyIndicatorCode: EMPTY`. Location: depot (`facilityTypeCode: DEPO`) or terminal | Yes — triggers end of demurrage/detention tracking |

---

## 4. Vessel Schedule / Transport Events

Vessel movement events tracked via the DCSA Track & Trace API as `TRANSPORT` type events. These provide ETD/ETA at each port on the route.

| # | Canonical Field Name | Abbreviation | Description | Maersk / DCSA Event Signature | Change Detection |
|---|---|---|---|---|---|
| 4.1 | **Estimated Time of Departure** | ETD | Estimated date/time the vessel will depart from a port. Progresses from Planned → Estimated → Actual | TransportEvent: `transportEventTypeCode: DEPA` + `eventClassifierCode: EST`. Planned: `PLN`. Actual: `ACT`. The `transportCall.location` identifies the port, `transportCall.vessel` the ship | **Yes — critical** — ETD changes cascade to all downstream ETAs |
| 4.2 | **Estimated Time of Arrival** | ETA | Estimated date/time the vessel will arrive at a port. Progresses from Planned → Estimated → Actual | TransportEvent: `transportEventTypeCode: ARRI` + `eventClassifierCode: EST`. Planned: `PLN`. Actual: `ACT`. Same location/vessel context as ETD | **Yes — critical** — ETA changes at destination are the most common notification trigger |
| 4.3 | **Vessel Arrival at Transshipment Port** | — | Actual or estimated arrival of the vessel at a transshipment (intermediate) port | TransportEvent: `transportEventTypeCode: ARRI` at intermediate port on the transport plan. Distinguish from destination arrival by comparing against `transportPlan` leg sequence | Yes — delays here cascade to connecting vessel |
| 4.4 | **Vessel Departure from Transshipment Port** | — | Actual or estimated departure from the transshipment port on the connecting vessel | TransportEvent: `transportEventTypeCode: DEPA` on the next leg's vessel after transshipment | Yes — confirms onward journey has resumed |

> **Note on "Container arrived at destination ETD"** from the original field list: This appears to be a labeling error. The relevant fields are:
> - Container **arriving** at destination → **ETA** (row 4.2 above)
> - Container **discharged** at destination → milestone 3.7 above
> The "ETD" abbreviation applies to departure, not arrival. If the intent was to track when the container physically arrived at destination, use milestone 3.7 (Container Discharged at Destination).

---

## 5. Change Detection & Notification Strategy

The original requirement noted: *"Any change to any of the dates — this would then trigger SSL needing to notify downstream client(s)."*

### Carrier-Side Mechanisms

| Mechanism | Maersk / DCSA Support | Description |
|---|---|---|
| **Event Subscriptions (Push/Webhook)** | DCSA TNT v3: `POST /v3/event-subscriptions` with `callbackUrl`. Filters by event type, booking ref, equipment ref, vessel, etc. **Optional for carriers to implement** — Maersk supports it | Carrier pushes events to SSL's endpoint as they occur. Most efficient for real-time notifications |
| **Event Polling** | DCSA TNT v3: `GET /v3/events` with `eventCreatedDateTime` filter. **Mandatory for carriers to implement** | SSL periodically polls for new events since last check. Universal fallback — all DCSA carriers must support this |
| **Event Classifier Progression** | Events progress: `PLN` → `EST` → `ACT`. A new event with a different `eventClassifierCode` or `eventDateTime` for the same milestone indicates a change | Compare `eventDateTime` between successive events for the same milestone to detect schedule changes |
| **Retracted Events** | `metadata.retractedEventID` field points to a previously-sent event that is now void | Indicates a prior event/estimate was wrong and is being replaced |
| **Change Remarks** | `changeRemark` field on TransportEvents (free text, max 250 chars) | Carrier-provided explanation of why a change occurred |
| **Delay Reason Codes** | `delayReasonCode` on TransportEvents (DCSA-standardized codes) | Machine-readable reason for delays |

### Recommended SSL-Side Approach

Since not all carriers support push, and even DCSA-compliant carriers may have varying push reliability:

1. **Maintain a local event store** — record the latest `eventDateTime` + `eventClassifierCode` for each milestone per shipment
2. **Poll on a schedule** — for each active shipment, poll carrier events APIs (e.g., every 1–4 hours)
3. **Diff against stored state** — when a new event arrives for a milestone that already has a stored value, compare timestamps
4. **Trigger notifications** — if the `eventDateTime` has changed by more than a configurable threshold (e.g., > 1 hour), or if `eventClassifierCode` has progressed, fire a notification to downstream clients
5. **Supplement with push where available** — subscribe to carrier webhooks for real-time updates, but don't depend on them exclusively

### Fields Most Likely to Trigger Notifications

| Priority | Field(s) | Why |
|---|---|---|
| 🔴 Critical | ETD change, ETA change at destination | Directly affects consignee's planning, warehouse scheduling, customs filing |
| 🔴 Critical | FCO / DCO / VCO cutoff changes | Shippers must adjust cargo delivery or documentation timelines |
| 🟡 High | Container loaded on vessel (actual) | Confirms shipment is underway; Bill of Lading can be issued |
| 🟡 High | Container discharged at destination (actual) | Triggers customs clearance and delivery coordination |
| 🟡 High | Transshipment delays | Missed connection at transshipment port can add days/weeks |
| 🟢 Medium | ERD / EFC changes | Affects shipper's stuffing and delivery scheduling |
| 🟢 Medium | Empty container returned | Ends demurrage/detention clock |
| ⚪ Low | Empty gate-out, full gate-in | Useful for tracking but rarely triggers client notifications |

---

## Appendix: DCSA Event Code Quick Reference

For agents researching other carrier APIs — these are the DCSA codes to look for or map to:

### Equipment Event Type Codes
| Code | Meaning | SSL Relevance |
|---|---|---|
| `LOAD` | Loaded onto vessel | ✅ Core milestone |
| `DISC` | Discharged from vessel | ✅ Core milestone |
| `GTIN` | Gated in (container enters facility) | ✅ Core milestone |
| `GTOT` | Gated out (container leaves facility) | ✅ Core milestone |
| `PICK` | Picked up | ✅ Alternative to GTOT at some carriers |
| `DROP` | Dropped off | ✅ Alternative to GTIN at some carriers |
| `AVPU` | Available for pick-up | Useful — precedes actual pickup |
| `AVDO` | Available for drop-off | Useful — precedes actual drop-off |
| `STUF` | Stuffed (cargo loaded into container) | Informational |
| `STRP` | Stripped (cargo unloaded from container) | Informational |
| `CUSS` | Customs selected for scan | Informational |
| `CUSI` | Customs selected for inspection | ⚠️ May cause delays |
| `CUSR` | Customs released | Useful — customs clearance confirmed |
| `RSEA` | Resealed | Informational |

### Transport Event Type Codes
| Code | Meaning |
|---|---|
| `ARRI` | Arrived at port |
| `DEPA` | Departed from port |

### Event Classifier Codes
| Code | Meaning |
|---|---|
| `PLN` | Planned (initial schedule) |
| `EST` | Estimated (updated projection) |
| `ACT` | Actual (confirmed happened) |

### Shipment Event Type Codes (Document Lifecycle)
| Code | Meaning | SSL Relevance |
|---|---|---|
| `RECE` | Received | Booking/SI received by carrier |
| `CONF` | Confirmed | Booking confirmed — cutoffs available |
| `REJE` | Rejected | ⚠️ Requires action |
| `ISSU` | Issued | B/L or transport document issued |
| `DRFT` | Drafted | Document in draft state |
| `APPR` | Approved | Document approved |
| `CANC` | Cancelled | Booking or document cancelled |
| `PENA` | Pending approval | Awaiting carrier approval |
| `PENU` | Pending update | Carrier requesting updates |
| `RELS` | Released | Document/cargo released |

### Cutoff Time Codes
| Code | Full Name | Description |
|---|---|---|
| `ECP` | Empty Container Pick-up | Earliest date to pick up empty (= ERD) |
| `EFC` | Earliest Full-Container delivery | Earliest date to deliver full container |
| `DCO` | Documentation Cut-Off | Deadline for shipping docs |
| `VCO` | VGM Cut-Off | Deadline for Verified Gross Mass |
| `FCO` | FCL Delivery Cut-Off | Deadline for full container delivery to terminal |
| `LCO` | LCL Delivery Cut-Off | Deadline for LCL cargo to CFS |
| `PCO` | Port Cut-Off | General port receiving deadline |
| `RCO` | Reefer Cut-Off | Deadline for reefer containers |
| `DGC` | Dangerous Goods Cut-Off | Deadline for DG cargo |
| `AFC` | Advanced Filing Cut-Off | Deadline for advance manifest filing |

---

## Appendix: Maersk API Endpoints Summary

| API | Endpoint Base | DCSA Standard | Auth Required |
|---|---|---|---|
| Track & Trace (Events) | `api.maersk.com/synergy/tracking/v2` | DCSA TNT v2/v3 | Yes (OAuth2) |
| Booking | `api.maersk.com/booking` | DCSA Booking v2 | Yes |
| Schedules | `api.maersk.com/schedules` | DCSA Commercial Schedules v1 | Yes |
| Spot Rates | `api.maersk.com/rates` | Proprietary (not DCSA) | Yes |

All Maersk APIs require registration at [developer.maersk.com](https://developer.maersk.com) to obtain credentials.
