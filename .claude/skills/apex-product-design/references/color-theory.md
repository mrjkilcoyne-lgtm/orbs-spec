# Color Theory

## Scope
Color systems, harmony, contrast, cultural meaning, and accessible color design.

## Core principles
- Color harmony (complementary, analogous, triadic) is a starting point, not a rule; effective palettes often break harmony rules if they serve the product need.
- Contrast isn't just visual — it's cognitive: bright vs dark, warm vs cool, saturated vs muted all create visual separation and help organize information.
- Cultural color meanings vary; red is stop in the West, luck in China, danger in traffic globally — consider audience.
- WCAG contrast minimums: 4.5:1 for text, 3:1 for UI elements — test with contrast checkers; most designs fail at first pass.
- Saturation and brightness matter as much as hue; desaturated (pastel) palettes feel calm, saturated (vibrant) feel energetic.

## Apex practices
- Build color systems with variables (lightness, saturation, hue) rather than fixed hex values; scales (10-step, 5-step) work across contexts.
- Test colors in context: colors look different on different backgrounds and in different sizes — verify contrast and perception, not just theory.
- Use color sparingly for emphasis; if everything is colored, nothing stands out — let neutrals (grays) be the majority.
- Test color blindness: use tools like Color Blindness Simulator or Contrast Ratio checker (accessible color mode); avoid red/green as the only distinction.

## Pitfalls
- Applying color harmony rules rigidly; trust your eye over theory.
- Using color as the only way to differentiate information (red = error, green = success) — add icons, text, or patterns for redundancy.
- Bright colors for text or critical information; saturated colors are harder to read for extended periods.

## Tools & references
Coolors, Adobe Color, Chir.py for palette generation, Contrast Ratio checker, WebAIM color blindness simulator; "Interaction of Color" (Albers); HSL/HSV color models for systematic palette building.
