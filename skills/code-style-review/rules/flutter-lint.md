---
paths:
  - "*.dart"
---

# Flutter / Dart Lint Rules

When reviewing Dart and Flutter code, enforce these conventions for consistency, performance, and maintainability.

**Naming:** Classes, enums, typedefs use PascalCase. Variables, functions, parameters use camelCase. Constants use camelCase (Dart convention, not UPPER_SNAKE). Libraries and file names use snake_case.

## Constraints

**1. Widget Structure:**
- Keep `build()` methods short and readable. Extract sub-trees into separate widgets or builder methods when they exceed ~80 lines.
- Prefer `StatelessWidget` unless you need mutable state. Use `StatefulWidget` only when `setState` is required.
- Prefer `const` constructors for widgets that don't depend on runtime values — enables framework-level rebuild optimization.

**2. State Management:**
- Choose one state management approach per project and use it consistently (Provider, Riverpod, Bloc, etc.).
- Don't mix `setState` with external state management in the same widget. Pick one.
- Keep business logic out of widgets — extract to controllers, services, or state notifiers.

**3. Null Safety:**
- Leverage Dart's sound null safety. Prefer non-nullable types by default.
- Use `late` only when you can guarantee initialization before access. Prefer nullable + null check otherwise.
- Avoid `!` (null assertion operator) — it defeats null safety. Use `??`, `?.`, or explicit null checks.

**4. Dart Idioms:**
- Use `final` for variables that aren't reassigned.
- Prefer collection literals (`[]`, `{}`) over constructors (`List()`, `Map()`).
- Use cascade notation (`..`) for chaining multiple operations on the same object.
- Prefer `switch` expressions (Dart 3+) over if-else chains for pattern matching.

**5. Async / Concurrency:**
- Always handle errors in async code — use `try/catch` or `.catchError()`.
- Cancel subscriptions and streams in `dispose()` to prevent memory leaks.
- Prefer `async/await` over raw `Future.then()` chains for readability.

**6. Performance:**
- Use `const` wherever possible (widgets, values, constructors).
- Avoid rebuilding expensive widget subtrees — use `RepaintBoundary`, `const` widgets, or selective state management.
- Use `ListView.builder` for long lists, not `ListView(children: [...])`.

**7. Project Structure:**
- Organize by feature, not by type (prefer `features/auth/` over `widgets/`, `models/`, `services/`).
- Keep imports organized: dart core → packages → relative imports, separated by blank lines.
- Prefer relative imports within the same package.