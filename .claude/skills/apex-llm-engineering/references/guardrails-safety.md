# Guardrails & Safety

## Scope
Keeping LLM applications within policy: input/output filtering, prompt-injection defense, PII handling, and safe failure modes for user-facing systems.

## Core principles
- Defense in depth, because the model will comply with something it shouldn't: layer system-prompt policy, input classification, output filtering, and tool-permission scoping — no single layer holds against a motivated adversary.
- Prompt injection is unsolved; architect as if the model can be jailbroken, because it can: the security boundary must be capabilities (what tools/data the session can touch), not instructions ("please ignore malicious content" is not a control).
- The lethal trifecta (Willison): private-data access + untrusted-content exposure + external communication in one agent = exfiltration by design; break at least one leg architecturally.
- Refusals are a product surface: over-blocking erodes trust as surely as under-blocking causes incidents — measure false-positive rate on benign traffic with the same rigor as attack catch-rate.
- PII must be handled structurally, not behaviorally: redact/tokenize before the model sees it where possible, scan outputs before display, and define retention for logs — "the model was told not to reveal it" is not a compliance answer.

## Apex practices
- Run a lightweight moderation/classifier pass (Llama Guard, provider moderation APIs, or a small fine-tuned classifier) on inputs and outputs asynchronously where latency allows, blocking only on high-confidence categories.
- Red-team continuously with a maintained attack corpus — direct injections, indirect injections via retrieved documents, encoding tricks (base64, translation), multi-turn crescendo attacks — and wire it into CI like any other eval.
- Scope tools per session to least privilege: read-only by default, user-scoped credentials (never a god-token), human confirmation for irreversible actions, and egress allowlists for anything that can make network calls.
- Design the failure UX deliberately: a refusal should state what it can't do and offer a safe alternative or human handoff; log every trip of every guardrail with enough context to tune thresholds.

## Pitfalls
- Trusting retrieved or tool-returned content implicitly — indirect injection via a poisoned webpage, email, or ticket is the dominant real-world attack on agents.
- Blocklist-string filtering as "safety" (regex for bad words): trivially bypassed by paraphrase, translation, or encoding, while flagging legitimate medical/security discussions.
- Bolting safety on after launch: retrofitting permission scoping onto an agent that already has broad tool access is a rewrite, not a patch.

## Tools & references
OWASP Top 10 for LLM Applications, Simon Willison's prompt-injection series, Llama Guard, NeMo Guardrails, Guardrails AI, Anthropic/OpenAI moderation APIs, NIST AI RMF.
