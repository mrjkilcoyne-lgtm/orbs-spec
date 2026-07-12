# Hallucination Awareness

## Scope
Confidently producing plausible-but-false specifics: API names, flags, citations, version numbers, historical details — the failure mode of fluent generators, human and machine.

## Core principles
- Fluency and truth are uncorrelated at the detail level: memory (biological or model weights) reconstructs rather than retrieves; the reconstruction fills gaps with plausible material and marks nothing.
- Specificity is where hallucination lives: broad claims ("Postgres supports JSON") are usually safe; specifics ("the `jsonb_deep_merge` function") are where invented details hide — treat every proper noun, flag, and number as unverified until checked.
- Interpolation between true anchors feels like knowledge: knowing v2 and v4 exist makes "v3 added X" feel remembered when it's inferred — inference wearing memory's clothes.
- The confabulation is self-consistent: invented details support each other (a fake function gets fake parameters with plausible types), so internal coherence is worthless as a truth check — only external verification counts.
- Frequency in training/exposure sets reliability: common, stable knowledge (HTTP 404) is reliable; rare, recent, or fast-changing knowledge (niche library APIs, current versions, prices) is exactly where confident recall fails.

## Detection tests
- Is this claim a checkable specific (name, number, flag, quote, citation)? Then has it actually been checked in docs/source/run output this session?
- Would I bet a day of work that this API exists exactly as I wrote it?
- Is the knowledge domain fast-moving or niche? Downgrade recall confidence accordingly.

## Countermeasures
- Verify specifics against the local source of truth before asserting: read the actual code, run --help, check the docs — the 30-second check beats the 3-hour wild goose chase.
- When unverifiable, mark it: "from memory, verify before relying" is honest; silent confidence is not.
- Prefer running/testing over recalling: an executed example is self-verifying.

## Tools & references
Docs-first workflows, `--help`/source-reading habits, retrieval-augmented patterns, citation-checking discipline from journalism.
