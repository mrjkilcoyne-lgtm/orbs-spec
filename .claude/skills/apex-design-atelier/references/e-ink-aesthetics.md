# E-Ink Aesthetics

## Scope
Designing for (and being inspired by) electrophoretic displays: monochrome, dithering, slow refresh, zero-power persistence — constraint as muse.

## Core principles
- E-ink's virtues are inversions of LCD's: reflective (sunlight improves it), bistable (a static image costs zero power), paper-calm (no flicker, no glow) — and its costs are inversions too: slow refresh, ghosting, limited grayscale. Design for what it is: a page, not a movie.
- The refresh hierarchy is the interaction model: full refresh (flash-to-black, clean slate) vs partial refresh (fast, accumulates ghosting) — great e-ink UX choreographs when to pay the flash (chapter turn, screen change) and when to tolerate ghosts (typing, cursor). Latency isn't hidden; it's scheduled.
- Grayscale is quantized (typically 16 levels or fewer): continuous tone must be dithered — ordered/Bayer (mechanical texture), error-diffusion/Floyd-Steinberg (photographic grain), or blue-noise (smoothest) — and the dither pattern becomes the work's texture, a visible aesthetic choice like halftone was for Pop art.
- Typography is the native art form: e-ink at 200-300 DPI with real contrast renders type as well as print — sturdy book faces, generous leading, ragged-right; the entire tradition of book typography applies unmodified.
- Slowness is a feature to design toward: an interface that updates rarely invites glanceability and calm (status boards, daily planners, ambient art) — the anti-notification aesthetic; the ideal e-ink design is one you check like a wall clock, not one you operate like a phone.

## Apex practices
- Design in 1-bit first: pure black/white with dither for midtones forces value discipline; add gray levels only where they earn legibility (the cave-pigment exercise, electrified).
- Choreograph refresh explicitly: batch updates, refresh regions, schedule full flashes at natural narrative breaks, and show progress with patterns that survive ghosting (growing bars, not fading spinners).
- Test in reflective conditions: e-ink contrast is ambient-dependent — judge designs on-device in lamplight and sunlight, never in a backlit simulator alone.
- Borrow the aesthetic even off-device: the e-ink look (paper white, ink black, dither texture, no gradients, no shadows) is a coherent, restful design language for reading-first products anywhere.

## Pitfalls
- Porting LCD interfaces straight over: animation-dependent affordances (spinners, smooth scroll, hover states) die on a 500ms refresh.
- Anti-aliased grays where crisp 1-bit edges were available — small type dissolves into fuzz.
- Fighting ghosting with constant full refreshes: the flashing screen is more disruptive than the ghosts.

## Tools & references
E Ink's developer guides, dithering literature (Floyd-Steinberg, Bayer, blue-noise), Kindle/reMarkable/Boox design patterns, book typography canon (Bringhurst "The Elements of Typographic Style").
