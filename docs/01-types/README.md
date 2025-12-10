# Types in TypeScript

This section covers the fundamentals of TypeScript's type system, from basic type annotations to type inference and the escape hatch of `any`.

## What is TypeScript?

TypeScript is a superset of JavaScript developed by Microsoft, meaning all JavaScript code is valid TypeScript. TypeScript adds **static typing** to JavaScript, enabling compile-time error checking for safer, more maintainable code.

The TypeScript compiler (`tsc`) validates your code and compiles it to JavaScript before execution. This catch bugs early and makes refactoring easier.

## Why TypeScript?

- **Catches bugs at compile time** before they reach production
- **Improves code readability** with explicit type contracts
- **Enables safer refactoring** with type-aware tooling
- **Better developer experience** with IDE autocomplete and documentation

## Topics

### [01. Basic Types](./01-basic-types.md)

Learn TypeScript's fundamental type system. Covers:
- Type annotations: `: string`, `: number`, `: boolean`, etc.
- Primitive types: `string`, `number`, `boolean`, `null`, `undefined`
- Type mismatch errors
- When to use explicit annotations

**Key takeaway**: Annotate types to create explicit contracts; TypeScript enforces them at compile time.

### [02. Type Inference](./02-type-inference.md)

Understand how TypeScript automatically infers types. Covers:
- Implicit type inference from variable values
- When inference is sufficient (local variables)
- When explicit annotations help (APIs, complex logic)
- Best practices for balancing inference and clarity

**Key takeaway**: Prefer inference for internal code; use annotations for public APIs and when you need an explicit contract.

### [03. Any](./03-any.md)

Learn about `any`, TypeScript's type escape hatch. Covers:
- What `any` means and why it exists
- Migration strategy: `.js` → `.ts` with `any`
- Gradually replacing `any` with specific types
- Why `any` is useful but should be minimized

**Key takeaway**: Use `any` during migrations to get TypeScript running; replace it with specific types over time.

## Quick Tips

1. **Use annotations for clarity**, not just to satisfy the compiler.
2. **Trust inference** for local variables and straightforward assignments.
3. **Annotate function parameters and return types** to document your API contract.
4. **Avoid `any`** in new code; use it strategically during migrations.
5. **Type errors are your friend** — they catch bugs before runtime.

## Type System Overview

| Concept | Example | Use Case |
|---------|---------|----------|
| Annotation | `const x: number = 5` | Explicit type contract |
| Inference | `const x = 5` | Local variables, clear intent |
| Any | `const x: any = ...` | Migrations, unknown types |
| Union | `string \| number` | Multiple possible types |
| Literal | `"north" \| "south"` | Restricted set of values |