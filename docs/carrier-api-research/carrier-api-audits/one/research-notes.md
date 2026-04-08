# Ocean Network Express (ONE) — Research Notes

> **Carrier**: Ocean Network Express (ONE)
> **SCAC**: ONEY
> **Researched**: 2026-02-17
> **Purpose**: Intermediate research artifact for API inventory

---

## 1. Developer Portal & API Documentation

### Developer Portal
- **URL**: https://developers.one-line.com/get-started
- **Status**: Exists, publicly accessible landing page, but content loads dynamically (SPA). Registration required to view full API documentation.
- **Pages discovered**:
  - Get Started: https://developers.one-line.com/get-started
  - API Auth: https://developers.one-line.com/api-auth
  - Publish: https://developers.one-line.com/publish
- The portal content could not be fully extracted via web fetch due to SPA rendering (JavaScript-rendered content). The actual API product listings, endpoint documentation, and Swagger specs are behind the dynamic portal.

### Documentation Quality
- **Assessment**: Unknown/Not fully accessible — the portal exists and appears functional but specific API documentation, endpoint references, and OpenAPI specs could not be reviewed without registration.
- No publicly visible Swagger/OpenAPI spec URLs were found.
- No API changelog or release notes page was identified.

### eCommerce Platform
- ONE operates a comprehensive eCommerce platform at https://ecomm.one-line.com
- Features include: Cargo Tracking, Mail Tracking, Rail Tracking Report (North America)
- Tracking supports: Container number, Bill of Lading number, Booking reference
- Login required for full features (upcoming deadlines, alerts); basic cargo tracking available without login
- Recently redesigned for improved usability and mobile responsiveness

---

## 2. DCSA Compliance

### Membership
- **DCSA member**: Yes -- confirmed founding member (one of 9 original carriers that established DCSA in April 2019)
- Source: https://dcsa.org/about-us/members
- DCSA currently has 10 members (PIL added April 2024); ONE is one of the original 9

### DCSA API Implementation
- ONE was reported as "one of the first to offer a Track & Trace API based on DCSA standards" (Source: Splash247 article, DCSA press releases from April 2021)
- As of April 2021, "Five members now have the API in production or testing" — ONE was listed among the 9 members but the specific 5 with production APIs were not named
- **DCSA TNT version**: Unknown — could not determine the specific version (v2.2 or v3) from public sources. Given that ONE has a developer portal and was an early adopter, it is likely at least v2.2 is implemented, but this is unverified.
- **DCSA Booking**: Unknown — not confirmed
- **DCSA Commercial Schedules**: Unknown — not confirmed
- **DCSA eDocumentation**: ONE is adopting DCSA eBL standards through GSBN blockchain partnership (announced 2025). Source: https://smartmaritimenetwork.com/2025/02/25/ocean-network-express-adopts-dcsa-ebl-standards-using-gsbn-blockchain/

### DCSA Standards Commitment
- ONE has committed to 100% eBL adoption by 2030 along with other DCSA members
- ONE is the second DCSA member (after Hapag-Lloyd) to partner with GSBN for eBL
- ONE is one of four major carriers issuing eBLs through GSBN (alongside COSCO, OOCL, and Hapag-Lloyd)

---

## 3. Authentication & Access

