# Survivorship Bias

## Scope
Drawing conclusions from the visible survivors while the failures — silent, deleted, churned, dead — hold the actual lesson.

## Core principles
- Wald's bombers are the template: armor where returning planes AREN'T hit, because planes hit there didn't return — the missing data is the message, and it is always missing for a reason.
- Success literature is a survivor gallery: studying ten unicorns' shared habits ignores the thousand dead companies with identical habits; without the denominator, "what winners do" is astrology.
- In engineering: error logs show errors that got logged; support tickets show users who bothered; benchmarks show configurations someone published — each observable is filtered by a survival mechanism you must name before trusting the sample.
- Churned users are the invisible fleet: feedback comes overwhelmingly from engaged survivors, so products iterate toward pleasing who stayed and never learn why the majority left.
- Your own memory survivorship-filters: remembered bets are the interesting ones (big wins, big losses); the boring base rate is forgotten, inflating both confidence and fear.

## Detection tests
- What's the denominator? (Selected from how many? Who's not in this dataset and why?)
- What filter did an item pass to become visible to me right now?
- Am I studying successes without a matched sample of failures?

## Countermeasures
- Hunt the missing data on purpose: exit interviews, failed-project retros, silent-user sampling, dead-competitor analysis.
- Instrument the non-event: log the request that didn't retry, the user who didn't click, the crash that didn't report.
- When citing exemplars ("X company does this"), require at least one counterexample check: who did the same and failed?

## Tools & references
Wald's memo, "Fooled by Randomness" (Taleb), funnel/cohort analytics that include the drop-offs, failure-case post-mortem libraries.
