# ANL Container Line -- Research Notes

> **Researched**: 2026-02-17
> **Researched by**: Agent

---

## 1. Developer Portal & API Documentation

ANL does not maintain a separate developer portal or API infrastructure. ANL shipments are tracked and managed through **CMA CGM's API portal** at https://api-portal.cma-cgm.com.

ANL's own website (https://www.anl.com.au/products-services/ecommerce/edi-api-channels) describes its EDI/API solutions as: "APIs work as a plug and play service allowing information systems, yours and CMA CGM Group's, to communicate easily. Systems talk to each other and data is exchanged in real-time."

The CMA CGM API portal explicitly states that its APIs cover "all carriers of the CMA CGM group" -- this includes CMA CGM (CMDU), APL (APLU), ANL (ANNU), and CNC.

**Key finding**: ANL has no independent API. All programmatic access goes through CMA CGM's API portal. The CMA CGM API inventory at `docs/carriers/cma-cgm/api-inventory.md` is the authoritative reference for ANL API capabilities.

### Documentation Quality
Same as CMA CGM: Good -- DCSA-standard APIs have detailed descriptions, event tables, and Swagger tabs; proprietary APIs have briefer descriptions.

---

## 2. DCSA Compliance

ANL itself is not a DCSA member -- CMA CGM (the parent) is a founding DCSA member (April 2019). ANL shipments tracked through CMA CGM's DCSA-compliant Track & Trace API (TNT v2.2.0) receive the same DCSA-standard event data as CMA CGM-branded shipments.

DCSA APIs available for ANL shipments (via CMA CGM portal):
- **Track & Trace (TNT)**: v2.2.0 (DCSA Information Model v3.3)
- **Commercial Schedules (CS)**: v1.0.7 (PILOT status)

Same deviations as CMA CGM: shipment events and DCSA subscription management endpoints are NOT implemented.

---

## 3. Authentication & Access Requirements

Identical to CMA CGM:
- **Public APIs**: API Key (header: `KeyId: <API_Key_Value>`)
- **Private APIs**: OAuth2 Client Credentials (endpoint: `https://auth.cma-cgm.com/as/token.oauth2`, token lifetime: 299 seconds)
- **Registration**: https://api-portal.cma-cgm.com -- requires approval (2-3 days for public, ~1 week for private)
- **Free trial**: 1 month production access
- **Private API access**: Requires being identified on booking as Booking Party, Deciding Party, Consignee, Notifier, or Shipper

---

## 4. Tracking / Shipment Visibility Endpoints

All CMA CGM tracking endpoints work for ANL shipments. The Track & Trace API returns events for any CMA CGM group carrier including ANL. Key endpoints:

- `GET /events` (DCSA TNT v2.2.0) -- equipment and transport events
- Schedules APIs (DCSA CS v1 PILOT + proprietary Routing Finder, Voyages, Lines & Services)
- Shipment API (proprietary) -- booking status and details
- Booking Request API (proprietary) -- booking lifecycle
- Shipping Instruction API (proprietary) -- SI management

All lookup methods supported: B/L number, booking reference, container number, vessel IMO/voyage.

---

## 5. Alternative / Non-API Access Methods

### Web Portal
- **ANL tracking URL**: https://www.anl.com.au/ebusiness/tracking
- **CMA CGM tracking URL**: https://www.cma-cgm.com/ebusiness/tracking (also works for ANL shipments)
- Login not required for basic tracking

### EDI
Same as CMA CGM: IFTMBF, IFTMIN, IFTSTA, IFTMCS, IFTSAI, VERMAS

### Third-Party Aggregators
- **project44**: Yes -- explicitly lists ANL tracking at https://www.project44.com/tracking/container/anl/
- **FourKites**: Yes (via CMA CGM group)
- **Vizion**: Yes (via CMA CGM group)
- **INTTRA / E2open**: Yes (via CMA CGM group)
- **CargoSmart**: Yes (via CMA CGM group)
- **Terminal49**: Yes (via CMA CGM CMDU SCAC)

---

## 6. Community & Third-Party Resources

No ANL-specific client libraries exist. The Python `tracktrace` library at https://github.com/dhruvkar/tracktrace lists CMA CGM (CMDU) support, which implicitly covers ANL.

---

## Key Findings Summary

1. **ANL is fully operated through CMA CGM's API infrastructure** -- no separate API portal, endpoints, or authentication. ANL's SCAC code is ANNU.
2. **CMA CGM's APIs explicitly cover all group carriers** including ANL. The same endpoints, auth, rate limits, and data quality apply.
3. **DCSA compliance is inherited from CMA CGM** -- TNT v2.2.0, CS v1.0.7 (PILOT).
4. **ANL has its own web portal** for tracking (anl.com.au) but this uses CMA CGM's backend infrastructure.
5. **The CMA CGM API inventory is the authoritative reference** for ANL's API capabilities. The ANL API inventory should reference the CMA CGM inventory rather than duplicate it.

---

## Sources

| Resource | URL |
|----------|-----|
| ANL Website | https://www.anl.com.au |
| ANL EDI/API Solutions | https://www.anl.com.au/products-services/ecommerce/edi-api-channels |
| ANL Tracking Portal | https://www.anl.com.au/ebusiness/tracking |
| CMA CGM API Portal | https://api-portal.cma-cgm.com |
| CMA CGM EDI/API Solutions | https://www.cma-cgm.com/products-services/ecommerce/edi-api-channels |
| CMA CGM Tracking Portal | https://www.cma-cgm.com/ebusiness/tracking |
| project44 ANL Tracking | https://www.project44.com/tracking/container/anl/ |
| Fluent Cargo ANL SCAC | https://www.fluentcargo.com/carriers/scac/ANNU |
| DCSA Members | https://dcsa.org/about-us-our-work-and-what-we-do-dcsa/members/ |
