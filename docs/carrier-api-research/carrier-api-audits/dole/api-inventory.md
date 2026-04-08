# Dole Ocean Cargo Express -- API Inventory

> **Status**: Complete
> **Methodology**: Documentation review only -- not verified with live API testing. Research based on public website (doleoceancargo.com, built on Salesforce Experience Cloud), Salesforce digital transformation case study (Freeway Consulting), Panjiva shipping profile, SeaDex carrier profile, DCSA membership records, and third-party aggregator carrier lists. No API credentials were obtained or used.
> **Researched by**: Agent (carrier API inventory workflow)
> **Date**: 2026-02-17
> **Last verified**: 2026-02-17

---

## Carrier Overview

| Detail | Value |
|--------|-------|
| **Carrier Name** | Dole Ocean Cargo Express, LLC (DOCE) |
| **SCAC Code** | DOLQ |
| **Parent Company** | Dole Food Company (parent); Reefership Marine Services, Ltd. (exclusive maritime transportation/vessel management provider) |
| **Alliance** | Independent -- not a member of any shipping alliance |
| **Primary Services** | Refrigerated container shipping (reefer specialist), conventional reefer pallet vessels, perishable cargo (bananas, fresh fruit, produce) |
| **Market Position** | Niche specialist: operates the largest dedicated refrigerated containerized fleet in the world. Not a top-20 container carrier by total TEU volume, but dominant in the Americas perishable trade (bananas, fresh fruit). Licensed VOCC offering third-party commercial cargo services on Dole's vessels |
| **Headquarters** | Charlotte, North Carolina, USA (200 South Tryon Street, Suite 500) |
| **Website** | [https://www.doleoceancargo.com](https://www.doleoceancargo.com) |

### Corporate Structure (Relevant Entities)

| Entity | Role | Digital Infrastructure |
|--------|------|----------------------|
| **Dole Ocean Cargo Express, LLC (DOCE)** | Commercial cargo arm -- sells space on Dole vessels to third-party shippers | Salesforce Experience Cloud portal at doleoceancargo.com |
| **Dole Food Company** | Parent company -- one of the world's largest producers/distributors of fresh fruit and vegetables | Corporate site at dole.com |
| **Reefership Marine Services, Ltd. (RMS)** | Exclusive maritime transportation provider for Dole Fresh Fruit and DOCE -- manages the vessel fleet | Separate site at dole-reefership.com |

> **Note**: Dole Ocean Cargo Express began in 1993 as Dole Ocean Liner Express Inc. It operates as a VOCC (Vessel Operating Common Carrier), selling available space on Dole's fleet to commercial customers. The fleet is technically managed by Reefership Marine Services, which has managed Dole's fleet since 1986.

---

## Digital Ecosystem & Developer Experience

| Detail | Value |
|--------|-------|
| **Has developer portal?** | **No** -- no public developer portal, API documentation, or developer program exists |
| **Developer portal URL** | N/A |
| **API documentation URL(s)** | N/A |
| **Documentation quality** | None -- no API documentation is publicly available |
| **OpenAPI/Swagger spec available?** | No |
| **Sandbox/test environment?** | No |
| **Developer registration** | N/A |
| **Developer support channels** | General contact only: [doleoceancargo.com contact page](https://dole.my.site.com/doce2/s/contact-information?language=en_US), email/phone via DOCE commercial team |
| **Community/third-party libraries** | None found -- no GitHub repos, npm packages, or PyPI packages for DOCE integration |
| **API changelog / release notes** | N/A |

### Salesforce Experience Cloud Portal

DOCE's customer-facing website at `doleoceancargo.com` is built on **Salesforce Experience Cloud** (formerly Community Cloud), implemented in partnership with Freeway Consulting (launched June 2023). The platform uses Salesforce Sales Cloud for CRM/transactional data and Experience Cloud for the customer-facing portal.

**Public site** (no login required):
- General service information and route descriptions
- Vessel fleet information (vessel names, specs)
- Published sailing schedules (US West Coast, other routes)
- Tracking page (lookup by B/L, container, or booking reference)
- Rate request form
- Booking request form

**Private site** (login required -- customer portal):
- Vessel tracking with detailed status
- Booking management (tickets, reservations)
- Billing and invoicing
- Bill of Lading access
- Dispatch orders
- Cargo collection status
- Signed contracts

The portal integrates data from both Salesforce Core and external systems (route information, shipping schedules, container capacity). The URL structure reveals Salesforce-native patterns: `/s/tracking-page`, `/s/doce-site-booking/{id}`, `/s/doce-container-traceability/{id}`, `/s/traceability-activity/{id}`.

**Traceability data model**: The portal exposes "Container Traceability" and "Traceability Activity" pages (e.g., URLs like `/s/doce-container-traceability/a3L3n00000F8nCiEAJ/szlu9899081` and `/s/traceability-activity/a3QUq000009668oMAA/vpf-discharged-from-vessel`). The latter URL fragment "vpf-discharged-from-vessel" confirms that individual container milestone events are tracked and exposed in the portal. However, this data is served through Salesforce Experience Cloud rendered pages -- not a REST API.

---

## Standards Compliance

### DCSA (Digital Container Shipping Association)

| Detail | Value |
|--------|-------|
| **DCSA member?** | **No** -- Dole Ocean Cargo Express is not a DCSA member. DCSA members (as of 2025) are: MSC, Maersk, CMA CGM, Hapag-Lloyd, ONE, Evergreen, Yang Ming, HMM, ZIM, and PIL. DOCE is a niche reefer specialist, not a major container line |
| **DCSA APIs implemented** | None |
| **DCSA TNT version** | N/A |
| **DCSA Booking version** | N/A |
| **DCSA Schedules version** | N/A |
| **Known DCSA deviations** | N/A -- no DCSA implementation |

### Other Standards

| Standard | Supported? | Notes |
|----------|-----------|-------|
| **UN/EDIFACT (EDI)** | Unknown | No public documentation of EDI support. As a licensed VOCC, DOCE likely supports basic EDI messaging for customs and booking, but this is unverified |
| **INTTRA integration** | Unknown | Not confirmed. DOCE's niche market (perishable/reefer) may not overlap heavily with INTTRA's primarily container-line customer base |
| **BIC (Bureau International des Containers)** | Likely Yes | Container numbers on the portal follow BIC ISO 6346 format (e.g., SZLU9899081) |
| **UN/LOCODE** | Unknown | Port codes are visible in booking references but format is not confirmed |

---

## Authentication & Access

| Detail | Value |
|--------|-------|
| **Auth mechanism** | N/A -- no public API |
| **Auth documentation** | N/A |
| **Registration process** | N/A for API. For portal access: customers receive login credentials through their DOCE commercial relationship |
| **Registration URL** | N/A |
| **Partner program required?** | N/A for API. Portal access requires active customer/business relationship |
| **Partner program URL** | N/A |
| **Credential type** | N/A (portal uses Salesforce username/password login) |
| **Token refresh supported?** | N/A |
| **Token lifetime** | N/A |
| **Access tiers** | N/A |
| **IP whitelisting required?** | N/A |

### Access Requirements Summary for SSL

There is no public API to access. The primary data access path for SSL would be through the Salesforce Experience Cloud portal (requires a customer/business relationship with DOCE to obtain login credentials), third-party aggregators (if DOCE is covered), or EDI messaging (if supported). SSL would need to contact DOCE's commercial team to discuss digital integration options. Given that DOCE built their portal on Salesforce in 2023, there may be willingness to discuss API access -- Salesforce provides API capabilities natively -- but this would require direct engagement.

---

## Required Fields Coverage Matrix

> Cross-reference with `docs/required-data-fields.md`. Every field must have a row.
> Availability assessment is based on what the Salesforce portal appears to expose (from URL structure and case study descriptions). Without API access, all assessments are inferred.

### API Domains (Section 1)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|-------------------------|-------------|-------|
| 1.1 | Vessel & Port Schedules | ⚠️ | Portal: `/s/us-west-coast-sailing-schedule` | N/A (rendered HTML) | N/A | Published sailing schedules are available on the public website for specific routes. Not available via API |
| 1.2 | Point-to-Point Route Options | ❌ | N/A | N/A | N/A | No point-to-point route query capability found |
| 1.3 | Booking Lifecycle | ⚠️ | Portal: `/s/doce-site-booking/{id}` | N/A (Salesforce objects) | N/A | Booking management available in the private customer portal. Not available via API. Booking request form exists on public site |
| 1.4 | Shipping Instructions | ❓ | Unknown | Unknown | N/A | May be available in the private portal but not confirmed |
| 1.5 | Rates | ⚠️ | Portal: rate request form | N/A | N/A | Rate requests submitted via web form. No programmatic rate API |

### Document & Cargo Cutoffs (Section 2)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Field/Event Code | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|-------------------------|-------------|-------|
| 2.1 | Earliest Container Release Date | ERD | ❓ | Unknown | Unknown | `ECP` | May be communicated through booking confirmation but not confirmed in any public-facing data |
| 2.2 | Earliest Full-Container Delivery Date | EFC | ❓ | Unknown | Unknown | `EFC` | Same as above |
| 2.3 | Documentation Cutoff | DCO | ❓ | Unknown | Unknown | `DCO` | Likely communicated to customers but method unknown |
| 2.4 | VGM Cutoff | VCO | ❓ | Unknown | Unknown | `VCO` | VGM submission is a SOLAS requirement; cutoff likely exists but exposure method unknown |
| 2.5 | Container/Cargo Cutoff (FCL) | FCO | ❓ | Unknown | Unknown | `FCO` | Likely communicated to customers but method unknown |
| 2.6 | Container/Cargo Cutoff (LCL) | LCO | ❓ | Unknown | Unknown | `LCO` | Likely N/A -- DOCE primarily handles FCL reefer containers, not LCL |

### Container Milestones (Section 3)

| # | Canonical Field | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|-----------|-----------------|------------------------|-------------|-------|
| 3.1 | Container Assigned to Booking | ❓ | Unknown | Unknown | Inferred from first EquipmentEvent | Unknown |
| 3.2 | Empty Container Gate-Out (Pickup) | ❓ | Unknown | Unknown | `GTOT` + `EMPTY` | Unknown -- may be tracked in private portal |
| 3.3 | Full Container Gate-In | ❓ | Unknown | Unknown | `GTIN` + `LADEN` | Unknown |
| 3.4 | Container Loaded on Vessel | ⚠️ | Portal: traceability activity pages | Inferred from URL slug (e.g., "loaded-on-vessel") | `LOAD` + `LADEN` | The portal exposes traceability activities but only through rendered HTML pages, not API |
| 3.5 | Container Discharged at Transshipment | ❓ | Unknown | Unknown | `DISC` + `LADEN` + transshipment | Unknown |
| 3.6 | Container Loaded at Transshipment | ❓ | Unknown | Unknown | `LOAD` + `LADEN` + transshipment | Unknown |
| 3.7 | Container Discharged at Destination | ⚠️ | Portal: `/s/traceability-activity/{id}/vpf-discharged-from-vessel` | "VPF - Discharged from vessel" | `DISC` + `LADEN` | Confirmed event type from portal URL. Available through portal but not via API |
| 3.8 | Full Container Gate-Out (Delivery) | ❓ | Unknown | Unknown | `GTOT` + `LADEN` | Unknown |
| 3.9 | Empty Container Returned | ❓ | Unknown | Unknown | `GTIN` + `EMPTY` | Unknown |

### Vessel Schedule / Transport Events (Section 4)

| # | Canonical Field | Abbrev | Available? | Carrier Endpoint | Carrier Event Signature | DCSA Mapping | Notes |
|---|----------------|--------|-----------|-----------------|------------------------|-------------|-------|
| 4.1 | Estimated Time of Departure | ETD | ⚠️ | Portal: sailing schedule pages | N/A (rendered HTML) | `DEPA` + classifier | Available on published schedule pages but not via API |
| 4.2 | Estimated Time of Arrival | ETA | ⚠️ | Portal: sailing schedule pages, booking details | N/A (rendered HTML) | `ARRI` + classifier | Available on published schedule pages and in booking details but not via API |
| 4.3 | Vessel Arrival at Transshipment | -- | ❓ | Unknown | Unknown | `ARRI` at intermediate | Unknown -- DOCE operates relatively direct routes (Central America to US) with limited transshipment |
| 4.4 | Vessel Departure from Transshipment | -- | ❓ | Unknown | Unknown | `DEPA` at intermediate | Same as above |

### Change Detection (Section 5)

| Mechanism | Supported? | Details |
|-----------|-----------|---------|
| Event Subscriptions (Webhooks) | ❌ | No webhook/push mechanism found |
| Event Polling with timestamp filter | ❌ | No API to poll |
| Event Classifier Progression (PLN->EST->ACT) | ❌ | No DCSA-style event classification |
| Retracted Events | ❌ | No mechanism found |
| Change Remarks | ❓ | Unknown -- may exist in portal notifications |
| Delay Reason Codes | ❓ | Unknown |

### Coverage Summary

| Category | Fields Available | Fields Unavailable | Fields Unknown | Coverage % |
|----------|-----------------|-------------------|----------------|-----------|
| API Domains (1.x) | 0/5 | 2/5 | 3/5 | 0% |
| Cutoffs (2.x) | 0/6 | 0/6 | 6/6 | 0% |
| Container Milestones (3.x) | 0/9 | 0/9 | 9/9 | 0% |
| Transport Events (4.x) | 0/4 | 0/4 | 4/4 | 0% |
| Change Detection (5.x) | 0/6 | 4/6 | 2/6 | 0% |
| **Total** | **0/30** | **6/30** | **24/30** | **0%** |

> **Note**: The 0% coverage reflects the absence of a programmatic API. The Salesforce portal likely tracks many of these fields internally (container milestones, ETD/ETA, booking lifecycle), but none are accessible via a public API. If Salesforce API access were negotiated, coverage could potentially improve significantly.

---

## Endpoint Reference

DOCE does not expose any public REST API endpoints. The customer-facing portal is a Salesforce Experience Cloud application. Salesforce Experience Cloud sites can expose data through Salesforce Connect APIs or custom Apex REST endpoints, but DOCE has not published any such endpoints for external consumption.

### Lookup Methods Summary

| Identifier Type | Supported? | Which Endpoints? | Notes |
|----------------|-----------|-----------------|-------|
| **Bill of Lading (B/L) number** | Portal only | Tracking page at `/s/tracking-page` | B/L lookup available on the public tracking page |
| **Booking reference** | Portal only | Tracking page, booking detail pages | Booking references follow pattern "GPTTxxxxHD" based on URL analysis |
| **Container number** | Portal only | Tracking page, container traceability pages | Container numbers follow BIC ISO 6346 format |
| **Carrier booking number** | Portal only | Same as booking reference | |
| **Vessel IMO / voyage** | Portal only | Vessel pages at `/s/vessels` | Vessel information available on the public site |

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
| **Webhooks supported?** | **No** -- no webhook or push notification mechanism found |
| **Alternative** | Salesforce Experience Cloud natively supports Platform Events and Streaming API, but DOCE has not exposed these capabilities externally |

---

## Non-API Access Methods

### Web Portal Tracking

| Detail | Value |
|--------|-------|
| **Tracking URL** | [https://www.doleoceancargo.com/s/tracking-page?language=en_US](https://www.doleoceancargo.com/s/tracking-page?language=en_US) |
| **Login required?** | No (for basic tracking); Yes (for detailed booking/cargo management) |
| **Data available on portal but NOT in API** | All data is portal-only: tracking milestones, booking details, sailing schedules, vessel information, B/L access, billing. There is no API |
| **Scraping feasibility** | **Difficult** -- the site is built on Salesforce Experience Cloud, which uses Lightning Web Components (LWC) with client-side rendering, CSRF tokens, and dynamic JavaScript. Standard scraping tools will not work. Salesforce Experience Cloud sites also have anti-bot protections. ToS likely prohibit scraping |

### Container Traceability (Portal)

The portal provides "Container Traceability" views showing individual container milestone events. Confirmed event types from URL analysis include:
- "VPF - Discharged from vessel" (from `/s/traceability-activity/{id}/vpf-discharged-from-vessel`)
- Additional event types likely exist but are not enumerable without portal access

### Published Sailing Schedules

| Route | URL |
|-------|-----|
| US West Coast | [https://www.doleoceancargo.com/s/us-west-coast-sailing-schedule](https://www.doleoceancargo.com/s/us-west-coast-sailing-schedule?language=en_US) |
| Other routes | Available on the service page at [/s/service-page](https://www.doleoceancargo.com/s/service-page?language=en_US) |

### EDI (Electronic Data Interchange)

| Detail | Value |
|--------|-------|
| **EDI supported?** | Unknown -- no public documentation. As a licensed VOCC, basic EDI messaging (for US Customs, AMS filings) is likely but unconfirmed for commercial B2B use |
| **EDI message types** | Unknown |
| **EDI connection method** | Unknown |
| **EDI documentation** | Not publicly available |

### Third-Party Aggregators

| Aggregator | Carrier Available? | Confidence | Notes |
|-----------|-------------------|------------|-------|
| **project44** | ❓ Unknown | Low | project44 lists DOLQ as a SCAC code in their ocean carrier appendix but whether they have active data coverage is unverified |
| **FourKites** | ❓ Unknown | Low | No specific mention of DOCE in available documentation |
| **Vizion** | **No** | High | DOCE/DOLQ is **not listed** on Vizion's supported carriers page (verified 2026-02-17). Contact support@vizionapi.com to inquire |
| **INTTRA / E2open** | ❓ Unknown | Low | Not confirmed. DOCE's niche reefer market may not overlap with INTTRA's core carrier network |
| **CargoSmart** | ❓ Unknown | Low | No specific mention found |
| **Terminal49** | **No** | High | DOCE/DOLQ is **not listed** among Terminal49's 33 integrated shipping lines (verified 2026-02-17) |
| **SeaRates** | Yes (tracking page) | Medium | SeaRates offers a [Dole Ocean Cargo Express tracking page](https://www.searates.com/sealine/dole_ocean_cargo_express) but this may rely on AIS vessel tracking rather than direct carrier data |
| **Visiwise** | Yes (tracking page) | Medium | Visiwise offers [B/L tracking for Dole](https://www.visiwise.co/tracking/bl/dole/) and [booking tracking](https://www.visiwise.co/tracking/booking/dole/) -- data source unclear |

> **Aggregator note**: Given that DOCE has no API, aggregator coverage is particularly important as a fallback. However, major aggregators (Vizion, Terminal49) do not list DOCE. SeaRates and Visiwise offer tracking pages but their data sources are unconfirmed -- they may scrape the DOCE portal or use AIS data. SSL should verify aggregator capabilities before relying on them.

### PayCargo Integration

| Detail | Value |
|--------|-------|
| **PayCargo available?** | Yes -- [DOCE is listed on PayCargo](https://paycargo.com/vendors/dole-ocean-express/) for freight payment processing |
| **Relevance** | PayCargo integration confirms DOCE has some digital B2B infrastructure, though this is financial (not tracking) |

---

## Data Quality & Operational Notes

| Aspect | Assessment | Source |
|--------|-----------|--------|
| **Event freshness** | Unknown -- no API to measure. Portal tracking appears to show milestone events (load, discharge) but update frequency is unknown | Unknown |
| **API uptime/reliability** | N/A -- no API | N/A |
| **Historical data depth** | Unknown | Unknown |
| **Timezone handling** | Unknown | Unknown |
| **Character encoding** | UTF-8 (Salesforce standard) | Estimated |

### Known Issues & Gotchas

- **No public API** -- the fundamental blocker. All data access is through the Salesforce Experience Cloud portal, which is not designed for programmatic consumption.
- **Salesforce-native data model** -- DOCE's data lives in Salesforce objects (likely custom objects for bookings, containers, traceability activities). The Salesforce IDs are visible in URLs (e.g., `a3NUq000000fQ6bMAE`, `a3L3n00000F8nCiEAJ`). If DOCE were willing to grant Connected App access, these objects could theoretically be queried via Salesforce APIs (REST API, SOQL).
- **Reefer-centric operations** -- DOCE's fleet is primarily refrigerated. Additional data fields like temperature monitoring, reefer unit status, and atmosphere control may be relevant but are not in the standard SSL field list.
- **Small fleet, limited routes** -- 17 vessels, 16 ports, 5 routes. Coverage is narrow (Americas/Caribbean perishable trade). This limits the volume of trackable shipments.
- **SSL certificate issue** -- `doleoceancargo.com` returned an SSL certificate verification error during research, suggesting a potential infrastructure issue (possibly Salesforce CDN configuration).
- **Booking reference format** -- References follow a "GPTTxxxxHD" pattern (e.g., GPTT1014HD, GPTT5795HD, GPTT7091HD, GPTT6644HD), which appears to be a DOCE-internal format.

### Recently Deprecated or Changed

- The Salesforce portal was launched in June 2023 (per Freeway Consulting case study). This is relatively new infrastructure, replacing whatever DOCE used previously.
- A legacy portal at `dole.my.site.com/doce2/` appears to still be accessible alongside the main `doleoceancargo.com` site (both are Salesforce Experience Cloud).

---

## SDK Adapter Recommendations

### Feasibility Assessment

| Aspect | Assessment |
|--------|-----------|
| **Can we build a useful adapter?** | **No** -- not with current publicly available access methods. DOCE does not expose an API. A useful adapter cannot be built without either (a) negotiating Salesforce Connected App API access directly with DOCE, (b) finding an aggregator with confirmed DOCE data coverage, or (c) web scraping (not recommended due to Salesforce anti-bot protections and ToS concerns) |
| **Implementation effort** | **Very High** -- no API exists. If Salesforce API access were negotiated, effort would be High (fully proprietary data model, Salesforce SOQL/REST, no DCSA compliance). If relying on aggregator, effort depends on the aggregator's data quality |
| **DCSA base adapter usable?** | **No** -- DOCE has no DCSA implementation. A fully custom adapter would be needed |

### Recommended Approach

**Phase 1: Verify third-party aggregator coverage.** Before investing in a direct integration, SSL should verify whether any aggregator (project44, SeaRates, Visiwise) has reliable programmatic access to DOCE tracking data. This is the lowest-effort path but depends on data quality and freshness.

**Phase 2: If SSL has meaningful DOCE shipping volume, explore direct Salesforce API access.** Contact DOCE's commercial/IT team to discuss whether they would grant Salesforce Connected App access (OAuth2-based). Salesforce natively supports REST APIs for querying custom objects, and DOCE's data model already includes the relevant objects (bookings, container traceability, traceability activities). This would be a partnership discussion, not a self-service integration.

**Phase 3: If Salesforce access is granted, build a custom adapter.** The adapter would:
1. Authenticate via Salesforce OAuth2 (Connected App)
2. Query booking objects via Salesforce REST API / SOQL
3. Query container traceability objects for milestone events
4. Map DOCE's proprietary event types (e.g., "VPF - Discharged from vessel") to DCSA canonical events
5. Query schedule data if exposed through Salesforce objects

**Architecture (if Salesforce API access is obtained):**

```
SDK CarrierAdapter (Dole / DOLQ)
    |
    +-- Auth: Salesforce OAuth2 Connected App flow
    |   +-- Client ID + Client Secret + username/password or JWT
    |
    +-- Tracking
    |   +-- SOQL: SELECT ... FROM Container_Traceability__c WHERE Container_Number__c = '...'
    |   +-- SOQL: SELECT ... FROM Traceability_Activity__c WHERE Container_Traceability__c = '...'
    |
    +-- Bookings
    |   +-- SOQL: SELECT ... FROM Booking__c WHERE Booking_Reference__c = '...'
    |
    +-- Schedules
        +-- SOQL: SELECT ... FROM Sailing_Schedule__c WHERE ...
```

> **Important caveat**: The Salesforce object names above are speculative, based on URL analysis. Actual object names and field names would only be discoverable after obtaining API access and inspecting the org's metadata.

### Recommended Lookup Method

**Container number** is the most reliable identifier based on portal URL analysis. The container traceability pages use container numbers as slugs. Booking references (GPTTxxxxHD format) are also supported.

### Recommended Polling Strategy

| Detail | Recommendation |
|--------|---------------|
| **Polling interval** | N/A until API access is established. If Salesforce API access is obtained: every 4-6 hours (conservative, respecting Salesforce API call limits) |
| **Incremental filter** | If Salesforce: use `LastModifiedDate` or `SystemModstamp` fields (standard on all Salesforce objects) for incremental queries |
| **Batch tracking** | If Salesforce: SOQL supports `IN` clauses and bulk queries. Multiple containers can be queried in a single call |

### Auth Implementation Notes

If Salesforce Connected App access is obtained:
1. Create a Connected App in the DOCE Salesforce org (requires DOCE admin cooperation)
2. Implement Salesforce OAuth2 Web Server flow or JWT Bearer flow
3. Access Token + Refresh Token pattern
4. Salesforce access tokens expire after the session timeout (default 2 hours)
5. Use the `instance_url` from the OAuth response as the API base URL
6. Respect Salesforce API call limits (varies by org edition -- typically 15,000-100,000 calls/24h)

### Edge Cases to Handle

- **Reefer-specific data**: DOCE is a reefer specialist. Temperature excursions, reefer unit alarms, and atmosphere control events may be critical for their customers but are not standard in the SSL field list. The adapter should be extensible for reefer-specific data.
- **Limited route network**: DOCE operates only in the Americas (Central America, South America, Caribbean to US/Europe). There are no transpacific or Asia-Europe routes. Transshipment is limited.
- **Small fleet dynamics**: With only 17 vessels and 5 routes, vessel substitutions and schedule changes may be more frequent and impactful than with larger carriers.
- **Perishable cargo urgency**: DOCE customers are perishable goods shippers. ETA accuracy and delay notifications are disproportionately important -- a 2-day delay can mean spoiled cargo.
- **Dual Salesforce sites**: Both `doleoceancargo.com` and `dole.my.site.com/doce2/` appear to be active. The adapter should target whichever site the API is exposed from.

### Mapping Complexity

**Unknown** until Salesforce API access is obtained. The key mapping challenge would be converting DOCE's proprietary event types (visible as URL slugs like "vpf-discharged-from-vessel") to DCSA canonical event codes. The "VPF" prefix in event names is unexplained -- it may be an internal code system. A complete event type enumeration would require querying the Salesforce picklist values for the Traceability Activity object.

---

## Open Questions

- [ ] **Q1: Does SSL have meaningful shipping volume with DOCE?** -- DOCE is a niche reefer carrier. If SSL doesn't actively book with DOCE, this integration may be low priority.
- [ ] **Q2: Would DOCE grant Salesforce Connected App API access?** -- This is the critical question. SSL should contact DOCE's commercial team to explore. The Salesforce platform natively supports API access, so the technical capability exists -- it's a business/partnership decision.
- [ ] **Q3: What are DOCE's container traceability event types?** -- The "VPF - Discharged from vessel" event type was identified from URL analysis. A complete list of event types is needed for milestone mapping.
- [ ] **Q4: Do any aggregators have reliable DOCE data?** -- SeaRates and Visiwise offer tracking pages but data source/quality is unverified. project44 may have coverage. SSL should test each with a known DOCE shipment.
- [ ] **Q5: Does DOCE support EDI?** -- If Salesforce API access is not feasible, EDI (IFTSTA for status messages) might be an alternative data path.
- [ ] **Q6: What is the "VPF" prefix in event types?** -- Seen in "VPF - Discharged from vessel". May stand for "Vessel Port Facility" or be an internal code. Needs clarification from DOCE.
- [ ] **Q7: Are reefer-specific data fields (temperature, atmosphere) tracked in the Salesforce system?** -- If so, SSL might want to capture this data for perishable cargo visibility.
- [ ] **Q8: What happened to DOCE's pre-Salesforce digital infrastructure?** -- The Salesforce portal launched June 2023. Any legacy API or EDI connections from the prior system may still exist.

---

## Source Links

| Resource | URL | Status |
|----------|-----|--------|
| DOCE Website (Salesforce Experience Cloud) | [https://www.doleoceancargo.com](https://www.doleoceancargo.com) | Active (SSL cert issue noted) |
| DOCE Tracking Page | [https://www.doleoceancargo.com/s/tracking-page](https://www.doleoceancargo.com/s/tracking-page?language=en_US) | Active |
| DOCE Service Page | [https://www.doleoceancargo.com/s/service-page](https://www.doleoceancargo.com/s/service-page?language=en_US) | Active |
| DOCE Vessel Fleet | [https://www.doleoceancargo.com/s/vessels](https://www.doleoceancargo.com/s/vessels?language=en_US) | Active |
| DOCE Contact Information | [https://dole.my.site.com/doce2/s/contact-information](https://dole.my.site.com/doce2/s/contact-information?language=en_US) | Active |
| Salesforce Digital Transformation Case Study (Freeway Consulting) | [https://freewayconsulting.com/en/success-stories/dole-salesforce-digital-transformation-freeway/](https://freewayconsulting.com/en/success-stories/dole-salesforce-digital-transformation-freeway/) | Active |
| Panjiva SCAC Profile (DOLQ) | [https://panjiva.com/scac_profiles/profile/DOLQ](https://panjiva.com/scac_profiles/profile/DOLQ) | Active |
| SeaDex Carrier Profile | [https://seadex.safecube.ai/en/carriers/dole-ocean-cargo-express](https://seadex.safecube.ai/en/carriers/dole-ocean-cargo-express) | Active |
| SeaRates Tracking Page | [https://www.searates.com/sealine/dole_ocean_cargo_express](https://www.searates.com/sealine/dole_ocean_cargo_express) | Active |
| Visiwise B/L Tracking | [https://www.visiwise.co/tracking/bl/dole/](https://www.visiwise.co/tracking/bl/dole/) | Active |
| Reefership Marine Services | [https://www.dole-reefership.com](https://www.dole-reefership.com/) | Active |
| PayCargo (DOCE payments) | [https://paycargo.com/vendors/dole-ocean-express/](https://paycargo.com/vendors/dole-ocean-express/) | Active |
| Dole Food Company (parent) | [https://www.dole.com](https://www.dole.com) | Active |
| DCSA Member List | [https://dcsa.org/about-us/](https://dcsa.org/about-us/) | DOCE NOT listed as member |
| Vizion Supported Carriers | [https://docs.vizionapi.com/docs/supported-carriers](https://docs.vizionapi.com/docs/supported-carriers) | DOCE NOT listed |
| Terminal49 Shipping Lines | [https://terminal49.com/shipping-lines](https://terminal49.com/shipping-lines) | DOCE NOT listed |
