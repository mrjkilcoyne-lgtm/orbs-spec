# Product Analytics

## Scope
Instrumenting and analyzing user behavior in-product: event tracking design, funnels, cohorts, and turning behavioral data into decisions.

## Core principles
- The tracking plan is a product artifact: a governed schema of events and properties (object-action naming like `checkout_completed`, versioned, owned) — analytics quality is decided at instrumentation time; no analysis rescues events that were never fired or mean different things per platform.
- Cohorts are the unit of truth: metrics blended across users who joined last week and three years ago are uninterpretable; cut retention, activation, and revenue by signup cohort (and acquisition channel) or the trend lines lie.
- Funnels measure a hypothesis about a path, not the path: users wander, re-enter, and take days; define the conversion window, the entry event, and whether steps are strictly ordered before comparing two funnel charts.
- Correlation in behavioral data is dense and mostly non-causal: power users do everything more ("users who used feature X retain better" is usually selection, the Facebook "7 friends in 10 days" pattern is a correlate that had to be tested); treat behavioral correlations as hypotheses for experiments.
- Qual explains what quant locates: analytics tells you WHERE users drop (step 3, Android, cohort of March); session replays and interviews tell you WHY — an analysis that ends at the chart is half done.

## Apex practices
- Enforce the tracking plan in CI: typed analytics wrappers or schema validation (Avo, Segment Protocols, Iteratively-style) so renamed or malformed events fail the build, not the quarterly board deck.
- Define activation empirically: find the early behavior that best separates retained from churned cohorts (setup-moment → aha-moment → habit-moment framing), then make that the onboarding target instead of an arbitrary checklist.
- Watch p50 AND p90 usage: median users and power users need different roadmaps; averaged engagement hides both.
- Audit data trust quarterly — event volume anomalies, duplicate events after SDK upgrades, unversioned redefinitions — because the fastest way to kill a data culture is one visibly wrong dashboard.

## Pitfalls
- Track-everything instrumentation: 2,000 unnamed auto-captured events nobody can interpret, resulting in the org paying an Amplitude bill to remain ignorant.
- Dashboard proliferation without questions: metrics reviewed weekly with no decision attached train everyone to nod at charts.
- Comparing funnels across releases while the event definitions silently changed between versions — the "improvement" is a schema migration.

## Tools & references
Amplitude/Mixpanel/PostHog/Heap, Segment + tracking-plan tools (Avo), "Lean Analytics" (Croll & Yoskovitz), Amplitude's "Mastering Retention" playbook, session replay (FullStory/PostHog).
