# Data Visualization

## Scope
Encoding data visually: choosing chart types, color palettes, marks, and interaction to make insights clear and false conclusions hard.

## Core principles
- Chart type follows the data's job: magnitude (bar/line), comparison (grouped bar), time-series (line), composition (stacked), relationships (scatter). Start with the question, not the template.
- Color has four jobs: categorical (identity—series A vs B), sequential (magnitude—low to high), diverging (polarity—loss to gain), and status (state—good/warning/bad). Each has one correct encoding rule; mixing them confuses the eye.
- Preattentive processing (what the eye reads before conscious thought) favors position > length > angle > area > color > texture. Top-accuracy encodings use position; avoid area/angle for precise comparison.
- Cognitive load increases with complexity; small multiples (many small charts) beat one crowded chart with a legend and dual axes (which is nearly always wrong).
- Dark mode is not an automatic flip; it requires separate color validation and slightly different saturation/lightness to maintain contrast and hierarchy.

## Apex practices
- Use the Diátaxis form heuristic: form (bar, line, etc.) → color by job → mark specs (thickness, rounding) → interaction (hover tooltip, filters).
- Validate color computationally, not by eye; run a CVD (color-vision-deficient) simulator and accessibility checker. Eyeballing fails at scale.
- Strip defaults: thin axes, muted grids, selective direct labels (label only key points), no chartjunk (3D, gradients, excessive borders).
- Include a table view alongside charts for precise reading; charts are for patterns, tables are for numbers.

## Pitfalls
- Rainbow palettes (common but harmful): they waste perceptual bandwidth, don't sort naturally, and fail for colorblind viewers.
- Dual-axis charts: they enable arbitrary correlation stories (scale one axis to match the other's noise). Use small multiples instead.
- Treating defaults as best practices; most visualization tools default to heavy gridlines, large fonts, and noisy styling that distract from data.

## Tools & references
Tufte's "The Visual Display of Quantitative Information," Wilkinson's "The Grammar of Graphics," Colorbrewer (categorical/sequential/diverging palettes), CVD simulator (coblis.cehd.uh.edu).
