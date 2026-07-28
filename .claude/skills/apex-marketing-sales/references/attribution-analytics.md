# Attribution Analytics

## Scope
Measuring which marketing efforts drive revenue: multi-touch attribution, cohort analysis, marketing mix modeling, and preventing common attribution pitfalls.

## Core principles
- Last-click attribution (giving all credit to the last touchpoint) is simple but biased; a prospect researches for 2 months (organic search, blog, webinar) then closes after a demo — giving all credit to the demo is wrong.
- Multi-touch attribution (splitting credit across touchpoints) is more accurate but has choice: time-decay (later touches count more), position-based (first and last touch count more), or algorithmic (ML-driven credit).
- Attribution window (how far back to count touchpoints) matters; if you use 30-day attribution and a prospect's customer journey is 90 days, you miss the early influence.
- Marketing ROI is only as good as the attribution model; wrong model = wrong decisions (defund high-impact channels, overfund low-impact ones).
- Cohort analysis (tracking a group of customers acquired via one channel through their lifetime) is more reliable than aggregate attribution (easier to interpret, more stable).

## Apex practices
- Start simple: last-click attribution is better than no attribution; algorithmic models are not required at $1M ARR.
- Measure cohort LTV by acquisition channel (what's the lifetime value of a customer acquired via paid search vs. organic vs. partnership?); this drives where to allocate budget.
- Use incrementality testing (holdout groups who don't see ads and see normal results, vs. treatment group who see ads) to measure true lift from campaigns; observed correlation isn't causation.
- Build a marketing dashboard (CAC by channel, payback period by channel, LTV by acquisition cohort, MRR contribution by channel) and review monthly; this drives allocation decisions.

## Pitfalls
- Attributing organic/social success to paid efforts (drove awareness which drove organic search, but paid gets all the credit).
- Using short attribution windows (7-day attribution) when sales cycles are 60+ days; you'll underestimate organic's impact.
- Confusing "leads generated" with "revenue influenced"; leads don't equal customers, and attribution should track to revenue, not lead count.

## Tools & references
Looker, Amplitude (cohort analysis), HubSpot's attribution, Google Analytics 4 (multi-touch attribution), Reforge measurement course, MMM (marketing mix modeling — advanced).
