# Monte Carlo Simulation

## Scope
Estimating quantities via random sampling: convergence rates, variance reduction, importance sampling, and when simulation beats analysis.

## Core principles
- The law of large numbers guarantees convergence: average of n samples converges to expectation; standard error ∝ 1/√n (slow convergence, but robust).
- Variance reduction (stratification, control variates, antithetic sampling) reduces error per sample without changing algorithm; critical for high-dimensional problems.
- Importance sampling reweights samples from an easy distribution to match a hard distribution; it trades bias correction (reweighting) for lower variance if proposal is close to target.
- Rejection sampling discards samples that don't match the target; wasteful if acceptance probability is low but requires no density evaluation.
- Markov chain Monte Carlo (MCMC) generates correlated samples from a target distribution; Metropolis-Hastings and Gibbs sampler are staples (burn-in and thinning are debugging tricks, not statistical requirements).

## Apex practices
- Use stratified sampling (partition domain, sample uniformly from each partition) for low variance without complex proposals.
- For high-dimensional posteriors, Hamiltonian MC (gradient-informed) beats random-walk MCMC; Stan and PyMC3 automate this.
- Check convergence diagnostically: R̂ (potential scale reduction factor) < 1.01 is gold standard; trace plots reveal whether chains mix.
- Validate simulations against known results or faster approximations; a simulation that doesn't match ODE solutions or closed-form special cases has a bug.

## Pitfalls
- Assuming MCMC converges when it's actually stuck; visual inspection of traces and formal diagnostics (R̂, autocorrelation) are non-negotiable.
- Over-thinning MCMC samples to reduce autocorrelation; every sample has information; just use all of them.
- Importance sampling with a proposal far from target; acceptance probability plummets and variance explodes; test on a toy problem first.

## Tools & references
Robert-Casella "Monte Carlo Statistical Methods," Stan probabilistic programming, PyMC3, variational inference as fast approximate alternative.
