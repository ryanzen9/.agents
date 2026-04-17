---
paths:
  - "*.java"
---

# Java Lint Rules

When reviewing Java code, enforce these conventions for type safety, readability, and robustness.

**Naming:** Classes use PascalCase. Methods and variables use camelCase. Constants use UPPER_SNAKE_CASE. Packages use lowercase.

## Constraints

**1. Null Safety:**
- Use `Optional<T>` for return values that may be absent. Never return `null` from public methods when `Optional` is viable.
- Use `@Nullable` / `@NonNull` annotations for method parameters and fields.
- Check external inputs (API responses, DB results) for null before use.

**2. Immutability by Default:**
- Prefer `final` for fields, parameters, and local variables when the value doesn't change.
- Use `List.of()`, `Map.of()`, `Set.of()` for immutable collections. Return unmodifiable views from getters.
- Prefer records (`record`) for simple data carriers (Java 16+).

**3. Exception Handling:**
- Never catch `Exception` or `Throwable` broadly — catch specific exception types.
- Don't swallow exceptions with empty catch blocks. At minimum, log the error.
- Use custom exceptions for domain-specific error conditions. Include context in the message.
- Prefer unchecked exceptions for programming errors; checked exceptions for recoverable conditions.

**4. Stream & Collection Usage:**
- Prefer Stream API for transformations and filtering over manual loops when it improves readability.
- Don't over-chain — if a stream pipeline exceeds 4-5 operations, extract intermediate steps into named variables or methods.
- Use `var` (Java 10+) when the type is obvious from context, not when it obscures intent.

**5. Class Design:**
- One public class per file. Keep classes focused on a single responsibility.
- Prefer composition over inheritance. Use interfaces for polymorphism.
- Keep methods short (< 30 lines guideline). Extract when a method does more than one thing.
- Use dependency injection over static singletons for testability.

**6. Concurrency:**
- Document thread-safety guarantees (or lack thereof) on public classes.
- Use `java.util.concurrent` utilities over raw `synchronized` / `wait` / `notify`.
- Mark shared mutable state with `volatile`, `Atomic*`, or proper synchronization.

**7. Logging & Debugging:**
- Use SLF4J / Logback (or project-standard logger), never `System.out.println` in production code.
- Use parameterized messages (`log.info("User {} logged in", userId)`) over string concatenation.