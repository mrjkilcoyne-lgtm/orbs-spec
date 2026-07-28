# Probability

## Scope
Foundational concepts: sample spaces, conditional probability, independence, distributions, and the laws of large numbers and central limit theorem.

## Core principles
- Probability is about uncertainty under a fixed model; it breaks down when the model itself is unknown (model risk is often the real risk).
- Conditional probability P(A|B) = P(A∩B)/P(B) is not symmetric with causation; P(sick|test+) ≠ P(test+|sick) unless base rates are equal.
- Independence is strong: X and Y independent means knowing Y tells you nothing about X; most real phenomena are correlated; independence assumptions should be justified.
- Tail behavior matters: the Pareto principle (80/20) and power-law distributions are common in nature, making expected value a poor predictor without understanding the distribution.
- Law of large numbers proves that averages stabilize to true expectation; CLT says the distribution of those averages is normal (to a first-order), enabling inference.

## Apex practices
- Use Bayesian networks and directed acyclic graphs to visualize conditional independence; they clarify which variables d-separate (conditional on others) and which confound.
- Compute probabilities from first principles using counting or integrals rather than memorizing formulas; builds intuition.
- Distinguish epistemic uncertainty (model/data) from aleatoric uncertainty (natural randomness); the former shrinks with information, the latter doesn't.
- Simulate to verify intuition: when a closed-form solution is unclear, Monte Carlo sampling often clarifies what's happening.

## Pitfalls
- Assuming independence without checking (e.g., coin flips) or assuming dependence where there is none; both break inference.
- Ignoring base rates: P(A|B) depends heavily on P(A); rare events stay rare even with strong evidence.
- Confusing "rare under H0" with "impossible"; a p=0.001 result still happens once per 1000 experiments under the null.

## Tools & references
Feller's "Introduction to Probability Theory," Jaynes' "Probability: The Logic of Science," Kullback-Leibler divergence, probability simplex visualization.
