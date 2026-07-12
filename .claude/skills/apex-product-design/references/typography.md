# Typography

## Scope
Font selection, type scales, readability, and accessibility in text design.

## Core principles
- Typeface personality (serif, sans-serif, script) sets tone; serif is traditional, sans-serif is modern/clean, script is decorative — choose one that matches the brand voice.
- Font size, line-height, and line-length interact to determine readability; 16–18px font, 1.5–1.6 line-height, 60–80 character line length is readable for body text.
- Type scales (proportional sizes: 12, 14, 16, 20, 24, 32px) create hierarchy and consistency; random sizes feel disjointed.
- Font weight (regular, medium, bold) adds nuance; using weight instead of size for hierarchy saves font requests and improves performance.
- Contrast between text and background must be ≥4.5:1 for normal text (WCAG AA), ≥7:1 for enhanced (AAA) — test with contrast checkers.

## Apex practices
- Limit typeface choices to 2–3 maximum; one serif + one sans-serif, or one highly versatile sans-serif with multiple weights.
- Use system fonts (SF Pro, Roboto) as defaults; they're fast, accessible, and feel native — custom fonts require loading time and can fail.
- Create a type scale and apply it consistently; Figma type libraries help enforce this.
- Test text at actual sizes and line lengths; a 14px font at 120 characters per line is hard to read, even if it's technically valid.

## Pitfalls
- Using decorative fonts for body text; readability suffers and file sizes bloat.
- Ignoring color contrast; low-contrast text fails WCAG standards and is hard to read.
- Font stacks that vary drastically between devices; specify fallbacks that have similar metrics (x-height, width) to prevent layout shifts.

## Tools & references
Google Fonts, FontPair, Contrast Ratio checker, Figma type libraries, system fonts (SF Pro, Roboto, Inter); "Thinking with Type" (Lupton); Variable fonts for weight flexibility.
