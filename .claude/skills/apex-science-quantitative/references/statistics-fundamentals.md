# Statistics Fundamentals

## Scope
Descriptive and inferential statistics: distributions, hypothesis testing, confidence intervals, p-values, and avoiding common misinterpretations.

## Core principles
- A statistic (sample mean, sample variance) is a random variable; its value changes with each sample. Confidence intervals quantify this uncertainty; a 95% CI does not mean "95% chance the true value is in this range."
- Hypothesis testing answers "How surprising is this data if the null hypothesis is true?" not "What is the probability my hypothesis is right?" — p-values are likelihood of data, not likelihood of hypothesis.
- Statistical significance ≠ practical significance; a 0.1% improvement that is p < 0.001 with n=100k may be irrelevant for real decisions.
- Selection bias, measurement error, and confounding corrupt inference silently; no amount of statistical sophistication recovers from bad data collection.
- Normal distribution appears everywhere (CLT) but doesn't describe all phenomena; tails, skew, and outliers require domain knowledge, not assumption.

## Apex practices
- Report effect sizes and confidence intervals, not just p-values; a reader should know both whether something is real and whether it matters.
- Check assumptions (normality, homogeneity of variance, independence) before running tests; violating them often invalidates the whole analysis.
- Use permutation tests and bootstrapping when parametric assumptions break; they're more robust and clearer to explain.
- Pre-register or clearly separate exploratory from confirmatory analyses; p-hacking (hunting for significance) is invisible unless you declare intent upfront.

## Pitfalls
- Interpreting a p-value as "probability the null is false"; it's the probability of the data under the null, a completely different object.
- Multiple comparisons without correction (Bonferroni, FDR); with 20 tests at p=0.05, you expect one false positive by chance alone.
- Confusing correlation with causation; a strong association says nothing about mechanism without experimental control or causal inference.

## Tools & references
Goodman's "A Dirty Dozen," Kline's "Becoming a Behavioral Science Researcher," null hypothesis significance testing (NHST) vs. effect sizes, Tukey's EDA.
