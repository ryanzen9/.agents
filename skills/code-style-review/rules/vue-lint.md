---
paths:
  - "*.vue"
---

# Vue Lint Rules

When reviewing Vue code, enforce these conventions for consistency and maintainability.

**API Style:** Prefer Composition API (`<script setup>`) for new code. Options API is acceptable in existing codebases that use it consistently.

**Naming:** Components use PascalCase in script, kebab-case or PascalCase in templates. Props use camelCase in script, kebab-case in templates. Events use kebab-case.

## Constraints

**1. Component Organization (`<script setup>`):**
- Order: imports → props/emits → reactive state → computed → watchers → functions → lifecycle hooks.
- Keep `<script setup>` concise. Extract complex logic into composables (`use*.ts`).

**2. Props & Emits:**
- Always define props with explicit types using `defineProps<T>()` (TS) or `defineProps({ ... })` with validators.
- Always declare emits with `defineEmits`. Never use `$emit` without declaration.
- Props are read-only — never mutate them directly.

**3. Reactivity:**
- Use `ref` for primitives, `reactive` for objects. Don't mix unnecessarily.
- Never destructure `reactive` objects without `toRefs` — it breaks reactivity.
- Use `computed` for derived values, not `watch` + manual assignment.
- Avoid unnecessary watchers — prefer `computed` when the value is purely derived.

**4. Template Best Practices:**
- Never use `v-if` and `v-for` on the same element (`v-if` takes precedence and can cause confusion).
- Always provide a unique `:key` on `v-for` elements using stable IDs, not array indices.
- Prefer `v-show` over `v-if` for frequently toggled elements (avoids re-mount cost).

**5. Composables:**
- Composables must start with `use` prefix and return a clear interface.
- Keep composables pure — accept arguments, return reactive state, avoid side effects in the module scope.
- Composables should be independently testable.

**6. Scoped Styles:**
- Always use `<style scoped>` unless global styles are intentionally needed.
- Avoid deep selectors (`:deep()`) unless styling third-party component internals.