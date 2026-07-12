# Localization & Translation

## Scope
Adapting content for different languages and cultures: translation quality, cultural sensitivity, and maintaining tone across locales.

## Core principles
- Translation is not word-for-word substitution; it's capturing intent in the target language's idiom. A literal translation often sounds wrong or offensive.
- Cultural context matters: colors, images, numbers (13, 4), gestures, and time formats vary by region. What works in US English may alienate or confuse elsewhere.
- Tone and voice are fragile across languages; humor especially is culture-bound. A pun untranslatable; irony requires trust in the relationship.
- String length expands/contracts across languages (German ≈ 20% longer, Chinese ≈ 20% shorter); UI layouts and copy must accommodate this.
- Quality tiers exist: machine translation (fast, cheap, noisy) → outsourced translation (human, slower, inconsistent terminology) → native-speaker review (gold standard, expensive).

## Apex practices
- Use pseudolocalization (replace text with gibberish of similar length) to test layouts before translating; catching UI breakage is cheaper than fixing translations.
- Maintain a glossary (key terms in all locales) to ensure consistency across documents.
- Have native speakers review for cultural appropriateness, not just linguistic correctness.
- Date, currency, and number formats must respect locale (1,000.50 in US, 1.000,50 in EU).

## Pitfalls
- Machine translation without review; it's good for gisting but inaccurate for public-facing content.
- Treating all locales as "translations of English"; idiom, formality, and structure vary. European Spanish ≠ Latin American Spanish.
- Over-localizing; some tone (brand voice) should persist; balance localization against consistency.

## Tools & references
XLIFF format (translation interchange), Crowdin / Lokalise (translation management), Unicode normalization, CLDR (Common Locale Data Repository).
