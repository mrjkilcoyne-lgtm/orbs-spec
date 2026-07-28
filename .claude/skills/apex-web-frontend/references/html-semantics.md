# HTML Semantics

## Scope
Structuring documents with meaningful elements as the foundation of accessibility, SEO, and resilient styling.

## Core principles
- Semantics are an API contract with browsers, assistive tech, and crawlers: `<button>` gives focus, keyboard, and role for free; a clickable div gives nothing.
- Document outline first: one h1, landmarks (header/nav/main/footer), heading levels that never skip.
- Native elements before ARIA: the first rule of ARIA is don't use ARIA when an element exists.
- Forms are semantic machinery: label-for, fieldset/legend, correct input types unlock validation, mobile keyboards, autofill.
- HTML is fault-tolerant by design; work with the parser (valid nesting) rather than against it.

## Apex practices
- Write the page without CSS first mentally: if the raw document reads sensibly, the structure is right.
- Use `<dialog>`, `<details>`, `<time>`, `<figure>` — modern semantics that replace div-and-script contraptions.
- Validate with the Nu checker in CI; broken nesting causes real parser reinterpretation.
- Test with a screen reader occasionally; semantics claims meet reality there.

## Pitfalls
- div/span soup with click handlers reimplementing buttons and links badly.
- Multiple h1s and skipped heading levels wrecking the outline.
- Placeholder text used as the only label.

## Tools & references
MDN HTML reference, W3C Nu validator, HTMHell (anti-pattern catalog), web.dev/learn/html.
