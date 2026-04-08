# FESCO Transportation Group -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing
> **Researched by**: Agent
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | PJSC Far Eastern Shipping Company (commonly "FESCO") |
| **SCAC Code** | FESO |
| **Parent Company** | FESCO Transportation Group (majority owned by Rosatom State Corporation since 2023) |
| **Alliance** | None / Independent |
| **Primary Services** | Container shipping, intermodal transport (sea + rail + truck), port operations, logistics |
| **Market Position** | Russia's largest private intermodal transportation group; largest port container operator in the Russian Far East. Regional specialist focused on Russia-Asia trade corridors |
| **Headquarters** | Moscow (legal); Vladivostok (operational branch), Russia |
| **Website** | https://www.fesco.com/en/ |

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | No |
| **Developer portal URL** | N/A |
| **API documentation URL(s)** | N/A -- no public API documentation found |
| **Documentation quality** | None -- no developer-facing documentation exists publicly |
| **OpenAPI/Swagger spec available?** | No |
| **Sandbox/test environment?** | No / Unknown |
| **Developer registration** | N/A -- no public API program |
| **Developer support channels** | General contact via fesco.com; no developer-specific channels found |
| **Community/third-party libraries** | None found for direct FESCO integration. Third-party aggregators (project44, Portcast, ShipsGo, GoComet) provide FESCO tracking via their own APIs |
| **API changelog / release notes** | N/A |

### MY.FESCO Portal

FESCO operates a customer-facing digital platform at https://my.fesco.com/ which provides:
- Container tracking (by container number, B/L number, or booking number)
- Quote requests
- Schedule and tariff information
- Personal account management

This is a web portal for end users, not a developer API. No REST/SOAP API endpoints, authentication tokens, or programmatic access methods have been documented or made publicly available.

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | No |
| **DCSA APIs implemented** | None |
| **DCSA TNT version** | N/A |
| **DCSA Booking version** | N/A |
| **DCSA Schedules version** | N/A |
| **Known DCSA deviations** | N/A -- FESCO does not implement any DCSA standards |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Unknown | No public documentation found on EDI capabilities. Given FESCO's focus on Russia-Asia corridors, EDI may be available for select partners but is not publicly documented |
| **INTTRA integration** | Unknown | No evidence of INTTRA/E2open partnership found. INTTRA's coverage of Russian carriers is limited |
| **BIC (Bureau International des Containers)** | Yes | Standard BIC container identification format used in tracking (container numbers follow ISO 6346) |
| **UN/LOCODE** | Unknown | Portal likely uses standard port codes for Russian Far East ports (RUVVO for Vladivostok, etc.) but not confirmed for API/data purposes |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | N/A -- no public API |
| **Auth documentation** | N/A |
| **Registration process** | N/A -- MY.FESCO portal registration available for customer tracking; no API credentials issued |
| **Registration URL** | https://my.fesco.com/ (portal only) |
| **Partner program required?** | N/A |
| **Partner program URL** | N/A |
| **Credential type** | N/A |
| **Token refresh supported?** | N/A |
| **Token lifetime** | N/A |
| **Access tiers** | N/A |
| **IP whitelisting required?** | N/A |

### Access Requirements Summary for SSL

FESCO does not offer a public API or developer portal. The only direct digital access is through the MY.FESCO web portal at https://my.fesco.com/, which provides container tracking and quote functionality through a browser-based interface.

Furthermore, FESCO is subject to sanctions from the EU, UK, Switzerland, Ukraine, and Monaco due to its role as a strategically significant Russian transport entity. While FESCO does not appear on the US OFAC SDN list as of the research date, the broad international sanctions regime creates significant compliance risk for any direct integration. SSL would need to conduct a thorough sanctions compliance review before pursuing any direct relationship or data exchange with FESCO.

