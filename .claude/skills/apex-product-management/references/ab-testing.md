# A/B Testing

## Scope
Designing, running, and reading controlled experiments on product changes: statistical hygiene, experiment design, and organizational discipline.

## Core principles
- Decide the hypothesis, primary metric, minimum detectable effect (MDE), and sample size BEFORE launch; peeking at running experiments and stopping at significance inflates false positives severalfold (optional-stopping problem) unless you use sequential methods built for it.
- Power drives everything: detecting a 2% relative lift on a 4% conversion rate needs on the order of hundreds of thousands of users per arm — most teams' "losers" are actually underpowered inconclusive tests, which is a different fact.
- Randomization unit must match the analysis unit and the exposure: user-level randomization with session-level analysis violates independence and fabricates significance; network effects (marketplaces, social) may need cluster or switchback designs.
- One primary metric per experiment, declared in advance; testing 20 metrics at α=0.05 yields ~1 false winner by chance — secondary metrics are for context and guardrails, not for shopping.
- Most experiments lose or do nothing: Microsoft/Bing report only ~1/3 of ideas improve metrics (Kohavi); an experimentation program that reports 80% winners has a measurement problem, not a genius PM.

## Apex practices
- Run A/A tests and sample-ratio-mismatch (SRM) checks continuously — SRM (e.g., 50.4/49.6 split with p<0.001) invalidates the experiment regardless of how exciting the lift looks.
- Maintain guardrail metrics (latency, error rate, unsubscribes, revenue) with automatic alerting so a "winning" UI change that degrades performance is caught by the platform, not by support tickets.
- Log every experiment in a searchable registry with hypothesis, result, and decision; institutional memory of dead ends is half the value of an experimentation culture.
- Extrapolate honestly: novelty and primacy effects decay, so check that week-3 treatment effects match week-1 before shipping, especially for engagement metrics.

## Pitfalls
- Calling a test at "significance reached" on day 2 of a 14-day plan — day-of-week cycles and novelty effects mean early reads are systematically biased.
- Segment fishing after a flat result ("it worked for Android users in Brazil!") without pre-registration or multiple-comparison correction.
- Testing trivialities (button hues) while the risky bets ship untested because "we can't experiment on that" — the biggest changes need experiments most, even if only as holdouts.

## Tools & references
Kohavi, Tang & Xu "Trustworthy Online Controlled Experiments," Evan Miller's sample-size calculator, Statsig/Eppo/GrowthBook/Optimizely, sequential testing (mSPRT), Microsoft ExP platform papers.
