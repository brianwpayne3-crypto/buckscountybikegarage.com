# BCBG Analytics and Conversion Tracking

Last updated: 2026-11-10

## Google Analytics 4 configuration

- Property: **Bucks County Bicycle Garage**
- Website: https://buckscountybicyclegarage.com
- Web stream name: **BCBG Website**
- Web stream ID: `16312193579`
- **Measurement ID: `G-GDG2KHST09`**
- Industry category: Sports
- Business size: Small (1–10 employees)
- Currency: USD
- Business objectives: Generate leads; Understand web and/or app traffic
- Enhanced measurement: enabled (including page views, scrolls, outbound clicks)
- Reporting time zone: **Los Angeles / Pacific at setup; change to New York / Eastern** in GA4 Admin.

## Implementation status (November 10, 2026)

- **Marketing site source merged:** PR [#3](https://github.com/brianwpayne3-crypto/buckscountybikegarage.com/pull/3), commit `ee0facc70b3c8c2b42f3e52170814b4321870de8`. Installs the GA4 tag on `index.html`, enables GA4 cross-domain linking, emits `service_request_click` for PedalFish CTAs, and forwards UTM tags. When only `fbclid` exists, labels the source as Facebook social, **not verified paid**, because organic Facebook links can also contain it.
- **PedalFish production deployed:** PR [#600](https://github.com/brianwpayne3-crypto/Bucks-County-Bike-Garage/pull/600), commit `23b899f26786a463277b93fbe737d4df05fe6ee5`. Vercel production deployment `dpl_7z5PiCMgiw3epyrhPoFNHWtBwwQk` is READY. GA4 is loaded only on the public BCBG service request route. The client emits `service_request_submitted` after a successful request API response, with protection against re-sending on a React rerender.
- **Existing persistence unchanged:** PedalFish continues to save campaign metadata in the successful service-request record via `marketingAttribution`.
- **Live analytics receipt not yet verified:** GitHub merge is not proof the public marketing domain has picked up the new HTML. Confirm live source or GA4 Realtime and inspect the request transition before calling the funnel operational end-to-end.
- **No customer PII sent in custom analytics events.** The form stores personal information in PedalFish but does not put it in the GA4 conversion event.

## Remaining verification and account configuration

1. Visit the live marketing site in an ordinary browser after its publish; verify the tag uses `G-GDG2KHST09` and GA4 Realtime shows your page view.
2. Click a `Start a service request` or `Request a Repair` CTA and confirm a `service_request_click` event and a page view on the PedalFish form, with cross-domain session attribution.
3. Submit one controlled test request (remove/label it in operations afterward as appropriate). Check the saved `marketingAttribution` in PedalFish and confirm **one** `service_request_submitted` in GA4 Realtime / DebugView.
4. In GA4 Admin > Events / Key events, mark `service_request_submitted` as a key event after receipt. Do not treat `service_request_click` as the lead conversion.
5. Change reporting time zone from **Los Angeles** to **New York** in GA4 Admin > Property settings.
6. Review website privacy/consent disclosures and any applicable requirements. Avoid importing customer names, emails, phone numbers, or other PII into Analytics.

## Operational notes

- A GA4 Measurement ID is a public configuration identifier, **not an API secret**.
- Cross-domain tracking between the marketing site and PedalFish needs deliberate design and testing; merely adding the same tag does not guarantee correct attribution.
- No paid Google Analytics subscription is required for this initial setup.
- This document records configuration and the implementation plan; it does **not** claim code changes or deployment have occurred.
