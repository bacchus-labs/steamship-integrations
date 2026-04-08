# Safmarine -- Research Notes

> **Carrier**: Safmarine (SCAC: SAFM)
> **Researched**: 2026-02-17
> **Researcher**: Agent (carrier API audit workflow)

---

## 1. Developer Portal & API Documentation

Safmarine does **not** have its own developer portal or API documentation. Safmarine was fully integrated into Maersk Line in 2020 (announced September 2020, completed by end of 2020). The Safmarine brand was retired as an independent entity.

- **No standalone Safmarine API exists.** All programmatic access goes through Maersk's developer portal at [developer.maersk.com](https://developer.maersk.com).
- The Maersk developer portal does not explicitly list Safmarine/SAFM as a supported `brandScac` value in its public documentation, though it does list `maeu` (Maersk Line), `mcpu` (Sealand Asia), `seau` (Sealand Americas), and `sejj` (Sealand Europe).
- The maersk.com/safmarine page confirms: "To track your cargo you can continue to use Safmarine Track and Trace for now" and that booking migrated to Maersk.com by end of 2020.
- Sources: [maersk.com/safmarine](https://www.maersk.com/safmarine), [developer.maersk.com](https://developer.maersk.com)

## 2. DCSA Compliance

Safmarine itself is **not** a DCSA member -- the nine founding members are MSC, Maersk, CMA CGM, Hapag-Lloyd, ONE, Evergreen, Yang Ming, HMM, and ZIM. However, since Safmarine shipments are managed through Maersk's infrastructure, they are de facto served by Maersk's DCSA-compliant APIs (TNT v2/v3, BKG v2, CS v1).

- DCSA compliance is inherited through the Maersk parent, not through Safmarine directly.
- Source: [dcsa.org](https://dcsa.org/)

## 3. Authentication & Access Requirements

Since Safmarine operates through Maersk's API infrastructure:

- **Auth mechanism**: Same as Maersk -- dual OAuth2 + API Key pattern
- **Registration**: Free self-service at developer.maersk.com
- **Key question**: Whether legacy Safmarine B/L numbers (prefixed SAFM) can be queried through the Maersk tracking API. The Maersk API documentation does not explicitly address this, though third-party aggregators (Terminal49, Vizion) successfully track Safmarine containers, suggesting the data flows through Maersk's backend.

## 4. Tracking / Shipment Visibility Endpoints

No separate Safmarine endpoints exist. All tracking goes through Maersk's APIs:

- **Track & Trace**: `api.maersk.com/track-and-trace/v3/events` and `api.maersk.com/synergy/tracking/v2/events`
- **Schedules**: `api.maersk.com/schedules/v1/vessel-schedules`, `port-schedules`, `point-to-point-routes`
- **Booking**: `api.maersk.com/booking` (DCSA Booking v2)

The Maersk Offers API uses a `brandScac` parameter. Known values include `maeu`, `mcpu`, `seau`, `sejj`. Whether `safm` is accepted is **unverified** -- the documentation placeholder says "bla bla about brands and add section somewhere to list supported brands" indicating incomplete docs.

## 5. Alternative / Non-API Access Methods

### Web Portal
- **maersk.com/tracking**: Can track Safmarine shipments using container numbers and B/L numbers (Safmarine credentials work on maersk.com login).
- **safmarine.com**: Redirects to maersk.com/safmarine. Legacy Safmarine Track and Trace was maintained during transition but has been deprecated in favor of maersk.com.

### EDI
- Safmarine historically supported EDI (IFTMIN, IFTSTA, COPARN, BAPLIE) through Maersk's EDI infrastructure. Post-integration, EDI is handled through Maersk's EDI services at [developer.maersk.com/support/getting-started-edi](https://developer.maersk.com/support/getting-started-edi).

### Third-Party Aggregators
- **Vizion**: Lists Safmarine as supported ([vizionapi.com/carrier-tracking/safmarine](https://www.vizionapi.com/carrier-tracking/safmarine)). Tracks via container, booking, and B/L numbers.
- **Terminal49**: Lists Safmarine (SAFM) as supported ([terminal49.com/shipping-lines/safm](https://terminal49.com/shipping-lines/safm-safmarine-container-line-container-tracking)). Supports B/L and booking tracking; container number tracking listed as unsupported.
- **project44**: Safmarine not explicitly found in their public carrier appendix, but project44 covers 98%+ of global ocean freight.
- **Portcast**: Lists Safmarine tracking ([portcast.io](https://www.portcast.io/carrier-coverage/safmarine-container-line-tracking)).
- **INTTRA / E2open**: Maersk (including former Safmarine operations) available through INTTRA.
- **CargoSmart**: No specific Safmarine listing found, but Maersk shipments available.

## 6. Community & Third-Party Resources

- No GitHub libraries, npm packages, or PyPI packages specific to Safmarine API integration.
- No developer forums or discussions specific to Safmarine API access.
- All developer resources point to the Maersk developer portal.

## Key Findings

1. **Safmarine is fully absorbed into Maersk** -- the brand was retired in 2020 and all operations run through Maersk's infrastructure.
2. **No separate Safmarine API exists** -- all access is via Maersk's developer.maersk.com APIs.
3. **SAFM SCAC code persists** in industry systems and aggregator platforms, but the underlying data comes from Maersk.
4. **Maersk's full DCSA suite is available** for Safmarine shipments by inheritance.
5. **The SDK adapter for Safmarine should be a thin alias/configuration layer on top of the Maersk adapter**, potentially with `brandScac=safm` if that value is accepted, or simply using the Maersk adapter directly with Safmarine B/L/container numbers.
6. **Unverified**: Whether `safm` is a valid `brandScac` value in the Maersk API. This must be tested with live credentials.
