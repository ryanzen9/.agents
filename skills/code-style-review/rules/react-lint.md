---
paths:
  - "*.tsx"
  - "*.jsx"
---

# React Lint Rules

When reviewing React code, enforce these conventions for consistency, performance, and maintainability.

**Component Structure:** Prefer functional components with hooks. Class components are only acceptable in legacy codebases that already use them.

**Naming:** Components use PascalCase. Hooks use `use` prefix. Event handlers use `handle` prefix (e.g., `handleClick`). Props interfaces use `ComponentNameProps`.

## Constraints

**1. Hooks Rules:**
- Never call hooks conditionally or inside loops.
- Custom hooks must start with `use` and encapsulate a single concern.
- Prefer `useMemo` / `useCallback` only when there's a measurable performance benefit — don't wrap everything by default.

**2. Component Size & Responsibility:**
- A component should do one thing. If it exceeds ~150 lines, consider splitting.
- Extract reusable logic into custom hooks, not utility functions that depend on React state.
- Keep render logic readable — extract complex JSX into named sub-components or variables.

**3. Props & State:**
- Destructure props in the function signature for clarity.
- Avoid prop drilling beyond 2 levels — use Context or composition instead.
- Derive state from props/other state when possible — don't duplicate with `useState`.
- Use `children` prop and composition over configuration props when layout flexibility is needed.

**4. Side Effects:**
- `useEffect` must have a clear, single purpose. One effect per concern.
- Always specify the dependency array. Missing deps cause stale closures; extra deps cause unnecessary re-runs.
- Clean up subscriptions, timers, and event listeners in the effect's return function.

**5. Key Prop:**
- Never use array index as `key` for lists that can be reordered, filtered, or modified.
- Keys must be stable, unique identifiers from the data.

**6. Event Handling:**
- Don't create inline arrow functions in JSX for handlers that are passed to child components (causes unnecessary re-renders).
- For simple handlers on native elements, inline arrows are acceptable.

**7. Conditional Rendering:**
- Prefer early return for guard clauses.
- Use ternary for simple two-branch rendering; extract to variables or sub-components for complex conditions.
- Beware of `&&` short-circuit with falsy numbers (`0 && <Component />` renders `0`).
