# Martech

## Scope
Marketing technology: audience data, segmentation, campaign management, personalization, and attribution.

## Core principles
- First-party data (owned by your company: emails, purchase history, behavior) is valuable; third-party data (broker-bought demographics) is degraded, regulated (GDPR kills third-party cookies), and expensive.
- Segmentation is targeting: dividing audience by characteristics (demographics, behavior, purchase intent) and tailoring messaging; broad campaigns fail, targeted campaigns convert.
- Attribution (which touchpoint drove conversion) is unsolvable perfectly: a customer sees 7 ads before buying; which caused the purchase? Last-click attributes to the final ad, but other models (first-touch, multi-touch) tell different stories.
- Personalization requires real-time data: serving the right message to the right person requires millisecond-latency audience profiles; batch personalization (overnight emails) is slow.
- Privacy regulations (GDPR, CCPA, iOS ATT) restrict data use; consent is mandatory; trackability across sites is dying; first-party data and contextual targeting (ad context matches user interest) replace behavioral tracking.

## Apex practices
- Implement a CDP (Customer Data Platform): unify data from web, email, ads, CRM into a single customer view, enabling segmentation and personalization.
- Use attribution modeling (multi-touch, probabilistic) rather than last-click; understand that different channels have different roles (awareness, consideration, conversion).
- Build personalization engines that respect privacy: segment based on first-party data and behavior within your properties; avoid creepy cross-site tracking.
- Measure incrementality (did the ad change behavior?) via holdout tests; observational correlation is misleading.

## Pitfalls
- Assuming correlation is causation; seeing a correlation between email open and purchase doesn't mean the email caused it (confounding: engaged customers both open email and buy).
- Ignoring consent; GDPR and CCPA require explicit opt-in for data collection and personalization; "we've always done this" doesn't exempt you from new regulations.
- Over-personalizing; serving ads that are too specific reads as creepy and kills trust.

## Tools & references
CDP platforms (Segment, Tealium, mParticle), marketing automation (HubSpot, Marketo, Pardot), analytics (Google Analytics, Mixpanel, Amplitude), attribution (Northbeam, Littledata), privacy frameworks (GDPR, CCPA).
