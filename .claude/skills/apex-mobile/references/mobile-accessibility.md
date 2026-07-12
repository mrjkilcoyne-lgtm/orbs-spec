# Mobile Accessibility

## Scope
Making apps usable by everyone: screen readers (VoiceOver/TalkBack), touch targets, contrast, and inclusive design.

## Core principles
- VoiceOver (iOS) and TalkBack (Android) read UI aloud; every interactive element needs a label (accessibilityLabel) and hint if not obvious.
- Touch targets must be ≥44x44 pt (iOS) or 48x48 dp (Android) — smaller targets are frustrating for everyone, impossible for people with motor disabilities.
- Color contrast (foreground/background) should be ≥4.5:1 for normal text (WCAG AA), 7:1 for enhanced contrast (AAA) — test with a contrast checker.
- Screen readers need semantic structure: use native UI components (UIButton, Switch) which VoiceOver recognizes; custom components need accessibilityRole attributes.
- Keyboard navigation must work: every interactive element reachable via Tab + arrow keys (iOS) or Tab (Android) — test by navigating the app without touching the screen.

## Apex practices
- Enable VoiceOver/TalkBack while testing every flow; if you can't use your app without seeing it, neither can users with vision disabilities.
- Use native UI components whenever possible; they have built-in accessibility — avoid custom-drawn everything.
- Test with system text size settings (larger text) — scale text dynamically and avoid hard-coded sizes.
- Provide captions for videos and audio; audio descriptions for images not decorative.

## Pitfalls
- Hiding interactive elements but showing them to screen readers (or vice versa) creates confusion.
- Touch targets that are too small; cramming buttons together saves space but makes them inaccessible.
- Color-only differentiation (e.g., red = error, green = success) — add icons, text, or patterns.

## Tools & references
iOS accessibility guide, Android accessibility guide, WCAG 2.1 standards, Contrast Ratio checker, Accessibility Inspector (Xcode), Accessibility Scanner (Android); "Inclusive Components" blog.
