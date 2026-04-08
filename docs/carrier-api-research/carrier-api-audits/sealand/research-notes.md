# SeaLand (A Maersk Company) -- Research Notes

> **Researched**: 2026-02-17
> **SCAC**: SEJJ (Europe), SEAU (Americas), MCPU (Asia)
> **Key finding**: SeaLand brand was retired in December 2023. All SeaLand operations are now fully integrated into Maersk. SeaLand shipments are tracked through Maersk's APIs at developer.maersk.com.

---

## 1. Developer Portal & API Documentation

SeaLand does **not** have its own developer portal or API infrastructure. As a Maersk subsidiary that was fully absorbed into the Maersk brand in December 2023, all API access is through Maersk's developer portal.

- **Developer portal**: https://developer.maersk.com (Maersk's unified portal)
- **API documentation**: Available at developer.maersk.com (SPA, requires JavaScript rendering)
- **Documentation quality**: Excellent (inherits Maersk's comprehensive DCSA-aligned docs)
- **OpenAPI/Swagger spec**: Yes, via DCSA standard specs and Maersk's interactive docs
- **Brand-specific API behavior**: Maersk APIs accept a `brandScac` parameter in some endpoints (e.g., Product Offers API). Known SeaLand SCAC codes:
  - `SEJJ` -- SeaLand Europe
  - `SEAU` -- SeaLand Americas
  - `MCPU` -- SeaLand Asia
- **Brand retirement timeline**:
  - January 2023: Maersk announced retirement of SeaLand, Hamburg Sud, and other acquired brands
  - October 1, 2023: All new bookings directed to Maersk.com
  - October 15, 2023: SeaLand mobile app closed
  - December 2023: SeaLand brand ceased to exist
  - sealandmaersk.com gradually migrated to maersk.com (redirect page at https://www.maersk.com/sealand)

**Source**: https://www.maersk.com/sealand, https://www.maersk.com/news/articles/2023/01/27/a-unified-maersk-brand

### Implication for SDK

Legacy SeaLand booking and container numbers may still exist in carrier systems and need to be trackable via the Maersk API. The SDK adapter for SeaLand should be a thin alias/wrapper around the Maersk adapter, potentially passing the appropriate `brandScac` for legacy lookups.

---

## 2. DCSA Compliance

SeaLand is not separately listed as a DCSA member. However, as a fully integrated part of Maersk (a DCSA founding member), SeaLand shipments inherit Maersk's full DCSA compliance:

- **DCSA TNT**: v2 and v3 (via Maersk endpoints)
- **DCSA Booking**: v2 (via Maersk endpoints)
- **DCSA Commercial Schedules**: v1 (via Maersk endpoints)
- **Known deviations**: Same as Maersk (none documented publicly)

**Source**: DCSA member list at https://dcsa.org (SeaLand not listed separately; Maersk listed as founding member)

---

## 3. Authentication & Access Requirements

Identical to Maersk:

- **Auth mechanism**: Dual -- OAuth2 Client Credentials (for `/synergy/` and `/v1/` paths) + API Key (Consumer-Key header for `/track-and-trace/` and `/schedules/` paths)
- **Registration**: Free self-service at https://developer.maersk.com
- **Partner program required?**: No for basic API access
- **Credential type**: Consumer-Key (API Key) for most endpoints; Client ID + Client Secret for OAuth2 endpoints
- **EDI note**: developer.maersk.com/support/getting-started-edi mentions that users registered with "any Sealand -- A Maersk Company region" need separate Developer Portal credentials

**Source**: https://developer.maersk.com, https://developer.maersk.com/support/getting-started-edi

---

## 4. Tracking / Shipment Visibility Endpoints

All SeaLand tracking is done through Maersk's API endpoints. The same endpoints documented in the Maersk API inventory apply:

### Track & Trace (Events)
- `GET /track-and-trace/v3/events` -- DCSA TNT v3 events (Equipment + Transport)
- `GET /synergy/tracking/v2/events` -- DCSA TNT v2 events
- `POST /track-and-trace/v3/event-subscriptions` -- Webhook subscriptions

### Schedules
- `GET /schedules/v1/vessel-schedules` -- Vessel schedules
- `GET /schedules/v1/port-schedules` -- Port schedules
- `GET /schedules/v1/point-to-point-routes` -- Route options

### Booking
- Booking endpoints exist (exact path prefix may differ from DCSA spec default)

### Lookup Methods
- Bill of Lading number
- Booking reference
- Container number
- Vessel IMO / voyage

**Key question**: Whether legacy SeaLand B/L numbers (prefixed with SEAU, SEJJ, or MCPU) are automatically resolved by Maersk's tracking API, or whether a specific `carrierCode` or `brandScac` parameter is needed. This requires live testing to confirm.

---

## 5. Alternative / Non-API Access Methods

### Web Portal Tracking
- **URL**: https://www.maersk.com/tracking/ (SeaLand tracking now redirects here)
- **Login required?**: No for basic container/B/L tracking
- **Legacy portal**: sealandmaersk.com (gradually being closed; redirects to maersk.com/sealand)

### EDI
- **Supported**: Yes (inherited from Maersk)
- **Message types**: IFTMIN, IFTSTA, COPARN, BAPLIE
- **Connection**: Via Maersk's EDI infrastructure
- **Documentation**: https://developer.maersk.com/support/getting-started-edi

### Third-Party Aggregators

| Aggregator | Available? | Notes |
|-----------|-----------|-------|
| project44 | Yes (via Maersk) | Maersk is a major project44 carrier |
| FourKites | Yes (via Maersk) | Supported through Maersk integration |
| Vizion | Yes | Vizion explicitly lists SeaLand with SCAC SEAU; provides container tracking |
| INTTRA / E2open | Yes | Maersk/SeaLand available on INTTRA platform; direct bookings and spot rates |
| CargoSmart | Yes (via Maersk) | Maersk supported |
| Portcast | Yes | Explicitly supports "Sealand Maersk" container tracking |
| Beacon | Yes | Lists SeaLand as supported carrier |
| ShipsGo | Yes | Provides SEALAND tracking API |
| Terminal49 | Yes | Lists "Sealand Americas (SEAU)" as supported carrier |

**Sources**: https://www.vizionapi.com/carrier-tracking/sealand, https://www.portcast.io/carrier-coverage/sealand-maersk-container-tracking, https://shipsgo.com/ocean/carriers/sealand/container-tracking, https://terminal49.com/shipping-lines/seau-sealand-americas-container-tracking/

---

## 6. Community & Third-Party Resources

- No SeaLand-specific API libraries found on GitHub, npm, or PyPI
- No separate developer community -- all development occurs against Maersk APIs
- Third-party aggregators (listed above) are the primary way external developers track SeaLand containers
- Multiple container tracking aggregator websites support SeaLand lookups using SEAU SCAC code

---

## Key Findings Summary

1. **SeaLand has no independent API** -- it is fully integrated into Maersk's API infrastructure as of December 2023
2. **All 30 required fields are accessible** through Maersk's APIs (same coverage as the Maersk inventory)
3. **SCAC codes still active**: Despite brand retirement, SEJJ/SEAU/MCPU SCAC codes remain in use for legacy tracking at aggregators
4. **SDK approach**: The SeaLand adapter should be a thin alias pointing to the Maersk adapter, with SCAC code mapping for legacy references
5. **Third-party aggregators widely support SeaLand** tracking, typically using SEAU as the carrier code
6. **DCSA compliance inherited** from Maersk (founding member) -- TNT v3, Booking v2, CS v1

```json
{
  "carrierName": "SeaLand (A Maersk Company)",
  "scac": "SEJJ",
  "researchNotesPath": "docs/carriers/sealand/research-notes.md",
  "hasApi": true,
  "isDcsaCompliant": true,
  "dcsaVersion": "TNT v3, BKG v2, CS v1 (via Maersk)",
  "estimatedFieldCoverage": "high",
  "keyFindings": [
    "SeaLand brand retired December 2023; fully integrated into Maersk",
    "All APIs accessed through developer.maersk.com (Maersk's unified portal)",
    "DCSA compliance inherited from Maersk (founding member)",
    "Multiple SCAC codes: SEJJ (Europe), SEAU (Americas), MCPU (Asia)",
    "Third-party aggregators widely support SeaLand tracking via SEAU"
  ],
  "blockers": [
    "Need to verify whether legacy SeaLand B/L numbers work directly in Maersk API without special parameters"
  ]
}
```
