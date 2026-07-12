# Color as Material

## Scope
Albers and Itten's discovery that color is relational, deceptive, and workable like a material — the practical physics and psychology of palettes.

## Core principles
- Color is never seen alone (Albers's law): the same hex value reads as two different colors on two different grounds — one color can be made to look like two, two like one. Every palette decision is therefore a decision about adjacencies, not swatches.
- Value does the structural work: compositions hold together in black-and-white or not at all; hue is emotional weather over a value skeleton. Check designs in grayscale before arguing about blue vs teal.
- Itten's seven contrasts are the complete lever set: hue, light-dark, cold-warm, complementary, simultaneous, saturation, and extension (proportion). Any color problem — dead palette, garish clash, vanishing button — is one of these contrasts set wrong.
- Proportion transforms identity (contrast of extension): the same five colors read as elegant at 70/20/5/4/1 distribution and as carnival at 20/20/20/20/20. A palette is colors plus their budget.
- Simultaneous contrast is the debugging key: neighboring colors push each other toward their complements — the gray that looks greenish beside red, the vibrating complementary edge. What you see is the interaction, not the value; trust measurement for consistency and eyes for effect.

## Apex practices
- Do Albers's core exercises with real UI colors: make one gray read as two on different app surfaces; it permanently recalibrates how you spec dark mode and elevation tints.
- Build palettes as value scales first (a 9-step light-to-dark ramp per hue), then choose hues — this is why systematic color scales (Material, Radix, Tailwind) work.
- Set the temperature strategy explicitly: dominant temperature + small opposite-temperature accent is the most reliable palette architecture (Rothko's hum, Hockney's pools, every good dashboard).
- Test under deployment conditions: sRGB vs P3, dark surroundings, night shift, colorblind simulations (8% of men), and print if relevant — color is device physics plus human variance, not a hex string.

## Pitfalls
- Picking colors in isolation on a white artboard, then shipping them onto dark, tinted, or image backgrounds.
- Saturation wars: every element at full chroma, so nothing is emphasized and everything vibrates.
- Meaning by hue alone (red=error) with no value/shape redundancy — fails colorblind users and gray-scale contexts.

## Tools & references
Albers "Interaction of Color" (do the plates, don't just read), Itten "The Art of Color," APCA/WCAG contrast math, Radix/Material color-scale generators, colorblindness simulators.
