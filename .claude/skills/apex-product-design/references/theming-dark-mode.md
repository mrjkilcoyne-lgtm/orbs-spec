# Theming & Dark Mode

## Scope
Supporting multiple themes and dark mode: color mapping, contrast preservation, and implementation patterns.

## Core principles
- Dark mode isn't just inverting colors; it's remapping a color system where light surfaces become dark and vice versa — requires a systematic approach, not a filter.
- Contrast constraints are tighter in dark mode: light text on dark is harder on eyes than dark text on light — ensure 4.5:1 contrast on both.
- Themes should be defined as variables, not scattered hardcoded colors — variable-based theming enables dynamic theme switching and proper implementation.
- Some colors change role in dark mode: secondary background becomes lighter to maintain hierarchy, while text becomes lighter to preserve contrast.
- User preference (prefers-color-scheme) should be detected and respected; force dark mode on users who prefer light causes accessibility issues.

## Apex practices
- Define two complete color systems (light and dark) with all roles mapped; test both in context, not in isolation.
- Use CSS custom properties (variables) or design tokens to implement theming; makes switching themes a single property change.
- Test contrast in both themes; tools like WebAIM Contrast Checker work for both modes.
- Respect user OS preference; app-level theme override should be available, but default to OS setting.

## Pitfalls
- Inverting colors as "dark mode"; it looks cheap and contrast often fails.
- Not testing dark mode early; discovering dark mode contrast issues late is expensive to fix.
- Force dark mode on users who prefer light; include a theme toggle, not a one-way switch.

## Tools & references
CSS custom properties, Figma variables with themes, Design Tokens for theme definition, prefers-color-scheme media query, Color Contrast Checker; "Dark Mode Design" best practices.
