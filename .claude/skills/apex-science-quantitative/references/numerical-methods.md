# Numerical Methods

## Scope
Solving differential equations, interpolation, integration, and root-finding via discrete approximation; understanding error and stability.

## Core principles
- Continuous problems (differential equations, integrals) are solved on finite grids; discretization introduces truncation error (algorithm error) and rounding error (floating-point).
- Stability is whether small input perturbations produce small output changes; unstable methods amplify errors and diverge; stability often conflicts with accuracy, requiring trade-offs.
- Step size (Δt, Δx) controls accuracy and stability; smaller steps are more accurate but accumulate rounding error; too-large steps miss features (overshooting, oscillation).
- Convergence rates (O(h), O(h²), exponential) tell you how fast error shrinks with refinement; a higher-order method pays off only if the problem is smooth.
- Adaptive methods adjust step size based on local error estimates; they balance accuracy and efficiency without manual tuning.

## Apex practices
- Use explicit methods (Euler, RK4) for non-stiff ODEs; implicit methods (backward Euler, BDF) for stiff ones where explicit methods require tiny steps.
- Verify convergence by solving with multiple step sizes and checking that error decreases at the predicted rate.
- Gauss quadrature and adaptive quadrature (Clenshaw-Curtis, tanh-sinh) are fast and accurate for smooth integrals; Monte Carlo for high-dimensional integrals.
- Test numerical code against known analytical solutions (when available) and manufactured solutions (plug in a known smooth function and check).

## Pitfalls
- Using forward Euler on stiff equations (timesteps must be tiny, convergence is slow); recognize stiffness (eigenvalues with very different scales) and switch methods.
- Ignoring error accumulation over long simulations; local error is small per step but compounds; use error-control methods (RK45 with adaptive step size).
- Assuming high precision in the solution when the model itself is approximate; no amount of numerical precision fixes bad modeling.

## Tools & references
Trefethen's "Finite Difference Computing with PDEs," SciPy integrate/solve_ivp, Butcher tables for Runge-Kutta methods, stability regions and absolute stability.
