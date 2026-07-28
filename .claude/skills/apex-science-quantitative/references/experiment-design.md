# Experiment Design

## Scope
Designing rigorous studies to isolate causal effects: randomization, blocking, sample size, power, and avoiding confounding.

## Core principles
- Randomization breaks confounding: if treatment and control differ only by chance, you can infer causation; confounding remains the silent killer of observational studies.
- Power (1−β) is the probability you detect a true effect; a well-powered study (typically 80%) needs larger sample sizes than people guess; running underpowered experiments wastes time.
- Blocking (stratifying by known confounders) reduces variance and increases power without requiring larger samples; it requires knowing what confounds.
- Intent-to-treat (ITT) preserves randomization; per-protocol analysis breaks it (non-compliance self-selects for motivation, etc.) and introduces bias.
- Blinding (single, double, or open) prevents bias in measurement and behavior; transparency about blinding level matters for interpreting results.

## Apex practices
- Pre-register the hypothesis, primary outcome, analysis plan, and sample size (via power calculation) before data collection; this prevents p-hacking.
- Use stratified randomization by known confounders to ensure balance on important covariates, especially with small sample sizes.
- Plan for missing data and attrition upfront; losing 30% of subjects to dropout invalidates randomization if non-random.
- Report all outcomes (primary and exploratory) and all analyses (planned and post-hoc); readers should see the full dataset, not a cherry-picked conclusion.

## Pitfalls
- Choosing sample size by convenience, not power; underpowered studies are noise with a random sign.
- Failing to account for multiple comparisons; running 20 "exploratory" tests and declaring significance on the one p<0.05 is expected under the null.
- Confusing statistical significance with clinical/practical significance; a tiny effect can be highly significant with large n but irrelevant in practice.

## Tools & references
Fisher's design of experiments, randomization and blocking schemes (Latin squares, incomplete blocks), power.t.test and pwr packages, effect-size meta-analyses.
