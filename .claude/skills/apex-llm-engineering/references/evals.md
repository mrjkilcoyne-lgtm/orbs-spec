# Evals

## Scope
Measuring LLM system quality: eval set construction, graders (code, human, LLM-judge), metrics, and wiring evals into the development loop.

## Core principles
- No eval, no engineering: without a fixed test set and grader, every prompt/model/retrieval change is vibes; the eval suite is to LLM work what the test suite is to code — it comes first and it gates merges.
- Evals must be drawn from real traffic, refreshed as usage drifts: 50-200 real, hard, labeled cases beat 5,000 synthetic easy ones; oversample past failures and edge cases, because the eval's job is to catch regressions, not flatter you.
- Graders form a ladder of trust: deterministic code checks (exact match, schema-valid, tests pass) > human labels > LLM-as-judge; use the cheapest grader that captures the criterion, and validate LLM judges against human labels (aim for agreement comparable to human-human) before trusting them.
- LLM judges have known biases — position bias (prefer first answer), verbosity bias, self-preference — mitigate with pairwise swaps, rubric-anchored scoring (score each criterion separately), and a different model family as judge.
- One aggregate score hides everything: slice results by intent, input length, language, and difficulty; a +3% average that's -20% on your top customer's use case is a regression.

## Apex practices
- Run evals in CI on every prompt, model, or pipeline change with statistical honesty: nonzero temperature means run multiple trials; report pass@k or mean±CI, and don't celebrate differences smaller than run-to-run noise.
- Convert every production incident into an eval case the same day — the eval suite should be a fossil record of everything that ever went wrong.
- Write rubrics as binary checks, not 1-10 scales: "cites at least one source: Y/N", "no fabricated fields: Y/N" — decomposed booleans are reproducible; holistic scores drift.
- Keep a small "canary" eval (10-20 cases, <2 min) for inner-loop iteration and a full suite for merges; evals only shape behavior if they're fast enough to run constantly.

## Pitfalls
- Grading against reference answers with exact string match on open-ended tasks — you end up measuring phrasing, not correctness.
- Eval-set overfitting: iterating on the same 50 visible cases until you've hand-tuned to them; hold out a hidden set and rotate.
- Benchmarking on public leaderboards (MMLU, HumanEval) to choose a model for your task — public benchmarks are contaminated and correlate weakly with domain-specific performance.

## Tools & references
promptfoo, OpenAI Evals, Braintrust, LangSmith, "Judging LLM-as-a-Judge / MT-Bench" (Zheng et al. 2023), Hamel Husain's "Your AI Product Needs Evals".
