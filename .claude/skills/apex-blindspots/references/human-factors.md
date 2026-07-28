# Human Factors

## Scope
The blindspot of designing for yourself: the expert's curse, the invisible mental-model gap between builder and user, and error-tolerant design.

## Core principles
- The curse of knowledge is irreversible: once you know how the system works, you cannot experience not-knowing it — your interface seems obvious because you built the model it assumes; users arrive with a different model and the gap is invisible from your side (five real users finding 85% of usability problems is the empirical fix).
- Users don't read, they forage: they scan for the first plausible-looking action and take it (satisficing), skip instructions, and interpret everything through what they were already trying to do — design for the scanner, and put the meaning where the eye lands.
- Human error is a design output, not a user defect: slips (right intention, wrong action — adjacent buttons) and mistakes (wrong model — misunderstood feature) have different fixes (spacing/confirmation vs conceptual clarity); a system that punishes predictable error patterns is the thing that's broken (Norman's doors, Dekker's new view).
- Cognitive load is a budget you're spending: every choice, field, unfamiliar term, and state the user must remember draws from working memory (~4 chunks); expert-designed interfaces routinely spend 10x the budget because the designer's chunks are pre-compressed.
- Real usage context is hostile: interrupted sessions, phone in one hand, low motivation, second language, first time — the lab-perfect flow meets the school pickup line; design for the distracted median, not the focused ideal.

## Detection tests
- Watch one real person attempt the task cold, silently: where do they pause, misclick, or say "hm"? (Every "hm" is a defect report.)
- Read the interface aloud pretending you don't know the system: which words are internal jargon?
- What happens when a user does the most plausible wrong thing? Is recovery one step or a support ticket?

## Countermeasures
- Usability-test small and often (5 users, think-aloud, before every major release) — watching is the only cure for the curse of knowledge.
- Design the error paths as first-class flows: undo over confirmation dialogs, forgiving formats (paste with spaces, any date format), inline recovery.
- Enforce a jargon audit: every label passes the "would a new user's mom parse this?" test or gets renamed.

## Tools & references
"The Design of Everyday Things" (Norman), Nielsen's heuristics + 5-user research, Krug "Don't Make Me Think," Dekker on human error, cognitive load theory (Sweller).
