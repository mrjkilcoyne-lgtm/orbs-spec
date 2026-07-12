# Platform & API Products

## Scope
Products sold as infrastructure: designing, pricing, and scaling developer platforms and APIs that form the backbone of customer systems.

## Core principles
- Developer adoption curves are steeper than consumer curves (activation in hours, network effects from day one), but longer to monetize; platforms succeed on free-to-paid conversion ratio, not free users.
- The API contract is immutable: breaking changes can crash millions of customer deployments; versioning and deprecation governance must be part of the product architecture, not an afterthought.
- Platforms live or die on developer experience: fast signup, good error messages, predictable billing, and documentation that works (executable examples beat prose — every code snippet you ship must run, or developers will stop trusting docs).
- Breadth vs. depth: the API should be narrow and composable (stripe/twilio model) rather than a kitchen sink (salesforce SOAP model); developers choose platforms because they're predictable, not because they do everything.
- Platforms require a two-sided marketplace mindset even in B2B: first-party usage (your team building on the API) validates the abstraction; ecosystem growth (third-party apps) unlocks value exponentially.

## Apex practices
- Release early, ship an SDK in your primary language first, then let the community own ports — Stripe's Ruby SDK shaped adoption in startups more than the REST API.
- Rate-limit with clear, predictable tiers; mystery quota changes crater trust faster than a price increase.
- Run a sandbox environment that's free forever and feature-complete; paid development (staging accounts cost money) kills long-tail adoption.
- Build observability into the platform: status pages, webhooks, operational dashboards, and SLA transparency so customers can debug without support tickets.

## Pitfalls
- Charging per API call without a clear cost model or simulator; customers avoid using the platform at scale if they can't predict the bill.
- Documentation that lives in a wiki while the API drifts; generated docs (OpenAPI, auto-playground) stay current by forcing them to match code.
- Launching a platform before the first-party product is live; if your own team doesn't use the API daily, you're shipping friction.

## Tools & references
OpenAPI specification, Stripe API docs (the exemplar), Twilio developer experience case study, Kong API gateway, Swagger UI, API design guidelines (Zalando's REST API standard).
