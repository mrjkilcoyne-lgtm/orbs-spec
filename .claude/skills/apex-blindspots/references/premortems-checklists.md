# Premortems & Checklists

## Scope
The two cheapest bias-defeating technologies: imagining failure before it happens, and externalizing memory so competence doesn't depend on recall under pressure.

## Core principles
- The premortem's trick is prospective hindsight: "it's six months from now and this project failed — write its history" produces ~30% more identified risks than "what could go wrong?", because declaring failure as fact licenses dissent that optimism-culture suppresses (Klein's method, Kahneman's endorsement).
- Premortems attack the planning fallacy at its root: plans are best-case narratives; the premortem forces the outside view in while changes are still cheap — one hour before kickoff outweighs a week of postmortem after.
- Checklists don't replace expertise, they free it: pilots and surgeons aren't reminded how to fly or cut — the checklist holds the killed-by-routine items (the retracted flaps, the unconfirmed patient ID, the un-run migration) so expert attention can go to judgment; the WHO surgical checklist cut deaths by nearly half with 19 items.
- The checklist must be short, killer-item-only, and paused-for: 5-9 items of "things that kill when skipped," run at a defined pause point (before merge, before deploy, before send) — comprehensive checklists get skimmed, and a skimmed checklist is theater.
- Both tools require cultural license: a premortem where dissent is punished and a checklist the senior person skips are dead rituals; the junior engineer must be able to say "checklist says no" and win.

## Detection tests
- Does this plan have a written list of ways it fails, generated before commitment?
- Do the recurring incident types in your postmortems appear as items in any pre-deploy checklist? (If not, you're paying for lessons twice.)
- Can anyone halt the process by invoking the checklist, in practice, against seniority?

## Countermeasures
- Run the 30-minute premortem on anything above a week's work: silent individual writing first (anti-anchoring), then aggregate, then assign the top 3 risks owners and tripwires.
- Convert postmortem action-items into checklist items or automation — the checklist is the interface between past incidents and future behavior.
- Review checklists quarterly: retire items automation now covers, add the newest near-miss; a stale checklist trains skipping.

## Tools & references
Gary Klein's premortem method, "The Checklist Manifesto" (Gawande), WHO surgical safety checklist, aviation CRM literature, pre-deploy checklist templates.
