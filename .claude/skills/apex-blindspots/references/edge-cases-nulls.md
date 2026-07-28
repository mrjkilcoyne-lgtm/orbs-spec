# Edge Cases & Nulls

## Scope
The inputs and states that break "working" code: empty, zero, one, many, huge, negative, duplicate, missing, malformed, unicode, concurrent.

## Core principles
- The zero-one-many rule: behavior at 0 items, 1 item, and many items are three different features; code written against the "several items" mental image fails at the edges (empty list rendering, single-element dropdowns, 10k-row payloads).
- Null has multiple meanings that code conflates: not-yet-set, explicitly-cleared, not-applicable, unknown, and error — schema and API designs that give them one representation guarantee downstream misinterpretation.
- Boundaries are where bugs live: off-by-one at limits, the value exactly AT the threshold (is 100 "under 100"?), the last page of pagination, the second-to-last byte of the buffer — test the fence, both sides, and the fencepost.
- Text is an adversarial input format: empty string vs whitespace, combining characters, RTL marks, emoji (multi-codepoint graphemes), homoglyphs, 'null' the string, and names like O'Brien or 毛 — every string field meets all of these eventually.
- The world's data is dirtier than the schema: duplicates where "impossible", future timestamps in历史 data, negative quantities, floats that should be ints — validation at boundaries is the immune system, and "can't happen" is a TODO for production to disprove.

## Detection tests
- For each collection: what happens at exactly 0, 1, and 10,000?
- For each nullable field: which of the five null-meanings is this, and does every consumer agree?
- For each numeric input: zero, negative, MAX, MIN, NaN, and the exact boundary value?

## Countermeasures
- Property-based testing generates the edges you didn't imagine (Hypothesis/fast-check find the empty-string-with-BOM cases mechanically).
- Encode edge decisions in types where possible (NonEmptyList, Positive Int, Option vs nullable) — make the compiler remember what you'll forget.
- Keep an edge-case checklist per input type and run it in review: strings, numbers, collections, dates, IDs, files each have a known rogues' gallery.

## Tools & references
Hypothesis/QuickCheck/fast-check, "Falsehoods Programmers Believe About X" series (names, addresses, time), naughty-strings list, fuzzing.
