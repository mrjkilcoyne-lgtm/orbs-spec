# Interaction Design

## Scope
Designing interactions: affordances, feedback, state changes, gestures, and how users perceive and engage with interface elements.

## Core principles
- Affordance is the perception of an object's properties and possible actions; a button should look clickable, a slider should look draggable — if an affordance is unclear, users don't interact correctly.
- Feedback confirms user action immediately; clicking a button with no response is confusing (was it registered?); haptic, visual, or auditory feedback reassures.
- State (enabled, disabled, hover, focus, active, loading) should be visually distinct; disabled buttons are dimmed, loading shows a spinner, focus shows a border for keyboard navigation.
- Gestures (swipe, pinch, drag) are powerful on touch but non-discoverable; pair with visual affordance (small swipe cue) and offer alternative interactions (buttons).
- Response time < 100 ms feels instant, 100–1000 ms is acceptable, > 1 s feels slow — for long operations, show progress (loading bar, spinner).

## Apex practices
- Design interactive states (hover, focus, active, disabled, loading, error) for every element; test keyboard navigation to ensure all states are visible.
- Use visual consistency in interactive elements; if a button changes on hover, other buttons should too.
- Provide multiple interaction methods; don't rely on gestures alone — offer buttons as alternative.
- Test interactions with users; some gestures (swipe right to go back) are platform-dependent and non-obvious.

## Pitfalls
- Interactive elements without clear affordances (underline text looks like a link, unclickable text doesn't) cause confusion.
- No feedback on interaction; a button that doesn't respond or change on click feels broken.
- Gestures that conflict with system gestures (swiping a list item vs iOS back swipe) confuse users and break navigation.

## Tools & references
Figma interactions, principle, Framer for interactive prototypes; "The Design of Everyday Things" (Norman); platform-specific gesture conventions (iOS HIG, Android Material Design).
