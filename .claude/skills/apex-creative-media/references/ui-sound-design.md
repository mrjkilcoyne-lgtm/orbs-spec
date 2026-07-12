# UI Sound Design

## Scope
Audio feedback for interactive systems: clicks, confirmations, transitions, state changes, and using sound to make interfaces feel responsive and intuitive without being annoying.

## Core principles
- Sound provides confirmation: a click sound 50ms after a button press tells the user "it registered" — critical for remote/network delays; missing confirmation makes interfaces feel broken.
- Timbre (the tone quality) communicates meaning: high-pitched sounds feel light/fast, low sounds feel heavy/slow, metallic feels digital, soft feels organic — map sound to semantic.
- Duration matters for usability: a 200ms feedback sound is satisfying; a 2-second jingle is annoying after the hundredth time; optimize for frequency of exposure.
- Layering (multiple sound components: attack, sustain, decay) creates richness without heaviness; a single sine tone sounds cheap compared to a complex envelope with multiple frequencies.
- Mixing UI sound with ambient or music sound requires headroom: UI sounds should be clear without drowning out content or other audio.

## Apex practices
- Keep UI sounds short (50–500ms) and distinctive so they don't interfere with focus on the interface; let visual feedback be primary.
- Use consistent sonic branding: similar timbral characteristics across UI sounds so they feel cohesive (Apple's UI sound language is exemplary).
- Test in context with other sounds (game audio, ambient, speech); what sounds good solo might compete badly in mix.
- Provide muting/control for users; persistent UI sounds can be deeply annoying, especially in public or professional contexts.

## Pitfalls
- Over-sonifying every interaction: not every state change needs sound; reserve it for important confirmations and state changes.
- Using poorly-recorded, cheap-sounding samples; good UI sound requires attention to signal quality and processing.
- Ignoring loudness normalization; UI sounds should be consistent in perceived loudness (use LUFS targets), not just amplitude.

## Tools & references
Freesound, Epidemic Sound (royalty-free UI packs), JSFX (real-time synthesis in REAPER), Max/MSP (interactive sound), Apple's HIG audio guidelines, game audio middleware (Wwise, FMOD).
