# Svelte

## Scope
Svelte 5 (runes) and SvelteKit: compiler-driven reactivity, minimal-runtime components.

## Core principles
- The compiler is the framework: components compile to targeted DOM updates, no virtual DOM diffing.
- Runes make reactivity explicit: $state for sources, $derived for computation, $effect for external sync — same discipline as other frameworks, finer syntax.
- $derived over $effect-writing-state: derivation is declarative and glitch-free; effect chains are the anti-pattern.
- Props go down, events/callbacks come up; bindable is deliberate two-way opt-in.
- SvelteKit's load/actions model: data fetching and mutation live on the server by default; the client enhances.

## Apex practices
- Keep $effect for true external systems (DOM APIs, subscriptions, analytics), and return cleanup functions.
- Use snippets/children for composition; context for dependency injection down deep trees.
- Progressive enhancement with form actions — apps that work before JS loads.
- Shared reactive state in .svelte.js modules — runes work outside components.

## Pitfalls
- Effect→state→effect cycles ("infinite loop" errors) from using effects as derivation.
- Assuming array/object mutation triggers updates in non-$state contexts.
- Fetching in components what SvelteKit load functions should own (waterfalls, no SSR data).

## Tools & references
svelte.dev docs + tutorial, SvelteKit docs, svelte-check, Svelte DevTools.
