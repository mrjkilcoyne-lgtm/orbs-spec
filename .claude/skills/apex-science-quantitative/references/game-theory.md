# Game Theory

## Scope
Strategic interaction: normal and extensive form, Nash equilibrium, dominant strategies, cooperative vs. non-cooperative games, and auction design.

## Core principles
- A game specifies players, actions, outcomes, and payoffs; Nash equilibrium is a strategy profile where no player benefits from unilateral deviation (it's self-enforcing, not necessarily efficient).
- Dominant strategies (best-response regardless of others' plays) are rare; instead, find equilibria where each player's strategy is a best-response to others'.
- Common-knowledge assumptions (everyone knows the game, everyone knows everyone knows, etc.) matter; many paradoxes dissolve under asymmetric information.
- Cooperative games (with binding agreements) can achieve efficiency that non-cooperative games cannot (prisoners' dilemma); incentive alignment is the core of economics and mechanism design.
- Mixed strategies (randomizing) occur in equilibrium when pure strategies don't suffice; they're unintuitive but force equal expected payoff across played actions.

## Apex practices
- Use WLOG (without loss of generality) symmetry to reduce game analysis; symmetric players often play symmetric equilibria.
- Backward induction on extensive form (game trees) finds subgame-perfect equilibrium; forward induction is subtler and handles signaling.
- Recognize auction design as a mechanism-design problem: set rules so truthful bidding is a dominant strategy (Vickrey auction).
- Apply network effects and externalities framing: if one player's payoff depends on others' choices, game-theory perspective clarifies design.

## Pitfalls
- Assuming rational play; bounded rationality, herding, and learning all reshape equilibrium in real settings.
- Confusing Nash equilibrium (stable strategy profiles) with Pareto efficiency (no mutual improvement possible); many equilibria are inefficient.
- Ignoring that multiplicity of equilibria means the model underdetermines outcomes; history, focal points, and coordination devices break ties.

## Tools & references
Osborne-Rubinstein "A Course in Game Theory," von Stengel's tutorials, Gambit (software), mechanism design (Myerson, Jackson).
