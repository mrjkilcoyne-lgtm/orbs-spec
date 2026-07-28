# Forms & Validation

## Scope
Form UX, HTML form machinery, client+server validation architecture.

## Core principles
- Server validation is the truth; client validation is UX sugar over it — never trust the client, never make the server the first feedback.
- Use the platform: correct input types, autocomplete attributes, native constraint validation as the base layer.
- Validate at the right moment: onBlur for format errors, onSubmit for cross-field, inline-as-you-fix after first error ("reward early, punish late").
- Error messages say what's wrong and how to fix it, adjacent to the field, associated via aria-describedby.
- Every extra field costs conversion: justify each one; progressive profiling beats the mega-form.

## Apex practices
- One schema, two runtimes: define validation once (zod & co.) and run it client and server.
- Preserve user input on failure — wiping a form is the cardinal sin.
- Design the async states: submitting (disable double-submit), success, server-error with retry, field-level server errors mapped back.
- Test the unhappy paths: paste, autofill, IME input, back-button restore, and keyboard-only completion.

## Pitfalls
- Premature validation shouting at users mid-typing.
- Client-only validation "because the API validates too" — until it doesn't.
- Custom dropdowns/date pickers losing accessibility and mobile behavior that native ones had.

## Tools & references
MDN constraint validation, react-hook-form/TanStack Form, zod, GOV.UK form design patterns.
