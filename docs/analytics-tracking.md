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

## Implementation status

The GA4 property and web stream have been created. At the time of setup, GA4 reported **no data received**. Creating a stream alone does not install tracking on the site.

### Planned work (not yet verified as implemented)

1. Install the Google tag using measurement ID `G-GDG2KHST09` on the BCBG website. Avoid duplicate page-view events.
2. Track meaningful service-request CTA clicks, with consistent event names and source/context parameters.
3. Preserve Facebook/Instagram campaign attribution (UTM parameters and applicable `fbclid`) through the transition from the BCBG site to the PedalFish service-request flow; define a fallback for lost campaign parameters.
4. Track **completed** service requests in PedalFish, distinctly from button clicks and form starts. Coordinate across the website and PedalFish repositories.
5. Configure the completed-request event as a GA4 key event after validating event receipt.
6. Validate with GA4 Realtime/DebugView and a controlled test request, confirming attribution and no duplicate conversions.
7. Review consent/privacy requirements; do not send customer names, email addresses, phone numbers, or other personally identifiable information in analytics events.

## Operational notes

- A GA4 Measurement ID is a public configuration identifier, **not an API secret**.
- Cross-domain tracking between the marketing site and PedalFish needs deliberate design and testing; merely adding the same tag does not guarantee correct attribution.
- No paid Google Analytics subscription is required for this initial setup.
- This document records configuration and the implementation plan; it does **not** claim code changes or deployment have occurred.
