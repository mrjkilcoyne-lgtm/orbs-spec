# User Stories

## Scope
Expressing requirements as thin, testable slices of user value: story writing, splitting, acceptance criteria, and the conversations they exist to trigger.

## Core principles
- A story is a token for a conversation, not a mini-spec (Ron Jeffries' 3 Cs: Card, Conversation, Confirmation); teams that skip the conversation and "just read the ticket" get the letter of the card and none of its intent.
- INVEST (Independent, Negotiable, Valuable, Estimable, Small, Testable) is a splitting diagnostic: a story failing "Valuable" is a task in disguise; failing "Small" needs vertical slicing, not a bigger sprint.
- Slice vertically through the stack (thin end-to-end path: UI → API → DB), never horizontally by layer — "build the database schema" delivers zero user value and can't be validated by anyone outside engineering.
- The "so that" clause is the load-bearing part of "As a…, I want…, so that…"; if the benefit is circular ("so that I can use the feature"), the team is coding without knowing what outcome to protect when trade-offs arise.
- Acceptance criteria define done in observable behavior (Given/When/Then works well), and they are examples, not exhaustive specs — edge cases emerge in the conversation and in example mapping.

## Apex practices
- Run example mapping (Matt Wynne): 25-minute sessions producing rules, examples, and questions per story; a story with too many rule cards gets split on the spot.
- Split with named patterns (SPIDR: Spikes, Paths, Interfaces, Data, Rules — Mike Cohn; or Richard Lawrence's 10 patterns) rather than improvising; workflow-step and business-rule splits cover 80% of cases.
- Write the demo script before the code: "here's what I'll show at review" is the cheapest acceptance test and catches unvaluable slices early.
- Keep stories problem-shaped and let solutioning happen in refinement — a story that prescribes the implementation forecloses the engineer's cheaper idea.

## Pitfalls
- Story-format theater: "As a system, I want a cron job" — mechanically wearing the template while expressing zero user intent.
- Stories so large they span sprints, then get "carried over" indefinitely; anything not completable in a few days should be split again.
- Treating acceptance criteria as a contract to lawyer over instead of updating them when the conversation reveals better understanding.

## Tools & references
Mike Cohn "User Stories Applied," Jeff Patton "User Story Mapping," example mapping (Wynne), INVEST (Bill Wake), SPIDR, Gherkin/Given-When-Then.