For tracking data, third-party aggregators (project44, Portcast, GoComet) offer FESCO container tracking through their own APIs, which may be a more practical and compliant access path.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field has a row.
> Availability legend: check = Available | x = Not available | warning = Partial / limited | question = Unknown

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ❌ | N/A | N/A | N/A | No public API. Schedule information visible on MY.FESCO portal and fesco.com but not programmatically accessible |
| 1.2 | Point-to-Point Route Options | ❌ | N/A | N/A | N/A | Quote request available via portal but no API |
| 1.3 | Booking Lifecycle | ❌ | N/A | N/A | N/A | Booking likely managed through direct commercial relationship; no API access |
| 1.4 | Shipping Instructions | ❌ | N/A | N/A | N/A | No API. Likely handled via email/portal for existing customers |
| 1.5 | Rates | ❌ | N/A | N/A | N/A | Quote request available via MY.FESCO portal but no programmatic rate API |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❌ | N/A | N/A | `ECP` | No API access |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❌ | N/A | N/A | `EFC` | No API access |
| 2.3 | Documentation Cutoff | DCO | ❌ | N/A | N/A | `DCO` | No API access |
| 2.4 | VGM Cutoff | VCO | ❌ | N/A | N/A | `VCO` | No API access |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ❌ | N/A | N/A | `FCO` | No API access |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❌ | N/A | N/A | `LCO` | No API access |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ❌ | N/A | N/A | Inferred from first EquipmentEvent | No API access |
| 3.2 | Empty Container Gate-Out (Pickup) | ❌ | N/A | N/A | `GTOT` + `EMPTY` | No API. May be visible on MY.FESCO portal |
| 3.3 | Full Container Gate-In | ❌ | N/A | N/A | `GTIN` + `LADEN` | No API. May be visible on MY.FESCO portal |
| 3.4 | Container Loaded on Vessel | ❌ | N/A | N/A | `LOAD` + `LADEN` | No API. May be visible on MY.FESCO portal |
| 3.5 | Container Discharged at Transshipment | ❌ | N/A | N/A | `DISC` + `LADEN` + transshipment | No API |
| 3.6 | Container Loaded at Transshipment | ❌ | N/A | N/A | `LOAD` + `LADEN` + transshipment | No API |
| 3.7 | Container Discharged at Destination | ❌ | N/A | N/A | `DISC` + `LADEN` | No API. May be visible on MY.FESCO portal |
| 3.8 | Full Container Gate-Out (Delivery) | ❌ | N/A | N/A | `GTOT` + `LADEN` | No API |
| 3.9 | Empty Container Returned | ❌ | N/A | N/A | `GTIN` + `EMPTY` | No API. GoComet offers FESCO empty return tracking via their platform |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ❌ | N/A | N/A | `DEPA` + classifier | No API. Schedule data visible on portal |
| 4.2 | Estimated Time of Arrival | ETA | ❌ | N/A | N/A | `ARRI` + classifier | No API. Schedule data visible on portal |
| 4.3 | Vessel Arrival at Transshipment | -- | ❌ | N/A | N/A | `ARRI` at intermediate | No API |
| 4.4 | Vessel Departure from Transshipment | -- | ❌ | N/A | N/A | `DEPA` at intermediate | No API |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❌ | No API, no webhook capability |
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

> **Notes on Coverage:**
> - FESCO has zero direct API coverage because the carrier does not offer any public API or developer portal.
> - The MY.FESCO web portal at https://my.fesco.com/ does provide container tracking, schedule information, and quote requests through a browser interface, but none of this is exposed as a programmatic API.
> - Third-party aggregators (project44, Portcast, GoComet, ShipsGo) do offer FESCO tracking data via their own APIs, providing an indirect path to some container milestones and transport events.
> - The sanctions status of FESCO further complicates any direct integration path.

---

## Endpoint Reference

FESCO does not offer any public API endpoints. This section is intentionally left empty.

### Lookup Methods Summary

| Identifier Type | Supported? | Which Endpoints? | Notes |
|----------------|-----------|-----------------|-------|
| **Bill of Lading (B/L) number** | ❌ (direct) | N/A | Supported on MY.FESCO web portal and via third-party aggregators |
| **Booking reference** | ❌ (direct) | N/A | Supported on MY.FESCO web portal |
| **Container number** | ❌ (direct) | N/A | Supported on MY.FESCO web portal and via third-party aggregators. Container number noted as the most precise lookup key |
| **Carrier booking number** | ❌ (direct) | N/A | Unknown |
| **Vessel IMO / voyage** | ❌ (direct) | N/A | Unknown |

---

## Rate Limits & Quotas

