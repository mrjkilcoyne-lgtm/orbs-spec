# The Accessibility Blindspot

## Scope
Why able-bodied builders systematically ship inaccessible products — the perceptual blindness itself, beyond the WCAG mechanics.

## Core principles
- You cannot feel the absence: the developer sees the screen, uses the mouse, hears the video — every missing alt text, focus trap, and uncaptioned clip is invisible in their own experience; accessibility failures are the canonical unknown-known, obvious the moment you switch modality and undetectable before.
- It's not edge-case work: ~16% of people have a disability, everyone ages into changing vision/motor/hearing, and situational impairment (bright sun, holding a baby, broken arm, loud train) makes every user a temporary member — the "small minority" framing is the blindspot talking.
- Retrofit costs 10-100x design-time cost: accessibility bolted on means re-architecting focus management, DOM order, and color systems; accessibility designed in means using the semantic element in the first place — the cost asymmetry means "later" effectively means "never."
- The automated-tool ceiling: axe and Lighthouse catch roughly a third of issues (the mechanically checkable ones); keyboard navigation logic, focus order sense, screen-reader comprehensibility, and cognitive load need a human actually operating the interface non-visually.
- Accessible ≠ pleasant to use with AT: passing WCAG while requiring 47 tab presses to reach the main action is compliant hostility — the goal is equivalent experience quality, not checkbox parity.

## Detection tests
- Unplug the mouse: can every task complete keyboard-only, with visible focus, in sensible order?
- Turn on the screen reader for one real task: does the page narrate sense or soup?
- Grayscale the screen: does anything lose its meaning (color-only signals)?

## Countermeasures
- Build modality-switching into the routine: one keyboard-only day-slice and one screen-reader session per feature, before review, by the person who built it.
- Adopt semantic-first construction (real buttons, labels, headings, landmarks) — 80% of accessibility is not un-breaking HTML.
- Put a11y checks in CI (axe) AND in the definition of done (manual keyboard pass) — automation for the floor, humans for the experience.

## Tools & references
WCAG 2.2 + ARIA APG, axe-core, NVDA/VoiceOver, WebAIM's screen-reader survey, Microsoft Inclusive Design toolkit (situational disability framing).
