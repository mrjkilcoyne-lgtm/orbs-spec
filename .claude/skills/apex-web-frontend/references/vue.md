# Vue

## Scope
Vue 3: composition API, reactivity system, single-file components.

## Core principles
- Reactivity is proxy-based dependency tracking: reading in a reactive context subscribes; mutating triggers — understand this and most magic demystifies.
- ref vs reactive: refs for everything is the consistent style; .value is the price of explicitness.
- computed for derivation (cached, lazy), watch for side effects — using watch to derive state is the classic smell.
- SFCs align template/logic/style per component; the template compiler optimizes what JSX can't (static hoisting, patch flags).
- Composables (useX functions) are the reuse unit — composition API exists to make them possible.

## Apex practices
- `<script setup>` + TypeScript + defineProps/defineEmits with type syntax as the baseline.
- Keep reactive graphs shallow and explicit; destructuring reactive objects loses reactivity (toRefs when needed).
- Pinia for shared state — it's composables with devtools, not a Vuex ceremony revival.
- v-for always with :key; v-if and v-for never on the same node.

## Pitfalls
- Losing reactivity via destructure/spread of reactive() objects.
- Deep watchers on large objects as a performance foot-cannon.
- Mutating props (one-way data flow violation) instead of emitting.

## Tools & references
vuejs.org guide, Vue DevTools, Pinia, Vitest + Vue Test Utils.
