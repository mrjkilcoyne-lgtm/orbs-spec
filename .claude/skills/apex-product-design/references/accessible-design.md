# Accessible Design

## Scope
Inclusive design: WCAG standards, contrast, keyboard navigation, screen readers, and designing for diverse abilities.

## Core principles
- Accessibility isn't a feature, it's a baseline; designs that work for everyone (vision, hearing, motor, cognitive disabilities) benefit all users.
- WCAG 2.1 has three levels (A, AA, AAA); AA is the standard (4.5:1 contrast, large touch targets, keyboard navigation); AAA is enhanced (7:1 contrast).
- Keyboard navigation enables use without a mouse; every interactive element must be reachable via Tab and have visual focus indicators.
- Screen readers (VoiceOver, NVDA) read content aloud; semantic HTML (headings, lists, landmarks) and descriptive alt text make content accessible.
- Color isn't enough; distinguish information by shape, text, or pattern — color-blind users (8% of men, 0.5% of women) must perceive all information.

## Apex practices
- Design with accessibility in mind from the start, not as an afterthought — retrofitting is expensive.
- Test with real screen readers (VoiceOver on Mac/iPhone, NVDA on Windows, Narrator) — usability insights differ from testing with sighted users.
- Ensure minimum 44x44 px (iOS) or 48 dp (Android) touch targets; smaller targets are frustrating for everyone, impossible for people with motor disabilities.
- Test with browser accessibility checkers (axe, Lighthouse) and manual testing; automated tools find 60–70% of issues, manual testing finds the rest.

## Pitfalls
- Using color alone to convey information (red = error, green = success) — add icons, text, or patterns.
- Low-contrast text (very common in fashionable "light gray on white" designs) — verify 4.5:1 ratio.
- Keyboard traps (keyboard can't reach an element or can't escape) — test Tab navigation without a mouse.

## Tools & references
WCAG 2.1 guidelines, axe DevTools, Lighthouse (Chrome), NVDA / VoiceOver, Color Contrast Checker; "Inclusive Components" blog; A11y Project resources.
