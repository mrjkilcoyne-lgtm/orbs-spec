# Optimization

## Scope
Finding minimum or maximum of functions: linear programming, convex optimization, heuristic search, and understanding when solvers guarantee optimality.

## Core principles
- Optimization problems have structure: linear objectives with linear constraints (LP) are polynomial-time solvable; convex problems have unique global minima; non-convex problems are NP-hard in worst case.
- Feasibility and optimality are separate: a point might satisfy all constraints (feasible) but not minimize the objective. Many problems are constraint-satisfaction in disguise.
- Duality: every primal optimization problem has a dual; the gap between primal and dual values bounds suboptimality and informs algorithm design.
- Heuristics (simulated annealing, genetic algorithms, tabu search) work well on non-convex problems but provide no optimality guarantees; they're practical, not theoretical.
- Scalability requires exploitation of structure: sparse LP solvers, interior-point methods for convex problems, and gradient-based methods for differentiable non-convex problems.

## Apex practices
- Formulate problems in standard form (LP, SOCP, SDP, etc.) and use specialized solvers (CPLEX, Gurobi, MOSEK); they exploit structure you'd miss with a generic gradient descent.
- For non-convex problems, try multiple random restarts to escape local minima; better yet, use a two-phase approach (convex relaxation to warm-start, then local refinement).
- Solve the dual problem when primal is intractable; Lagrangian relaxation breaks hard problems into tractable pieces.
- Use warm-starts (previous solutions) to accelerate re-solves; sensitivity analysis shows how solutions change with problem parameters.

## Pitfalls
- Assuming gradient descent will find the global optimum in non-convex problems; it won't, even with good initialization.
- Ignoring numerical precision in linear programming; solvers can fail on ill-conditioned problems or with poor scaling.
- Over-engineering heuristics when a simple relaxation + rounding works well enough.

## Tools & references
Boyd's "Convex Optimization," NEOS (optimization server), CPLEX/Gurobi/SCIP (MIP solvers), Metaheuristics (Lin-Kernighan for TSP).
