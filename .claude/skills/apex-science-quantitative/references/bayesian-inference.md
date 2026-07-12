# Bayesian Inference

## Scope
Using Bayes' theorem to update beliefs with data, choosing priors, credible intervals, and epistemically navigating uncertainty.

## Core principles
- Bayes' theorem P(H|D) = P(D|H)P(H)/P(D) formalizes belief updating: your new belief in H given data D is proportional to how likely the data is under H times your prior.
- The prior P(H) encodes domain knowledge and regularizes inference; pure "objectivity" (flat priors) often produces absurd posteriors on edge cases.
- Posterior depends on both data and prior; with weak priors and strong data they converge, with vague data and strong priors the prior dominates — transparency about this trade-off matters more than the choice.
- Credible intervals (Bayesian) and confidence intervals (frequentist) answer different questions; a 95% credible interval means "given this data, 95% posterior mass is in this range" which is what people intuitively want.
- Marginalizing (integrating) over nuisance parameters avoids the multiple-comparisons penalty; you pay in interpretation complexity but gain statistical power.

## Apex practices
- Start with a generative model: write down how you believe data are created, then invert it (likelihood × prior → posterior).
- Use weakly informative priors (not flat, not tight) that encode reasonable bounds without dictating the answer.
- Visualize the posterior, not just point estimates; a bimodal posterior tells a different story than a normal one.
- Run sensitivity analyses: how does the posterior change with different priors? If it's stable, that's confidence; if it flips, transparency about prior dependence is critical.

## Pitfalls
- Choosing priors that determine the answer (confirms known result → "good Bayesian," contradicts gut → "bad prior"); this is backwards.
- Ignoring model misspecification; a "wrong" model with good inference is still wrong about the world.
- Posterior predictive checks require comparison to forward simulation from the posterior; many analysts skip this and miss that their model predicts nonsense.

## Tools & references
Gelman et al.'s "Bayesian Data Analysis," McElreath's "Statistical Rethinking," Stan probabilistic programming language, posterior predictive checks.
