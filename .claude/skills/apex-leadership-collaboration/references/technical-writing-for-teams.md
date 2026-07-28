# Technical Writing for Teams

## Scope
Writing that coordinates engineering work: design docs, RFCs, ADRs, postmortems, and async proposals.

## Core principles
- A design doc's job is to be disagreed with cheaply: an hour of writing that surfaces a fatal objection before code exists is the highest-ROI hour in engineering — docs are a debugging tool for thinking.
- BLUF (bottom line up front): state the decision/proposal in the first three sentences; readers triage in 30 seconds, and a conclusion buried on page four is a conclusion unread.
- Write for the skimming reader: informative headings that carry the argument by themselves, one idea per paragraph, and a "tl;dr + what I need from you" block at the top — assume 80% of readers read 20%.
- Architecture Decision Records capture the why at decision time: context, options considered, decision, consequences — six months later, "why is it built this way?" has a written answer instead of archaeology.
- The alternatives section is the credibility section: a proposal listing only one option reads as a conclusion in search of a justification; steelman the rejected paths, including "do nothing."

## Apex practices
- Circulate docs before meetings and open the meeting with silent reading time (the Amazon 6-pager model) — discussion quality doubles when everyone has actually read it.
- Scope docs by decision, not by system: "should we shard by tenant or by region?" gets a decision; "the architecture of everything" gets 40 comments about naming.
- Timebox comment periods explicitly ("comments by Thursday, decision Friday") — RFCs without a decision deadline become permanent suggestion boxes.
- Keep a team decision log (dated one-liners linking to ADRs); it converts tribal memory into greppable history and cuts re-litigation dramatically.

## Pitfalls
- Writing the doc after the code to ratify a decision already made — reviewers smell it, feedback becomes theater, and the doc culture dies.
- Comprehensive-first documents: a 15-page spec for an idea that needed a 1-page problem statement to test whether anyone cares.
- Treating "no comments" as approval; silence usually means "didn't read," so require named reviewers to sign off explicitly.

## Tools & references
Google's design docs culture (industry write-ups by Malte Ubl), Nygard's ADR format (adr.github.io), Amazon's narrative 6-pager and PR/FAQ, "Docs for Developers" (Bhatti et al.).