N/A -- FESCO does not offer a public API. Rate limits would apply to third-party aggregator APIs if used for FESCO tracking.

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | https://my.fesco.com/ |
| **Login required?** | Unknown -- portal access likely requires account registration |
| **Data available on portal but NOT in API** | All data is portal-only since no API exists. Portal provides container tracking (by container number, B/L, or booking number), schedule/tariff information, and quote requests |
| **Scraping feasibility** | Not assessed -- sanctions compliance concerns would likely prohibit direct data extraction regardless of technical feasibility. Third-party aggregators provide a cleaner path |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Unknown |
| **EDI message types** | Unknown -- no public documentation found |
| **EDI connection method** | Unknown |
| **EDI documentation** | N/A -- contact FESCO directly |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Notes |
|-----------|-------------------|-------|
| **project44** | Yes | project44 has a dedicated FESCO container tracking page (https://www.project44.com/tracking/container/fesco/). Likely the most practical integration path |
| **FourKites** | Unknown | FourKites covers 85+ ocean carriers; FESCO coverage not explicitly confirmed |
| **Vizion** | Unknown | Vizion claims 99% ocean freight coverage; FESCO coverage not explicitly confirmed |
| **INTTRA / E2open** | Unknown | No evidence of FESCO-INTTRA partnership found |
| **CargoSmart** | Unknown | No evidence of FESCO-CargoSmart connection found |
| **Portcast** | Yes | Portcast offers FESCO container tracking with predictive ETAs (https://www.portcast.io/carrier-coverage/fesco-far-eastern-shipping-company-container-tracking) |
| **GoComet** | Yes | GoComet provides FESCO tracking including empty return tracking (https://www.gocomet.com/online-container-tracking/carriers/far-eastern-shipping-company) |
| **ShipsGo** | Yes | ShipsGo offers FESCO container tracking API integration (https://shipsgo.com/ocean/carriers/fesco/container-tracking) |
| **Fluent Cargo** | Yes | Fluent Cargo provides FESCO sailing schedules (https://www.fluentcargo.com/carriers/scac/FESO) |

> **Aggregator note:** Since FESCO has no direct API, third-party aggregators are the only programmatic path to FESCO tracking data. project44 and Portcast appear to have confirmed FESCO coverage with dedicated carrier pages. However, sanctions compliance must be evaluated -- aggregators scraping or receiving data from a sanctioned entity may carry its own compliance implications depending on jurisdiction.

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown -- no direct API. Aggregator freshness depends on their data source (likely portal scraping or carrier data feeds) | Unknown |
| **API uptime/reliability** | N/A -- no API | N/A |
| **Historical data depth** | Unknown | Unknown |
| **Timezone handling** | Unknown -- FESCO operates primarily in Russia (Moscow Time UTC+3 and Vladivostok Time UTC+10). Portal data timezone handling unknown | Estimated |
| **Character encoding** | Unknown -- portal content available in Russian and English. Cyrillic character handling may be relevant | Estimated |

### Known Issues & Gotchas

- **No public API**: FESCO does not provide any developer-facing API, making direct integration impossible. All programmatic access must go through third-party aggregators.

- **International sanctions**: FESCO is sanctioned by the EU, UK, Switzerland, Ukraine, and Monaco. While not currently on the US OFAC SDN list (as of research date), the broad sanctions regime creates significant compliance risk. SSL must conduct a thorough legal/compliance review before any integration, even via third-party aggregators.

- **Russia-focused operations**: FESCO's services are concentrated on Russia-Asia trade corridors (particularly Russia Far East to China, South Korea, Japan, and India). Limited relevance for carriers operating primarily in Western trade lanes.

- **Rosatom ownership**: FESCO has been majority-owned by Rosatom (Russia's state nuclear energy corporation) since 2023, which may compound sanctions and compliance concerns.

- **Limited English documentation**: FESCO's digital presence is primarily in Russian. English-language information on fesco.com is limited compared to the Russian-language site at fesco.ru.

- **Portal-only tracking**: Container tracking on MY.FESCO is web-portal-based with no documented API. The portal accepts container number, B/L number, and booking number as lookup keys.

### Recently Deprecated or Changed

- No deprecation notices found. FESCO has not had a public API to deprecate.

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | No (direct) / Partial (via aggregator) -- FESCO has no public API, making direct adapter development impossible. Tracking data is accessible through third-party aggregators (project44, Portcast, GoComet) which could serve as an indirect data source. However, sanctions compliance must be resolved first |
| **Implementation effort** | Very High (no API) for direct integration. Medium for aggregator-mediated integration (depends on chosen aggregator's SDK/API) |
| **DCSA base adapter usable?** | No -- FESCO is not a DCSA member and has no API at all |

### Recommended Approach

Direct integration with FESCO is not feasible given the absence of any public API. The recommended approach, if FESCO tracking is required, is aggregator-mediated integration:

1. **Primary path**: Use project44's ocean visibility API, which has confirmed FESCO coverage. project44 normalizes carrier data into a standard format, abstracting away the lack of direct API access. This also provides a layer of separation that may simplify (though not eliminate) sanctions compliance considerations.

2. **Alternative path**: Portcast or GoComet offer similar FESCO tracking capabilities and may be more cost-effective depending on SSL's existing aggregator relationships.

3. **Prerequisite**: Before any integration path is pursued, SSL must conduct a sanctions compliance review with legal counsel. Even indirect data access through aggregators may carry compliance implications given FESCO's sanctioned status under EU/UK regulations.

FESCO should be considered a low-priority carrier for integration given the combination of no direct API, sanctions risk, and the carrier's regional focus on Russia-Asia corridors which may have limited relevance for SSL's primary markets.

### Recommended Lookup Method

If pursuing aggregator-mediated tracking, **container number** is reported as the most precise lookup key for FESCO shipments. Bill of Lading number is also supported by the MY.FESCO portal and most aggregators.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | Dependent on aggregator API -- follow aggregator's recommended polling intervals (typically every 2-6 hours) |
| **Incremental filter** | Dependent on aggregator -- project44 and others typically support event-based filtering |
| **Batch tracking** | Dependent on aggregator -- most aggregators support batch container tracking |

### Auth Implementation Notes

No direct auth implementation needed since FESCO has no public API. Auth requirements would be determined by the chosen aggregator (project44, Portcast, etc.) and their respective API authentication mechanisms.

### Edge Cases to Handle

- **Sanctions compliance changes**: The sanctions landscape affecting FESCO is evolving. SSL would need to monitor for changes in OFAC, EU, and UK sanctions lists that could affect the legality of receiving FESCO data, even through aggregators.

- **Cyrillic data**: Port names, vessel names, and status descriptions from FESCO may include Cyrillic characters, particularly for Russian domestic ports. Ensure UTF-8 handling throughout the data pipeline.

- **Limited route coverage**: FESCO primarily operates Russia-Asia corridors. Container tracking may be less comprehensive for any services touching Western ports (if applicable).

- **Aggregator data gaps**: Third-party aggregators may not have complete milestone coverage for FESCO. Data availability may be limited compared to major global carriers.

### Mapping Complexity

**Low complexity for the mapping itself, but high complexity for the overall integration.** Since no direct API exists, there is no carrier-specific field mapping to perform. The mapping complexity shifts to the chosen aggregator's data model, which is typically already normalized. The primary complexity is operational/legal (sanctions compliance) rather than technical.

---

## Open Questions

- [ ] Is FESCO on the US OFAC SDN list or any other US sanctions list? -- Requires definitive legal review; preliminary research suggests not currently on SDN but sanctions landscape is fluid
- [ ] Does SSL have any business need for FESCO tracking given its Russia-Asia corridor focus?
- [ ] Would sanctions compliance permit SSL to receive FESCO tracking data even through third-party aggregators?
- [ ] Does project44's FESCO coverage include full container milestone tracking or only basic status?
- [ ] Does FESCO offer any private/partner API that is not publicly documented? -- Would require direct commercial engagement (subject to sanctions review)
- [ ] Does FESCO support EDI through any network? -- No public documentation found
- [ ] What is the data freshness of FESCO tracking data through aggregators like project44 or Portcast?

---

## Source Links

| Resource | URL |
|----------|-----|
| Carrier Website (English) | https://www.fesco.com/en/ |
| Carrier Website (Russian) | https://www.fesco.ru/ |
| MY.FESCO Portal | https://my.fesco.com/ |
| FESCO Annual Report 2024 | https://ar2024.fesco.com/about |
| Wikipedia | https://en.wikipedia.org/wiki/Fesco_Transport_Group |
| OpenSanctions Entry | https://www.opensanctions.org/entities/NK-9b6nPmnZBk6UuBPmBhS967/ |
| project44 FESCO Tracking | https://www.project44.com/tracking/container/fesco/ |
| Portcast FESCO Tracking | https://www.portcast.io/carrier-coverage/fesco-far-eastern-shipping-company-container-tracking |
| GoComet FESCO Tracking | https://www.gocomet.com/online-container-tracking/carriers/far-eastern-shipping-company |
| ShipsGo FESCO Tracking | https://shipsgo.com/ocean/carriers/fesco/container-tracking |
| Fluent Cargo FESCO Schedules | https://www.fluentcargo.com/carriers/scac/FESO |
| SeaRates FESCO Tracking | https://www.searates.com/sealine/fesco |
| FESCO LinkedIn | https://www.linkedin.com/company/fesco-transportation-group |
