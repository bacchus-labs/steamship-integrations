# ZIM Integrated Shipping Services -- Research Notes

**Researched**: 2026-02-17
**SCAC**: ZIMU

---

## 1. Developer Portal & API Documentation

ZIM operates a developer portal at **https://api.zim.com/** built on Microsoft Azure API Management. The portal allows developers to discover APIs, try them interactively, and sign up for API keys.

- **Portal URL**: https://api.zim.com/
- **Portal accessibility**: Requires registration to view full API documentation. The portal landing page is publicly visible but API specs and product details are behind authentication.
- **Documentation quality**: Limited public documentation. The portal itself is not crawlable; detailed endpoint specs require login. No publicly accessible Swagger/OpenAPI specifications were found.
- **Secondary documentation site**: https://docs.zimconnections.com/ -- appears to host Redoc-based API documentation but returned only CSS/styling content when fetched (no actual API specs loaded). The underlying OpenAPI spec file URL was not discoverable.
- **API Support page**: https://www.zim.com/contact-us/zim-api-support
- **API Terms**: https://www.zim.com/help/api-terms-and-conditions -- covers EULA for API access, token usage restrictions, and revocation policies.

### Key findings from API Terms:
- Organizations must apply for and obtain a security token ("API Token")
- Usage is limited by calls per minute or per day as stated during registration
- API tokens cannot be shared with third parties unless the third party is a pre-approved service provider
- Tokens can be revoked if license term expires or terms are breached

### OpenAPI/Swagger
No publicly accessible OpenAPI/Swagger specification files were found for ZIM's APIs.

---

## 2. DCSA Compliance

ZIM is a **founding member** of the Digital Container Shipping Association (DCSA), established in April 2019 alongside MSC, Maersk, CMA CGM, Hapag-Lloyd, ONE, Evergreen, Yang Ming, and HMM.

- **DCSA member**: Yes (founding member)
- **DCSA Track & Trace adoption**: ZIM is listed among the nine carriers that adopted the DCSA T&T standards. As of April 2021, the DCSA reported that "Five members now have the API in production or testing; all expect to soon be providing shippers access." It is not publicly specified whether ZIM was among the five with production/testing APIs at that time.
- **DCSA TNT version**: Not confirmed publicly. DCSA has published v2.2 and v3.0 of the TNT standard. ZIM's specific implemented version is unknown from public sources.
- **DCSA Booking / Schedules / eDocumentation**: No public evidence of DCSA-standard Booking, Commercial Schedules, or eDocumentation API implementations.
- **Known deviations**: None documented publicly.

**Sources**:
- https://splash247.com/top-carriers-adopting-dcsa-track-and-trace-standards/
- https://dcsa.org/resource/dcsa-track-trace-standards-adopted-member-carriers/

---

## 3. Authentication & Access Requirements

- **Auth mechanism**: API Token (security token obtained through registration on api.zim.com). The Azure API Management platform typically supports subscription keys (passed as headers). OAuth2 may also be supported given the platform, but not confirmed from public sources.
- **Registration**: Organizations must apply and be approved. This appears to require a business relationship or at minimum a customer account with ZIM.
- **Self-service**: Unclear. The portal allows signup at https://api.zim.com/profile but the approval process and timelines are not publicly documented.
- **Access tiers**: Rate limits (calls per minute/day) are defined during registration. Specific tier details are not publicly available.
- **IP whitelisting**: Unknown
- **Sandbox**: Unknown -- no public mention of a sandbox or test environment.

---

## 4. Tracking / Shipment Visibility

### Web Portal Tracking
- **URL**: https://www.zim.com/tools/track-a-shipment
- **Login required**: No -- public tracking available
- **Lookup methods**: Container number, B/L number, Booking number
- **B/L format**: ZIM B/L numbers use prefix "ZIMU" followed by 8-12 alphanumeric characters

### API Tracking
ZIM's API portal (api.zim.com) provides tracking capabilities, but specific endpoint paths, methods, parameters, and response formats are not publicly documented outside the authenticated portal.

The secondary documentation site (docs.zimconnections.com) appears to contain API documentation built with Redoc but the actual OpenAPI specification was not accessible during research.

### US Inland Tracing
ZIM provides a dedicated **US Inland Tracing Status** tool at https://www.zim.com/tools/us-inland-tracing-status for tracking inland US movements.

---

## 5. Schedules

ZIM provides a public schedules tool at https://www.zim.com/schedules with search by:
- Point-to-point
- Port
- Vessel
- Line (service)

Whether this is exposed via the API at api.zim.com is not confirmed from public sources, but given the platform capabilities (booking, tracking, schedules are typical), it is likely available.

---

## 6. Booking & Shipping Instructions

