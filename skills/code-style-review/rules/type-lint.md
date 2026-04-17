---
paths:
  - "*.ts"
---

# Type Lint Rules

When reviewing code or writing new features, strictly enforce TypeScript type-checking conventions to ensure the type safety, robustness, and maintainability of the code.

**Type Safety First:** Ensure that all variables, function parameters, component Props, and return values have explicit or inferable types.
**Type Simplicity:** Type declarations should not be overly nested. For excessively deep nesting, `any` can be appropriately used for optimization.
**Accurate Type Definition:** Type declarations should be explicit and specific, with complete property definitions.
**Leverage Type Inference:** Fully utilize TS's automatic type inference capabilities to avoid redundant explicit declarations (e.g., `let count: number = 0` should be written directly as `let count = 0`).

## Constraints

**1. Choosing Between `interface` and `type`:**
- Prioritize using `interface` to declare objects, API responses, and class structures, making it easier to extend and utilize the Declaration Merging feature.
- Use `type` to declare primitive type aliases, Union types, Intersection types, and complex utility types.

**2. Strict Null Handling:**
- Adhere to the `strictNullChecks` convention and properly handle potential `null` or `undefined` values.
- When accessing properties that might be empty or calling methods that might not exist, you must use the optional chaining operator (`?.`) and the nullish coalescing operator (`??`) to avoid `Cannot read properties of undefined` errors.

**3. Type Reuse and Derivation:**
- Avoid repeatedly copying and pasting the same structures across different files. Extract common business types into dedicated `types` or `interfaces` directories.
- Make good use of built-in TypeScript utility types (such as `Pick<T, K>`, `Omit<T, K>`, `Partial<T>`, `Record<K, T>`) to derive new types (like DTOs, update parameters, etc.) based on existing core business entities.

**4. Type Assertions at External Data Boundaries:**
- For dynamic data coming from API requests (API Responses) or local storage (`localStorage`), explicit interface types must be defined. Whenever possible, combine them with Type Guards or validation libraries like Zod to verify structures at runtime. Use forced assertions (`as Type`) cautiously.
