---
name: apex-orchestration
description: The harness doctrine for using the apex skillsets at scale. Use when planning any multi-step or multi-agent task, when deciding which skillsets to combine for a job, when rotating lenses across iterations, or when running agent swarms/batches with token economy. This is the meta-skill that makes the other 27 skillsets combinatorial.
---

# Apex Orchestration: Rotation & Combinatorial Skill Use

The 27 apex skillsets (540+ areas) are not a library to browse — they are lenses to stack, rotate, and distribute. This skill encodes the three mechanisms plus the token-economy rules that keep the whole system cheap.

## The core model
- **A skillset is a lens**: it makes certain defects and opportunities visible and leaves others invisible. No single lens sees everything — that is why apex-blindspots exists as the universal second lens.
- **A task gets a stack**: domain lens (what the work is about) + craft lens (what the artifact is) + check lens (how it fails). Example: "payment webhook handler" = backend-distributed(idempotency, background-jobs) + software-engineering(error-handling) + blindspots(concurrency, silent-failures).
- **An iteration gets a rotation**: the lens that authored is never the only lens that reviews.

## Areas
- references/combination-patterns.md — the stacking grammar: which skillsets amplify each other
- references/rotation-protocols.md — cycling lenses across iterations, reviews, and time
- references/swarm-harness.md — batched multi-agent execution with token economy

## Quick protocol (any nontrivial task)
1. Name the stack: 2-3 skillsets, ≤6 reference files total. Write it down in one line.
2. Read only those files. Execute.
3. Rotate for the check: review with a lens not used in authoring (blindspots minimum).
4. If the task decomposes into ≥5 independent units → swarm-harness.md; otherwise stay inline.
