# Empty States & Error UX

## Scope
Designing for edge cases: empty states, loading states, errors, and 404s with empathetic messaging and clear guidance.

## Core principles
- Empty states aren't failures; they're opportunities to guide users toward next steps (create first item, invite friends, upgrade plan).
- Error messages should be specific (not "Error"), explain why it happened, and suggest action (not a blank error code).
- Loading states (spinners, skeletons, progress bars) reduce perceived wait time; 0–1 s feels instant, 1–10 s needs progress indication, >10 s needs cancel option.
- 404s and permission errors are common but often dismissive; use them to clarify what happened and offer alternatives (search, homepage, contact support).
- Messages should use plain language, avoid jargon, and match the user's mental model (not internal error codes).

## Apex practices
- Design empty states proactively in wireframes; they're not afterthoughts.
- Test error messages with users; what's clear to the developer ("Status code 403") is gibberish to users ("Access denied. Contact your admin" is better).
- Provide context in loading states; instead of just "Loading," show "Syncing 3 of 10 items" to give users confidence.
- Use illustrations and tone in empty states to match brand voice; a playful app's empty state should be playful, not generic.

## Pitfalls
- Showing technical error messages to users (error codes, stack traces).
- Empty states with no guidance (blank page says "No data" but doesn't explain how to add data).
- Loading spinners with no indication of how long to wait; users assume it's broken after a few seconds.

## Tools & references
Error state design patterns, Basecamp error pages (famous for personality), Figma empty state templates; "Don't Make Me Think" (Krug); A11y Project for accessible error handling.
