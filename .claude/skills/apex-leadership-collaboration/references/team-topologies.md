# Team Topologies

## Scope
Organizing teams and their interaction modes so architecture, cognitive load, and delivery flow align.

## Core principles
- Conway's law is not a warning, it's a tool: systems mirror the communication structure of the org that builds them, so design the org to get the architecture you want (the "reverse Conway maneuver").
- Four fundamental team types (Skelton & Pais): stream-aligned (the default, owns a slice of user value end-to-end), platform (reduces others' cognitive load), enabling (temporary capability injection), and complicated-subsystem (deep specialist niche) — most orgs need mostly stream-aligned teams.
- Three interaction modes only: collaboration (temporary, expensive, for discovery), X-as-a-Service (cheap, for stable interfaces), and facilitating; a team pair stuck permanently in collaboration mode signals a boundary drawn wrong.
- Team cognitive load is the binding constraint: when a team owns more domains than it can hold in its head, quality and flow collapse — split ownership before splitting the codebase.
- Teams should be long-lived and work should flow to teams; project-based team reshuffling destroys the trust and shared context (Tuckman's forming-storming cost) that takes months to rebuild.

## Apex practices
- Map your current teams against the four types and flag the mutants: "DevOps teams" that are ticket-driven ops queues, "platform teams" nobody chose to use, shared-service teams that are pure dependencies.
- Treat the platform as a product with internal customers: adoption must be optional-but-irresistible; mandated platforms with captive users rot within two years.
- Run a cognitive-load survey ("do you understand, can you confidently change, everything you own?") before any reorg — reorganize around the overload, not the org chart aesthetics.
- Define team APIs explicitly: what the team owns, how to request work, communication channels, and working agreements — reduce the need for meetings by making the interface self-service.

## Pitfalls
- Splitting teams by technical layer (frontend team, backend team, DB team) so every user story requires three teams and two handoffs — Conway's law then ships you a lasagna.
- Creating an "enabling team" that becomes permanent and load-bearing; enabling teams that never leave are dependencies wearing a costume.
- Reorging as the first move; most flow problems are boundary or interaction-mode problems fixable without changing anyone's manager.

## Tools & references
Skelton & Pais "Team Topologies," Conway's 1968 paper "How Do Committees Invent?", teamtopologies.com patterns, "Dynamic Reteaming" (Helfand) for the counterpoint.
