# Functions in TypeScript

This section covers how to annotate and work with function types in TypeScript, from basic parameter and return type syntax to advanced patterns.

## Overview

Functions are first-class values in TypeScript, which means they have types too. Understanding function types helps you write safer, more maintainable code with clear contracts between callers and implementations.

## Topics

### [01. Function Type Syntax](./01-type-syntax.md)

Learn how to annotate function parameters and return types. Covers:
- Basic parameter and return type annotations
- Regular functions vs arrow functions
- Optional, default, and rest parameters
- Function overloads
- Generic functions

**Key takeaway**: Annotate parameters to clarify intent; consider inferring return types for short functions.

### [02. Inferred Return Types](./02-inferred-return-types.md)

Understand when and how TypeScript infers function return types. Covers:
- Simple inference (e.g., `const divide = (a, b) => a / b`)
- Async functions and `Promise<T>` inference
- When to prefer explicit return types (public APIs, complex logic)
- Generic helpers

**Key takeaway**: Prefer inference for internal helpers; use explicit return types for exported/critical functions.

### [03. Void](./03-void.md)

Explore the `void` type for functions that don't return meaningful values. Covers:
- Using `void` for side-effect-only functions
- Event handlers and callbacks
- Async functions with `Promise<void>`
- The difference between `void`, `undefined`, and `any`

**Key takeaway**: Use `void` to signal intent that a function is not meant to produce a meaningful value.

### [04. Function Types](./04-function-types.md)

Master function types as values. Covers:
- Function type syntax: `(param: type) => returnType`
- Type aliases for function types
- Assigning function types to variables
- Higher-order functions with generics
- Optional and default parameters in function types

**Key takeaway**: Use type aliases to name complex function signatures for clarity and reusability.

### [05. Type Alias](./05-type-alias.md)

Learn how to name and reuse complex types using `type`. Covers:
- Simplifying verbose function signatures
- Object types, union types, and generic aliases
- Benefits: readability, reusability, maintainability
- When to use type aliases

**Key takeaway**: Always use type aliases for types that appear multiple times or are complex.

### [06. Importing Types](./06-importing-types.md)

Understand how to import types cleanly and efficiently. Covers:
- `import type { ... }` syntax
- Why it's better (smaller bundles, clearer intent)
- Alternative inline syntax (`import { type User, ... }`)
- Best practices

**Key takeaway**: Always use `import type` for types to keep bundles lean and intent clear.