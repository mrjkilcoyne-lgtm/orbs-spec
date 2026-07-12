# Image Editing

## Scope
Post-processing and manipulation: color grading, retouching, compositing, and non-destructive workflows to refine captured or created images.

## Core principles
- Non-destructive editing (layers, adjustment layers, smart objects) preserves optionality: you can undo, adjust, and experiment without degrading the original or committing to a choice.
- Editing is not fixing; it's amplifying intent. The edit should be invisible (so subtle the viewer doesn't see editing, only the final image) or intentional (style that serves the story).
- Color spaces and bit depth matter: editing in 16-bit or 32-bit preserves tonality and avoids banding; working in sRGB vs. Adobe RGB affects color range and export implications.
- Histograms and clipping indicators show you what you can't see on a monitor alone; relying on the image on screen is guessing, not precision.
- Retouching is an ethical statement: removing blemishes or distracting elements is enhancement; changing body shape or removing people is manipulation — the line matters.

## Apex practices
- Set up a non-destructive workflow from the start: work on adjustment layers, use layer masks instead of erasing, save working files in editable formats (PSD, TIFF).
- Use curves, not brightness-contrast, for tonal adjustments — curves give you pixel-level control and reveal tonal distribution at a glance.
- Retouch on a separate layer with a specific tool (clone, healing, inpaint) so you can control opacity and easily undo isolated fixes.
- Proof on multiple monitors or color-calibrated devices and export in the target color space (sRGB for web, Adobe RGB for print); monitor calibration is non-negotiable for color work.

## Pitfalls
- Over-sharpening or over-processing — the goal is refinement, not Instagram-filter style transformation (unless intentional).
- Editing on an uncalibrated monitor and being shocked by color shifts in other contexts.
- Destructive editing (flattening, direct pixel manipulation) that traps you in past decisions.

## Tools & references
Adobe Lightroom (non-destructive, batch), Photoshop (compositing, retouching), Capture One (color grading, tethering), GIMP (open-source), Affinity Photo; color management: ICC profiles, ColorChecker.
