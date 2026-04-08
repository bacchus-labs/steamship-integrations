# Alianca Navegacao e Logistica -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing. No API exists; research focused on web portal capabilities, aggregator availability, and Maersk subsidiary relationship.
> **Researched by**: Agent (carrier-api-inventory workflow)
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | Alianca Navegacao e Logistica Ltda (commonly "Alianca") |
| **SCAC Code** | ANRM |
| **Parent Company** | A.P. Moller-Maersk A/S (via Hamburg Sud acquisition, closed December 2017) |
| **Alliance** | None (domestic cabotage operator; parent Maersk participates in Gemini Cooperation) |
| **Primary Services** | Container cabotage (Brazilian domestic coastal shipping), multimodal logistics (rail, trucking, warehousing) |
| **Market Position** | Leading Brazilian cabotage operator; pioneer in container cabotage between Brazilian ports. Fleet of 9 container vessels (~33,660 TEU capacity) |
| **Headquarters** | Brazil |
| **Website** | https://www.alianca.com.br |

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | No |
| **Developer portal URL** | N/A |
| **API documentation URL(s)** | N/A |
| **Documentation quality** | None -- no API documentation exists |
| **OpenAPI/Swagger spec available?** | No |
| **Sandbox/test environment?** | No |
| **Developer registration** | N/A |
| **Developer support channels** | Customer contact form at https://www.alianca.com.br/contato-en |
| **Community/third-party libraries** | None found |
| **API changelog / release notes** | N/A |

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | No -- Alianca is not independently a DCSA member. Parent company Maersk is a founding DCSA member, but DCSA standards are not exposed for Alianca's cabotage operations |
| **DCSA APIs implemented** | None |
| **DCSA TNT version** | N/A |
| **DCSA Booking version** | N/A |
| **DCSA Schedules version** | N/A |
| **Known DCSA deviations** | N/A |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Yes (via INTTRA/E2open) | Alianca is listed in the INTTRA ocean carrier network; specific message types unpublished |
| **INTTRA integration** | Yes | Confirmed on INTTRA carrier network page (https://www.inttra.com/ocean-carrier-network/) |
| **BIC (Bureau International des Containers)** | Yes | Container prefix ANRM is registered |
| **UN/LOCODE** | Unknown | Likely used for Brazilian port codes but not confirmed in public documentation |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | N/A -- no API exists |
| **Auth documentation** | N/A |
| **Registration process** | N/A |
| **Registration URL** | N/A |
| **Partner program required?** | N/A |
| **Partner program URL** | N/A |
| **Credential type** | N/A |
| **Token refresh supported?** | N/A |
| **Token lifetime** | N/A |
| **Access tiers** | N/A |
| **IP whitelisting required?** | N/A |

### Access Requirements Summary for SSL

Alianca has no public API. All digital interaction requires a customer relationship and login credentials for Portal Cabotagem (https://www.portalcabotagem.com.br/). To track Alianca shipments programmatically, SSL would need to either (a) use a third-party aggregator like project44 that supports Alianca (SCAC: ANRM), (b) establish EDI connectivity via INTTRA/E2open, or (c) negotiate a direct data-sharing agreement with Alianca/Maersk. The Maersk developer portal (developer.maersk.com) does not appear to cover Alianca cabotage shipments.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field must have a row.
> Assessments below reflect direct carrier API availability. Aggregator availability (e.g., project44) is noted separately.

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ❌ | N/A | N/A | N/A | Vessel schedules visible on Portal Cabotagem and alianca.com.br but no API. Daily Position updates available via portal |
| 1.2 | Point-to-Point Route Options | ❌ | N/A | N/A | N/A | Portal Cotacao Online provides quotations but no programmatic access |
| 1.3 | Booking Lifecycle | ❌ | N/A | N/A | N/A | Booking managed via Portal Cabotagem (login required). EDI booking may be possible via INTTRA |
| 1.4 | Shipping Instructions | ❌ | N/A | N/A | N/A | Document management via Portal Cabotagem only |
| 1.5 | Rates | ❌ | N/A | N/A | N/A | Portal Cotacao Online provides online quotations but no API |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❌ | N/A | N/A | `ECP` | No API; may be communicated via portal or EDI |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❌ | N/A | N/A | `EFC` | No API; may be communicated via portal or EDI |
| 2.3 | Documentation Cutoff | DCO | ❌ | N/A | N/A | `DCO` | No API; may be communicated via portal or EDI |
| 2.4 | VGM Cutoff | VCO | ❌ | N/A | N/A | `VCO` | VGM submission supported via portal (individual or CSV batch); cutoff timing unknown |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ❌ | N/A | N/A | `FCO` | No API |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❌ | N/A | N/A | `LCO` | No API |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ❌ | N/A | N/A | Inferred from first EquipmentEvent | No API |
| 3.2 | Empty Container Gate-Out (Pickup) | ❌ | N/A | N/A | `GTOT` + `EMPTY` | Tracking on Portal Cabotagem / MonitorAli only |
| 3.3 | Full Container Gate-In | ❌ | N/A | N/A | `GTIN` + `LADEN` | Tracking on Portal Cabotagem / MonitorAli only |
| 3.4 | Container Loaded on Vessel | ❌ | N/A | N/A | `LOAD` + `LADEN` | Tracking on Portal Cabotagem / MonitorAli only |
| 3.5 | Container Discharged at Transshipment | ❌ | N/A | N/A | `DISC` + `LADEN` + transshipment | Cabotage routes are typically direct; transshipment uncommon |
| 3.6 | Container Loaded at Transshipment | ❌ | N/A | N/A | `LOAD` + `LADEN` + transshipment | Cabotage routes are typically direct; transshipment uncommon |
| 3.7 | Container Discharged at Destination | ❌ | N/A | N/A | `DISC` + `LADEN` | Tracking on Portal Cabotagem / MonitorAli only |
| 3.8 | Full Container Gate-Out (Delivery) | ❌ | N/A | N/A | `GTOT` + `LADEN` | Tracking on Portal Cabotagem / MonitorAli only |
| 3.9 | Empty Container Returned | ❌ | N/A | N/A | `GTIN` + `EMPTY` | No API |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ❌ | N/A | N/A | `DEPA` + classifier | Vessel schedules on portal; no API |
| 4.2 | Estimated Time of Arrival | ETA | ❌ | N/A | N/A | `ARRI` + classifier | Vessel schedules on portal; no API |
| 4.3 | Vessel Arrival at Transshipment | -- | ❌ | N/A | N/A | `ARRI` at intermediate | Cabotage routes typically direct; transshipment uncommon |
| 4.4 | Vessel Departure from Transshipment | -- | ❌ | N/A | N/A | `DEPA` at intermediate | Cabotage routes typically direct; transshipment uncommon |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❌ | No API |
| Event Polling with timestamp filter | ❌ | No API |
| Event Classifier Progression (PLN->EST->ACT) | ❌ | No API |
| Retracted Events | ❌ | No API |
| Change Remarks | ❌ | No API |
| Delay Reason Codes | ❌ | No API |

### Coverage Summary

| Category | Fields Available | Fields Unavailable | Fields Unknown | Coverage % |
|----------|-----------------|-------------------|----------------|-----------|
| API Domains (1.x) | 0/5 | 5/5 | 0/5 | 0% |
| Cutoffs (2.x) | 0/6 | 6/6 | 0/6 | 0% |
| Container Milestones (3.x) | 0/9 | 9/9 | 0/9 | 0% |
| Transport Events (4.x) | 0/4 | 4/4 | 0/4 | 0% |
| Change Detection (5.x) | 0/6 | 6/6 | 0/6 | 0% |
| **Total** | **0/30** | **30/30** | **0/30** | **0%** |

---

## Endpoint Reference

Alianca has no public API. This section is intentionally omitted.

---

## Rate Limits & Quotas

N/A -- no API exists.

---

## Webhook / Push Support

N/A -- no webhook or push support exists.

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | https://www.portalcabotagem.com.br/ |
| **Login required?** | Yes |
| **Data available on portal but NOT in API** | All data is portal-only: booking management, real-time satellite tracking (MonitorAli), vessel schedules, document download, billing/invoicing, VGM submission, pick-up scheduling |
| **Scraping feasibility** | Not assessed -- login required, ToS not reviewed. Portal appears to be a modern web application |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Yes (via INTTRA/E2open) |
| **EDI message types** | Unpublished -- Alianca is listed in the INTTRA carrier network but specific message types are not publicly documented |
| **EDI connection method** | Via INTTRA/E2open platform |
| **EDI documentation** | Contact Alianca or INTTRA for details |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Yes | Dedicated tracking page at https://www.project44.com/tracking/container/alianca/ -- supports container tracking by MBL/BL number or container number |
| **FourKites** | Unknown | No specific confirmation found |
| **Vizion** | No | Alianca/ANRM is NOT listed in Vizion's supported carriers (https://docs.vizionapi.com/docs/supported-carriers). Hamburg Sud (SUDU) IS supported |
| **INTTRA / E2open** | Yes | Alianca is listed in the INTTRA ocean carrier network |
| **CargoSmart** | Unknown | No specific confirmation found |
| **Other**: SeaRates | Yes | Tracking page at https://www.searates.com/sealine/alianca |
| **Other**: Shipsgo | Yes | Tracking via ANRM prefix at https://shipsgo.com/ocean/container-prefixes/anrm/container-tracking |

> **Aggregator note**: Since Alianca has no direct API, aggregators represent the only programmatic access path. project44 is the most established aggregator with confirmed Alianca support. Their data likely comes from web scraping of Portal Cabotagem or a direct data partnership with Alianca/Maersk. The data freshness and field coverage available through project44 for Alianca is unknown and should be verified.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown -- Portal Cabotagem offers "real-time" satellite tracking (MonitorAli) but no API to measure against | Unknown |
| **API uptime/reliability** | N/A -- no API | N/A |
| **Historical data depth** | Unknown | Unknown |
| **Timezone handling** | Unknown -- likely Brasilia Time (BRT, UTC-3) for domestic cabotage | Estimated (unverified) |
| **Character encoding** | Unknown -- portal content is in Portuguese and English | Unknown |

### Known Issues & Gotchas

- Alianca operates Brazilian cabotage only -- all routes are domestic between Brazilian ports. This is fundamentally different from international deep-sea shipping.
- Despite being a Maersk subsidiary, Alianca's digital infrastructure is completely separate from Maersk's developer portal and API ecosystem.
- The Hamburg Sud brand has been retired and migrated to Maersk systems, but Alianca has NOT been similarly migrated, due to Brazilian cabotage regulations requiring Brazilian-flagged vessels and local operations.
- VGM submission is available via Portal Cabotagem (individual entry or CSV batch upload), suggesting some degree of structured data interchange capability.
- Portal Cabotagem and alianca.com.br are bilingual (Portuguese/English).

### Recently Deprecated or Changed

- No known deprecations. Alianca recently launched "Portal Cotacao Online" for online freight quotations, indicating continued investment in their independent digital infrastructure.

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | Partial -- only through third-party aggregators (project44 recommended) or portal scraping |
| **Implementation effort** | Very High (no API) -- requires either aggregator integration or custom scraping solution |
| **DCSA base adapter usable?** | No -- fully custom; Alianca does not implement DCSA standards |

### Recommended Approach

Alianca has no public API, so a direct carrier adapter is not feasible. The recommended approach for SSL is to integrate via **project44** (confirmed Alianca support) or establish **EDI connectivity via INTTRA/E2open**. project44 would provide the simplest integration path since SSL may already use project44 for other carriers, and it avoids the complexity of EDI setup.

If aggregator access is insufficient or too costly, a **portal scraping approach** could be explored against Portal Cabotagem, but this would require customer credentials, careful ToS review, and ongoing maintenance as the portal evolves. This is not recommended as a primary strategy.

A third option is to escalate through Maersk's partnership team to determine if Maersk's API can be extended to cover Alianca cabotage shipments, though this appears unlikely given the separate digital infrastructure.

### Recommended Lookup Method

Container number is the most widely supported identifier across aggregators (project44, SeaRates, Shipsgo). Bill of Lading number is also supported by project44.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Dependent on aggregator -- project44 typically supports polling intervals of 1-4 hours for ocean shipments |
| **Incremental filter** | Dependent on aggregator capabilities |
| **Batch tracking** | Dependent on aggregator -- project44 supports batch container tracking |

### Auth Implementation Notes

No direct auth required with Alianca. Authentication would be with the chosen aggregator (project44 API key, INTTRA EDI credentials, etc.).

### Edge Cases to Handle

- Brazilian cabotage routes are short (domestic port-to-port), so the shipment lifecycle is compressed compared to international routes
- Transshipment events are rare/nonexistent for cabotage -- routes are typically direct
- Container number prefixes may use ANRM (Alianca) or Maersk-group prefixes (MAEU, MSKU) depending on equipment pool

### Mapping Complexity

If using project44, the mapping complexity depends on project44's data format for Alianca. The main challenge is that Alianca's event model (visible on Portal Cabotagem) is proprietary and undocumented publicly. project44 likely normalizes this to their own format, adding a layer of abstraction. Mapping from project44's normalized format to SSL's canonical model should be straightforward since project44 follows industry conventions.

---

## Open Questions

- [ ] Does SSL have an existing business relationship with Alianca?
- [ ] Does SSL already use project44? If so, is Alianca/ANRM included in their project44 subscription?
- [ ] What is the data freshness and field coverage that project44 provides for Alianca shipments specifically?
- [ ] Can Maersk's partnership team extend API access to cover Alianca cabotage operations?
- [ ] What specific EDI message types does Alianca support via INTTRA?
- [ ] Is portal scraping of Portal Cabotagem permitted under Alianca's terms of service?
- [ ] Does Alianca plan to develop a public API or migrate to Maersk's digital platform in the future?

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website | https://www.alianca.com.br |
| Carrier Website (English) | https://www.alianca.com.br/home-en |
| E-Commerce/Digital Services | https://www.alianca.com.br/e-commerce-en |
| Portal Cabotagem | https://www.portalcabotagem.com.br/ |
| About Alianca | https://www.alianca.com.br/the-alianca |
| Hamburg Sud Migration (Maersk) | https://www.maersk.com/hamburgsud |
| Maersk Brand Unification | https://www.maersk.com/news/articles/2023/06/19/unifying-with-the-maersk-brand |
| Maersk API Solutions | https://www.maersk.com/digital-services/data-integrations/api |
| Maersk Developer Portal | https://developer.maersk.com |
| DCSA About/Members | https://dcsa.org/about-us |
| INTTRA Carrier Network | https://www.inttra.com/ocean-carrier-network/ |
| project44 Alianca Tracking | https://www.project44.com/tracking/container/alianca/ |
| Vizion Supported Carriers | https://docs.vizionapi.com/docs/supported-carriers |
| SeaRates Alianca Tracking | https://www.searates.com/sealine/alianca |
| Shipsgo ANRM Tracking | https://shipsgo.com/ocean/container-prefixes/anrm/container-tracking |
| SCAC Code Reference | https://www.sli-logistics.com/scac-code |