ZIM's **myZIM** platform (https://www.zim.com/digital-solutions/myzim-personal-area) provides:
- Booking creation and management
- Shipping instruction submission for confirmed bookings
- Bill of Lading approval and editing
- Commodity code lookup
- Document management (import/export documents, booking confirmations, arrival notices, delivery orders)
- 24/7 access to view and print original Bills of Lading

The **eZIM** platform was closed at end of December 2025 -- booking and shipping instructions migrated to myZIM.

Whether booking/SI is available via the API (api.zim.com) is not confirmed publicly, but given the platform and modern API approach, it is plausible.

---

## 7. Non-API Access Methods

### EDI (Electronic Data Interchange)
ZIM supports bilateral EDI (directly connected EDI) as listed on their eCommerce partners page.
- **Source**: https://www.zim.com/tools/ecommerce-partners
- **EDI message types**: Not specified publicly, but as a major carrier, likely supports standard types (IFTMIN, COPARN, IFTSTA, BAPLIE, VERMAS)

### eCommerce Partner Portals
ZIM works with the following portal partners for booking and supply chain management:
- **INTTRA** (now part of e2open)
- **Infor Nexus** (formerly GT Nexus)
- **CargoSmart**
- **ENP**
- **Logwing**

ZIM is explicitly listed as an INTTRA carrier partner.
- ZIM adopted INTTRA's eVGM service: https://www.scmr.com/article/zim_is_latest_ocean_carrier_to_opt_for_inttras_evgm_service/news/news/more

### WAVE BL
ZIM offers WAVE BL service for digital release of original Bills of Lading.

---

## 8. Third-Party Aggregators

| Aggregator | Available? | Evidence |
|-----------|-----------|---------|
| **Vizion** | Yes | ZIMU listed as supported carrier with B/L and Booking tracking. Source: https://docs.vizionapi.com/docs/supported-carriers |
| **project44** | Yes | ZIM included in project44's ocean visibility coverage (98%+ of global ocean freight). Source: https://www.project44.com/platform/visibility/ocean/ |
| **FourKites** | Yes (likely) | FourKites covers 85+ ocean carriers; ZIM is a top-10 carrier. Not explicitly listed in search results but highly likely given coverage claims. |
| **INTTRA / E2open** | Yes | ZIM is an INTTRA carrier partner. Source: https://www.zim.com/tools/ecommerce-partners |
| **CargoSmart** | Yes | Listed as ZIM eCommerce partner. Source: https://www.zim.com/tools/ecommerce-partners |

---

## 9. Community & Third-Party Resources

- **GitHub libraries**: No ZIM-specific shipping API wrapper libraries found on GitHub (search results returned ZIM file format libraries, unrelated).
- **npm/PyPI packages**: No ZIM shipping API packages found.
- **Third-party tracking APIs**: Several third-party services provide ZIM tracking aggregation:
  - TrackingMore: https://www.trackingmore.com/zim-tracking-api
  - JSONCargo: https://jsoncargo.com/zim-container-tracking-api/
  - ShipsGo: https://shipsgo.com/ocean/carriers/zim/container-tracking
  - Terminal49: https://terminal49.com/container-tracking-api
- **Reddit/forums**: No developer discussions about ZIM's API found.

---

## 10. Recent Corporate Development

**Hapag-Lloyd acquisition announced 2026-02-17**: Hapag-Lloyd signed an agreement to acquire 100% of ZIM shares at $35/share (~$4.2 billion total). Regulatory approvals expected by late 2026. Until closing, both companies remain independent competitors.

This acquisition could significantly impact ZIM's API strategy long-term:
- Hapag-Lloyd has its own well-documented API portal at https://api-portal.hlag.com
- Post-acquisition, ZIM's APIs may migrate to or integrate with Hapag-Lloyd's platform
- For SSL's purposes, ZIM's current APIs remain operational until merger completion

---

## Summary

```json
{
  "carrierName": "ZIM Integrated Shipping Services",
  "scac": "ZIMU",
  "researchNotesPath": "docs/carriers/zim/research-notes.md",
  "hasApi": true,
  "isDcsaCompliant": true,
  "dcsaVersion": "Unknown (likely v2.2 based on DCSA membership)",
  "estimatedFieldCoverage": "medium",
  "keyFindings": [
    "ZIM has an API portal at api.zim.com (Azure API Management) with tracking capabilities",
    "DCSA founding member, adopted T&T standards, specific version not publicly confirmed",
    "API documentation is behind authentication -- no public Swagger/OpenAPI specs",
    "Strong aggregator coverage: Vizion, project44, INTTRA, CargoSmart all support ZIM",
    "EDI and eCommerce partner integrations available",
    "Hapag-Lloyd acquisition announced Feb 2026 -- long-term API strategy may change"
  ],
  "blockers": [
    "Cannot determine exact API endpoints, response shapes, or rate limits without portal access",
    "DCSA TNT version not publicly confirmed",
    "Webhook/subscription support not confirmed from public sources"
  ]
}
```
