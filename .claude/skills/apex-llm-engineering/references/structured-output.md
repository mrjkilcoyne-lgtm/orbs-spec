# Structured Output

## Scope
Getting machine-parseable output from LLMs: JSON modes, schema-constrained decoding, extraction pipelines, and validation/repair loops.

## Core principles
- Use the strongest constraint the platform offers, in order: native structured-outputs/schema mode (grammar-constrained decoding) > tool/function-call with JSON Schema > JSON mode > "please output JSON" — each rung down trades guarantees for hope.
- Constrained decoding guarantees syntax, never semantics: the JSON will parse, but fields can still be wrong, empty, or hallucinated — validation (Pydantic/Zod, business rules) and evals remain mandatory.
- Schema design is prompt engineering: field names and descriptions are read by the model, so `delivery_date` with description "ISO 8601, null if not mentioned in the text" outperforms `dt1`; every optional-without-default field is an invitation to invent.
- Force an escape hatch for absence: require nullable fields or an explicit `"not_found"` value — a schema in which every field is required-and-non-null converts missing information into fabrication.
- Over-constraining hurts reasoning: models score worse on hard reasoning when forced into rigid formats mid-thought; let the model reason in free text (or a `reasoning` field ordered first), then emit the structured answer.

## Apex practices
- Define schemas once in code (Pydantic/Zod) and derive both the API schema and the runtime validator from it — hand-maintained parallel schemas drift within a week.
- Build a validate-and-repair loop: on validation failure, re-prompt with the specific error and the invalid output, cap retries at 1-2, then fall back to a stronger model or a human queue; log every repair as an eval case.
- For extraction, quote evidence: add a `source_quote` field per extracted value so downstream code (and reviewers) can verify each field against the input verbatim.
- Keep enums closed and small, and order object fields so dependent values come after the evidence for them (models generate tokens in order — field order is computation order).

## Pitfalls
- Parsing JSON out of markdown fences with regex when the API has a structured mode — brittle, and it breaks the day the model adds a preamble.
- Deeply nested, anyOf-heavy schemas: constrained decoders and models both degrade; flatten to 1-2 levels and split mega-schemas into multiple calls.
- Assuming temperature 0 + schema = determinism: sampling still varies across versions and hardware; idempotency must come from your pipeline, not decoding settings.

## Tools & references
OpenAI Structured Outputs, Anthropic tool-use for extraction, Pydantic/Instructor, Zod, Outlines and llguidance (open-source constrained decoding), JSON Schema spec.
