# Calculus for ML

## Scope
Derivatives, gradients, chain rule, second-order methods, and geometric interpretation for optimization and learning.

## Core principles
- The gradient ∇f points in the direction of steepest ascent; gradient descent moves opposite to find minima. Local curvature (Hessian eigenvalues) determines how far you can step safely.
- The chain rule (d/dx f(g(x)) = f'(g)g'(x)) is the engine of backpropagation; without it, neural networks wouldn't scale.
- Second-order information (Hessian) tells you about the curvature of the loss surface; pure gradient descent is agnostic to this, but Newton's method and quasi-Newton (BFGS) exploit it.
- Convexity is powerful: a convex function has one global minimum and any local minimum is global; most neural networks are non-convex, which is why initialization matters.
- Lagrange multipliers connect constrained optimization to unconstrained: add penalties to handle constraints, or work with dual formulations.

## Apex practices
- Compute gradients via automatic differentiation (reverse-mode / backprop for scalars, forward-mode for many derivatives) rather than finite differences, which are slow and numerically unstable.
- Understand learning rates: large steps overshoot, small steps crawl. Adaptive methods (Adam, RMSprop) adjust per-coordinate; learning-rate schedules (decay, warmup) often help.
- Use second-order methods (Newton, BFGS) for well-conditioned problems; gradient descent is more robust for ill-conditioned or noisy (stochastic) settings.
- Check numerical stability of loss gradients; log-domain tricks prevent underflow/overflow (e.g., log-sum-exp instead of direct softmax).

## Pitfalls
- Ignoring numerical precision in gradient computation; accumulated floating-point error in deep chains can corrupt learning.
- Confusing optimization surface smoothness with generalization; a smooth loss landscape doesn't guarantee the learned model generalizes.
- Assuming convex approximations locally hold globally; the loss is non-convex, and saddle points outnumber local minima in high dimensions.

## Tools & references
Goodfellow et al.'s "Deep Learning" (chapter 4), Boyd's "Convex Optimization," automatic differentiation papers, matrix calculus cookbook.
