Utility Types
=============

As a TypeScript codebase grows, it’s easy to end up with many slightly different versions of the same shape – "user without id", "user for updates", "user response", and so on. Instead of copy‑pasting these variants, TypeScript’s **utility types** let you **derive** them from a single source of truth.

This chapter walks through the most commonly used built‑in utilities and shows how they help you keep your types DRY, expressive, and safe.

- **[Single Source of Truth](./01-single-source-of-truth.md)** – introduces the idea of defining core types once and building everything else from them.
- **[`Partial<T>`](./02-partial-utility-type.md)** – makes all properties optional, perfect for "update" or "patch" shapes derived from an existing type.
- **[`Required<T>`](./03-required-utility-type.md)** – does the opposite of `Partial`, forcing all top‑level properties to be present.
- **[`Readonly<T>`](./04-readonly-utility-type.md)** – turns all top‑level properties into `readonly`, great for immutable views and configuration.
- **[`Record<K, T>`](./05-record-utility-type.md)** – builds strongly‑typed dictionaries and lookup tables from a key type `K` and value type `T`.
- **[`Pick<T, K>`](./06-pick-utility-type.md)** – creates a focused view of a type by selecting a subset of its properties.
- **[`Omit<T, K>`](./07-omit-utility-type.md)** – the inverse of `Pick`, producing a type by excluding specific properties (for example, to strip sensitive fields before returning API responses).

Together, these utilities form a toolkit for transforming existing types into the exact shapes you need, without sacrificing type safety or maintainability.
