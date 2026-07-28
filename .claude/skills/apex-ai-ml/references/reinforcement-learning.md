# Reinforcement Learning

## Scope
Learning from interaction with an environment: rewards, value functions, policy gradients, and Q-learning. Markov decision processes and temporal difference learning.

## Core principles
- Reinforcement learning models interaction as MDP (Markov Decision Process): agent takes action in state, receives reward, moves to next state. Goal: maximize cumulative reward.
- Value function V(s) = expected cumulative reward from state s; Q(s, a) = expected cumulative reward for taking action a in state s. Value function methods (value iteration, Q-learning) learn value estimates.
- Policy π(a|s) = probability of taking action a in state s. Policy gradient methods (REINFORCE, Actor-Critic, PPO, A3C) directly optimize the policy by taking gradient steps that increase expected reward.
- The exploration-exploitation tradeoff: exploit known good actions (greedy), explore to find better ones (random). Epsilon-greedy (act random with probability epsilon) is simple; more sophisticated: Thompson sampling, upper confidence bound.
- Credit assignment is hard: a sequence of actions (a1, a2, ..., an) produces a reward at the end. Which action caused success? Value functions with bootstrapping and discount factors (γ < 1) solve this.

## Apex practices
- Start with simple environments (grid world, Atari) to debug algorithms. Policy gradient methods (A3C, PPO) are more stable than Q-learning for continuous control.
- Use reward shaping (auxiliary rewards) to guide learning if task reward is sparse. A well-shaped reward accelerates learning; poorly shaped rewards can lead astray.
- Implement experience replay: store transitions (s, a, r, s') in a buffer, sample minibatches for learning. This decorrelates samples (breaks serial correlations) and improves sample efficiency.
- Normalize rewards and observations to stabilize learning. Unstable training (loss diverges, no progress) often traces to poor normalization.

## Pitfalls
- Non-stationary policy: exploration policy (for collecting data) differs from target policy (being optimized). This breaks Q-learning convergence. On-policy (REINFORCE, A3C) methods are safer; off-policy (Q-learning, DQN) require importance sampling corrections.
- Reward misspecification: if the environment reward is mis-aligned with the actual goal, the agent optimizes the reward (literally) rather than solving the task. Example: agent learns to cheat (game rules vs. spirit of the game).
- Not accounting for stochasticity in environments; deterministic algorithms (value iteration) fail in stochastic environments (environment dynamics are random). Robust methods (distributional RL) account for randomness.

## Tools & references
OpenAI Gym (environments), Stable Baselines3 (algorithms), Ray RLlib (distributed), "Reinforcement Learning: An Introduction" (Sutton & Barto), "Deep Reinforcement Learning Doesn't Work Yet" (Irpan, blog), Atari benchmarks.
