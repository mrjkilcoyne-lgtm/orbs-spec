# Gaming Industry

## Scope
Game development, publishing, and operations: live-service games, monetization (F2P, premium), matchmaking, anti-cheat, and community management.

## Core principles
- Live-service games are software-as-service: they launch unfinished and evolve via updates, cosmetics, and seasonal content — the product never ships, it operates.
- Monetization strategy (F2P with battle pass, cosmetics, P2P, premium + DLC) shapes design: F2P requires endless progression loops and FOMO (fear of missing out); P2P can ignore extraction maximization.
- Player retention follows power law: a few whales (high-spending players) fund the game; most are casuals; systems must support both, which creates complexity.
- Matchmaking (skill-based, player count-based) affects experience and retention; poor matchmaking (stomping or being stomped) drives churn; algorithms are non-trivial.
- Anti-cheat is an arms race: cheats evolve faster than detection (kernel-level anticheats like Vanguard are increasingly required); purely server-side detection is loseable.

## Apex practices
- Design for telemetry from day one: player behavior (session length, churn, spending, progression rate) informs balance and economy changes; data shapes the game post-launch.
- Implement server-authoritative gameplay: client sends input, server simulates, server sends result; never trust client state for anything meaningful (position, resources, kills).
- Version assets and content: a patch system that downloads deltas (changed files only) saves bandwidth and update time; full reimport is slow.
- Build moderation tools and community guidelines: player-generated content (chat, user names, clans) requires filtering (profanity, hate speech) and reporting (abuse).

## Pitfalls
- Launching without server capacity forecasting; viral growth crashes servers (or underutilization wastes money).
- Extractive monetization without fun; a game designed around payment friction kills engagement.
- Ignoring toxicity; competitive games with poor moderation drive away new players and foster grinding/toxic culture.

## Tools & references
Unity, Unreal Engine, GDC talks (production, monetization, live-ops), Newzoo (market research), SpeedRun (MMO design), Beihoff's "The Ultimate Guide to Video Game Writing and Design."
