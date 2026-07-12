# Causal Inference

## Scope
Identifying and estimating causal effects from observational data using structural methods: DAGs, backdoor criterion, instrumental variables, difference-in-differences.

## Core principles
- Correlation is not causation; but causation produces correlation (and is never the only explanation for it). The challenge is ruling out confounding paths.
- A directed acyclic graph (DAG) maps causal relationships and reveals which variables must be controlled to block backdoor paths; visual inspection beats intuition.
- The backdoor criterion formalizes which variables to adjust for; controlling the wrong ones (like a mediator) can introduce bias even with good intentions.
- Instrumental variables (IV) exploit natural variation uncorrelated with confounders to estimate causal effects; they require strong assumptions (exclusion restriction) that are often untestable.
- Counterfactual logic: causation is defined by what would have happened in an alternate world; most causal quantities are not empirically observed, only inferred.

## Apex practices
- Draw a DAG for your problem before analyzing data; it clarifies what you're actually estimating and what might go wrong.
- Use propensity-score matching or inverse probability weighting to approximate randomization when confounders are measured.
- Difference-in-differences leverages natural experiments (policy changes, geographic rollouts) to compare treated and control groups over time, removing unobserved time-invariant confounding.
- Sensitivity analyses: show how conclusions change if there's unmeasured confounding of unknown magnitude; honesty about assumptions is higher value than illusion of precision.

## Pitfalls
- Controlling for a collider (a variable caused by both treatment and outcome) opens a backdoor path that wasn't there; this introduces bias.
- Assuming IV assumptions (exclusion restriction, first-stage strength, monotonicity) without strong justification; even slight violations produce large biases.
- Over-interpreting observational studies as causal without explicit causal identification strategy; correlation masquerading as causation remains common.

## Tools & references
Pearl's "Book of Why," Cunningham's "Causal Inference Mixtape," DAG software (DAGitty), causal effect estimation (causal forests, double/debiased machine learning).
