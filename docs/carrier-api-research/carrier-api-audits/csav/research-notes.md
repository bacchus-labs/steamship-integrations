# CSAV (Compania Sudamericana de Vapores) -- Research Notes

> **Researched**: 2026-02-17
> **Researched by**: agent (audit/csav)

---

## Key Finding: CSAV No Longer Operates Container Shipping Directly

CSAV merged its container shipping operations into Hapag-Lloyd in December 2014. By July 2020, CSAV closed its last directly operated services. Today, CSAV is an investment holding company whose primary asset is a ~30% equity stake in Hapag-Lloyd AG. CSAV does not operate vessels, does not issue bills of lading under its own name for new shipments, and does not maintain any shipping API infrastructure.

**All container shipping operations, digital systems, and APIs are provided by Hapag-Lloyd.**

Sources:
- https://www.csav.com/our-business/ -- confirms CSAV "closed its directly operated services" in July 2020, sole business is Hapag-Lloyd investment
- https://www.hapag-lloyd.com/en/press/releases/2014/12/hapag-lloyd-and-csav-complete-the-merger-and-become-the-fourth-l_37308.html -- merger completion press release
- https://www.freightwaves.com/news/hapag-lloyd-csav-complete-merger -- FreightWaves coverage of merger completion

---

## 1. Developer Portal & API Documentation

**CSAV has no developer portal and no API documentation.** CSAV's website (csav.com) is a corporate investor-relations site focused on financial reporting and governance. There are no technical, shipping, or developer resources.

All API infrastructure for container tracking, booking, schedules, and events is provided by Hapag-Lloyd at:
- Developer portal: https://api-portal.hlag.com
- Full API inventory: see `docs/carriers/hapag-lloyd/api-inventory.md`

---

## 2. DCSA Compliance

CSAV is **not** a DCSA member. The nine DCSA founding members are MSC, Maersk, CMA CGM, Hapag-Lloyd, ONE, Evergreen, Yang Ming, HMM, and ZIM.

However, since all CSAV container operations are now under Hapag-Lloyd, and Hapag-Lloyd **is** a DCSA founding member implementing TNT v2.2.4, CS v1.0.1, and OVS v3.0.7, any shipment historically associated with CSAV would be tracked via Hapag-Lloyd's DCSA-compliant APIs.

---

## 3. Authentication & Access Requirements

N/A -- CSAV has no separate API. Access to Hapag-Lloyd APIs requires registration at https://api-portal.hlag.com (free, self-service). See Hapag-Lloyd inventory for details on API Key (X-IBM-Client-Id / X-IBM-Client-Secret) authentication and access tiers (Tryout: 100 calls/day, Default: 6,000 calls/day, Premium: 100,000 calls/day).

---

## 4. Tracking / Shipment Visibility Endpoints

No CSAV-specific endpoints exist. All tracking is through Hapag-Lloyd's API infrastructure.

### Container Prefix Mapping
CSAV containers use prefixes **CSVU** and **LNXU**. These are tracked through Hapag-Lloyd's container tracking system at:
- Web: https://www.hapag-lloyd.com/en/online-business/track/track-by-container-solution.html
- API: Hapag-Lloyd TNT v2.2 API

### SCAC Code
CSAV's historical SCAC code is **CHIW** (sometimes referenced as CSAV Norasia). However, since CSAV no longer operates independently:
- Third-party aggregators map CSAV to Hapag-Lloyd's SCAC **HLCU** (confirmed by Vizion API's carrier mapping)
- Container tracking platforms redirect CSAV tracking requests to Hapag-Lloyd

---

## 5. Alternative / Non-API Access Methods

### Web Portal Tracking
- CSAV has no tracking portal. csav.com is investor-relations only.
- All tracking is done via Hapag-Lloyd: https://www.hapag-lloyd.com/en/online-business/track/track.html

### EDI
CSAV does not offer EDI services. Hapag-Lloyd offers EDI through standard industry channels (INTTRA/E2open).

### Third-Party Aggregators

| Aggregator | CSAV Available? | Notes |
|-----------|----------------|-------|
| **Vizion** | Yes -- mapped to HLCU | Vizion explicitly lists "Compania Sud Americana de Vapores (CSAV)" with carrier code HLCU (Hapag-Lloyd). Source: https://docs.vizionapi.com/docs/supported-carriers |
| **project44** | Likely via Hapag-Lloyd | project44 supports Hapag-Lloyd (HLCU). CSAV shipments would be tracked under HL. |
| **FourKites** | Likely via Hapag-Lloyd | FourKites tracks 85+ ocean carriers including Hapag-Lloyd. CSAV shipments would route through HL. |
| **INTTRA / E2open** | Via Hapag-Lloyd | Hapag-Lloyd is a founding member of INTTRA. CSAV shipments managed through HL's INTTRA integration. |
| **CargoSmart** | Via Hapag-Lloyd | CargoSmart supports Hapag-Lloyd. CSAV/HL integration confirmed by CargoSmart's carrier page showing HL with note about CSAV's 22.6% ownership. |

---

## 6. Community & Third-Party Resources

- No GitHub libraries, npm packages, or PyPI packages exist for CSAV API integration
- No developer forums or community discussions about CSAV APIs (because none exist)
- All developer resources are for Hapag-Lloyd -- see Hapag-Lloyd inventory for community libraries

---

## Summary

CSAV is a pure investment holding company. It has zero shipping API infrastructure. All container operations flow through Hapag-Lloyd. For SSL's purposes:

1. **Do not build a separate CSAV adapter** -- there is nothing to connect to
2. **Use the Hapag-Lloyd adapter** for any CSAV-related tracking
3. **Map CSAV SCAC (CHIW) to HLCU** in the carrier registry so lookups resolve correctly
4. **Container prefixes CSVU and LNXU** are tracked through Hapag-Lloyd's systems

```json
{
  "carrierName": "Compania Sudamericana de Vapores (CSAV)",
  "scac": "CHIW",
  "researchNotesPath": "docs/carriers/csav/research-notes.md",
  "hasApi": false,
  "isDcsaCompliant": false,
  "dcsaVersion": "N/A",
  "estimatedFieldCoverage": "low",
  "keyFindings": [
    "CSAV merged container operations into Hapag-Lloyd in 2014; closed all direct operations by July 2020",
    "CSAV is now a pure investment holding company with ~30% stake in Hapag-Lloyd",
    "No CSAV API, developer portal, or digital shipping infrastructure exists",
    "All tracking is through Hapag-Lloyd APIs (HLCU)",
    "Third-party aggregators (Vizion, etc.) map CSAV to HLCU",
    "Container prefixes CSVU and LNXU are tracked via Hapag-Lloyd"
  ],
  "blockers": [
    "No independent API exists -- CSAV adapter would simply be an alias to Hapag-Lloyd"
  ]
}
```