- **Developer portal**: https://developers.one-line.com
- **Auth mechanism**: Unknown — could not extract from the SPA-rendered portal. The portal has a dedicated "API Auth" page (https://developers.one-line.com/api-auth) but content was not accessible via web fetch.
- **Registration process**: Appears to require creating an account on the developer portal ("Start by creating an account, seeing our full API")
- **Access tiers**: Unknown
- **Sandbox**: Unknown
- **Partner program**: Unknown whether business relationship is required

---

## 4. Tracking / Shipment Visibility Endpoints

### Known Tracking Capabilities (from eCommerce platform and third-party sources)
- Tracking by: Container number, Bill of Lading number, Booking reference
- Data includes: Current status, estimated time of future events, past events history
- Key milestones reported (from third-party sources): Gate in Full, Loaded at POL, Departure from POL, Arrival at POD, Discharged at POD, Gate out Full
- Real-time shipment status information with recommended "to-do actions"
- Cutoff dates at origin and cargo availability dates at destination are available (from eCommerce platform)
- Dynamic point-to-point schedules and routing options available

### API Endpoints
- Could not enumerate specific REST API endpoints. The developer portal at developers.one-line.com likely documents these, but the SPA-rendered content could not be extracted.
- Given ONE's DCSA membership and early adoption claims, expected endpoints would follow DCSA standards (TNT events, event subscriptions, possibly schedules and booking).

---

## 5. Non-API Access Methods

### Web Portal Tracking
- **URL**: https://ecomm.one-line.com/one-ecom/manage-shipment/cargo-tracking
- Also: https://us.one-line.com/CargoTracking (US-specific)
- **Login**: Not required for basic tracking; login enables additional features (deadlines, alerts)
- **Lookup types**: BL number, Booking number, Container number
- **Mobile app**: Available on Google Play (and presumably App Store)

### EDI (Electronic Data Interchange)
- **Supported**: Yes — comprehensive EDI support
- **Portal**: https://www.one-line.com/en/standard-page/edi-portal
- **Standards**: ANSI and EDIFACT
- **Message types**:
  | Function | ANSI | EDIFACT |
  |----------|------|---------|
  | Booking Requests | 300 | IFTMBF |
  | Booking Confirmation | 301 | IFTMBC |
  | Shipping Instructions | 304 | IFTMIN |
  | Bill of Lading | 310 | IFTMCS |
  | Container Movements | 315 | IFTSTA |
  | Schedules | 323 | IFTSAI |
  | Verified Gross Mass | -- | VERMAS |
  | Functional Acknowledgements | 997 | CONTRL |
  | Application Acknowledgements | 824 | APERAK |
- **Additional formats**: XML, CSV, Flat Files
- **Connection methods**: AS2, FTP, SMTP email
- **Stedi network**: ONE listed on Stedi EDI Network with X12 301 (Confirmation Ocean) and X12 322 (Terminal Operations) transaction sets

### Third-Party Aggregators
- **project44**: Yes — ONE container tracking available (https://www.project44.com/tracking/container/one/)
- **FourKites**: Likely yes — FourKites covers 85+ carriers and ONE is the 6th largest carrier globally. Not explicitly confirmed but highly probable.
- **Vizion**: Yes — ONE explicitly listed as supported carrier (https://www.vizionapi.com/carrier-tracking/ocean-network-express-one). Supports tracking by Container ID, Booking number, BL number.
- **INTTRA / E2open**: Yes — ONE is listed on INTTRA's ocean carrier network (confirmed from carrier network page). Electronic booking, shipping instructions, BL, and tracking available.
- **CargoSmart**: Not explicitly confirmed from research. ONE is a major carrier and likely available but could not verify.

---

## 6. Community & Third-Party Resources

### GitHub / npm / PyPI
- **No community libraries found** for ONE's API specifically. The "Ocean Networks Canada" results are a different organization entirely.
- No npm packages, PyPI packages, or GitHub wrappers for ONE's carrier API were identified.

### Third-Party Tracking Integrators
Multiple third-party services offer ONE tracking:
- JSONCargo: https://jsoncargo.com/ocean-network-express-container-tracking-api/
- Dockflow: https://dockflow.com/container-tracking/one/
- Portcast: https://www.portcast.io/carrier-coverage/ocean-network-express-one-container-tracking
- GoComet: https://www.gocomet.com/online-container-tracking/carriers/one-line
- Beacon: https://www.beacon.com/tracking/container/ocean-network-express
- 17TRACK: https://www.17track.net/en/carriers/one-ocean-network-express
- Shipsgo: https://shipsgo.com/ocean/carriers/one/container-tracking

### Google Cloud Case Study
- ONE uses Google Cloud infrastructure (https://cloud.google.com/customers/one)

---

## Key Findings Summary

1. **ONE has a developer portal** at developers.one-line.com with API documentation, but it is SPA-rendered and content could not be fully extracted without registration.
2. **ONE is a DCSA founding member** and was reported as one of the first carriers to implement DCSA TNT standards.
3. **Specific API version and endpoint details are unknown** without portal access — the exact DCSA version (v2.2 vs v3), authentication mechanism, rate limits, and endpoint paths could not be determined from public sources alone.
4. **Comprehensive EDI support** with both ANSI and EDIFACT standards, covering booking, shipping instructions, BL, container movements, schedules, and VGM.
5. **Available through major aggregators**: project44, Vizion, and INTTRA confirmed; FourKites highly likely.
6. **eCommerce platform** provides web-based tracking with Container, BL, and Booking number lookup.
7. **No community libraries** (GitHub, npm, PyPI) exist for ONE's API.

---

## Blockers and Open Questions

- [ ] What specific API products are available on developers.one-line.com? (requires registration)
- [ ] What DCSA TNT version does ONE implement? (v2.2 or v3)
- [ ] Does ONE implement DCSA Booking and Commercial Schedules APIs?
- [ ] What authentication mechanism is used? (OAuth2, API Key, JWT?)
- [ ] What are the rate limits?
- [ ] Is there a sandbox/test environment?
- [ ] Does ONE support webhooks/event subscriptions?
- [ ] Is the API freely accessible or does it require a business relationship?
