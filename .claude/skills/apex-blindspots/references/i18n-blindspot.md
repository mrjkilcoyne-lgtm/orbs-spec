# The i18n Blindspot

## Scope
The monolingual defaults that break software abroad — the assumptions themselves: about names, text, formats, directions, and cultural constants.

## Core principles
- Your locale feels like physics: word order, name structure (given+family), left-to-right flow, spaces between words, the Latin alphabet, MM/DD dates — each is a local custom experienced as a law of nature; i18n bugs are these assumptions meeting a world that never agreed to them.
- Names are the gateway blindspot: single-word names, family-name-first, no "middle name," characters outside ASCII, names longer than your VARCHAR(50) — the "Falsehoods About Names" list is a map of how deep locale assumptions run in ordinary schemas.
- Text operations are locale operations: uppercasing (Turkish dotless-ı breaks naive .toUpper()), sorting (Swedish ö after z, not after o), truncating (mid-grapheme emoji corruption), searching (accent sensitivity) — string code without a locale parameter is wrong somewhere.
- Concatenation is the grammar killer: "You have " + n + " new messages" hardcodes English word order and plural logic; languages reorder sentences and have up to six plural forms — full-sentence templates with ICU plural rules or the string is untranslatable.
- Layout mirrors and expands: German labels run +35%, RTL scripts flip the entire visual flow (including icon direction where meaning is directional), CJK needs different line-breaking — a pixel-perfect English layout is a broken layout in waiting.

## Detection tests
- Run pseudo-localization (àçčéñťéd, 40% longer, bracketed): what truncates, overflows, or stays untranslated (hardcoded)?
- Flip to an RTL locale: does the layout mirror sensibly or shatter?
- Feed the system a name like "Björk" alone, "王小明", and a 60-character Thai name: what breaks?

## Countermeasures
- Externalize every user-visible string from day one with ICU MessageFormat; ban concatenation of translated fragments in lint.
- Use Intl/ICU APIs for all formatting (dates, numbers, currency, lists, plurals, collation) — never hand-rolled patterns.
- Design layouts with logical properties and flexible sizing; test the +35% and RTL cases in the design tool, not after translation delivery.

## Tools & references
CLDR/ICU, "Falsehoods Programmers Believe About Names," pseudo-localization tooling, ECMA-402 Intl, Unicode segmentation (UAX #29).
