# Hallucination Mitigation

## Scope
Reducing and containing fabricated LLM output: grounding, abstention, verification layers, calibration, and UX that makes residual errors survivable.

## Core principles
- Hallucination is intrinsic to autoregressive generation, not a bug to be patched out: the model always emits plausible continuations, and training that rewards guessing over abstaining makes confident fabrication the default — so the engineering goal is containment and detection, not elimination.
- Risk concentrates in predictable places: specifics beyond the model's knowledge (citations, URLs, case law, prices, version numbers, people), low-resource topics, and questions premised on false assumptions — treat these as hot zones needing grounding or verification, not general anxiety.
- Grounding converts generation into transcription: answers restricted to provided context ("answer only from <docs>; otherwise say you don't know") with mandatory citations shift the failure mode from invisible fabrication to checkable claims — this is the single highest-leverage mitigation.
- Verification must be independent of generation: self-review by the same model in the same context re-samples the same error distribution; real checks are retrieval-backed fact verification, code execution, schema/business-rule validation, or a second model with different grounding.
- Calibration matters more than accuracy at the margin: a system that is 90% accurate and says "I'm not sure" on the right 10% is deployable; one that is 95% accurate with uniform confidence is a liability — measure abstention quality, not just correctness.

## Apex practices
- Give every prompt an explicit out ("if the information isn't present, say so — never guess") and eval the null case with questions that have no answer in the corpus; without unanswerable cases in the eval, abstention silently atrophies.
- Post-process high-stakes claims: extract factual assertions, verify each against retrieval or APIs (do the cited docs exist? does the quoted line appear?), and flag or strip unverified ones — citation-existence checking alone catches the most embarrassing class.
- Use sampling disagreement as a cheap confidence signal (SelfCheckGPT pattern): sample 3-5 answers; facts that vary across samples are unreliable, facts stable across samples usually aren't — route unstable answers to review.
- Design the UX for fallibility: inline citations, "verify before use" affordances on hot-zone content, and one-click feedback that feeds the eval set — users are your last verification layer, so equip them.

## Pitfalls
- Believing temperature 0 stops hallucination — it makes fabrication deterministic, not true; the model confidently repeats the same wrong answer.
- Prompting "do not hallucinate" as the mitigation strategy; without grounding, abstention instructions, or verification, it measurably does almost nothing.
- Trusting the model's self-reported confidence ("I'm 95% sure") — verbalized confidence is itself generated text, poorly calibrated, and biased high.

## Tools & references
SelfCheckGPT (Manakul et al. 2023), "Why Language Models Hallucinate" (OpenAI 2025), RAGAS faithfulness metrics, TruthfulQA/HaluEval benchmarks, provider grounding/citations features (Anthropic citations, Gemini grounding).
