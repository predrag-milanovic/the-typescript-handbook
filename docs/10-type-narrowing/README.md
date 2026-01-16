# Type Narrowing

Type narrowing is the process of refining types from broader to more specific as you write code. It's one of TypeScript's most powerful features, enabling better tooling support, clearer self-documenting code, and catching more errors at compile time.

## Overview

This section covers the essential techniques and concepts for working with type narrowing in TypeScript:

### Core Concepts

- **[Narrowing Types](./01-narrowing-types.md)** - Introduction to conditional narrowing and how TypeScript automatically refines types in control flow
- **[Unknown Type](./02-unknown-type.md)** - The safe alternative to `any` that forces explicit type checking
- **[Type Hierarchy](./03-type-hierarchy.md)** - Understanding how types are organized from widest to narrowest and assignability rules

### Narrowing Techniques

- **[Narrowing Using In](./04-narrowing-using-in.md)** - Property existence checks for discriminating object types
- **[Type Predicates](./05-type-predicates.md)** - Creating custom type guards with `value is Type` syntax
- **[Guard Clauses](./07-guard-clauses.md)** - Using early returns to narrow types and handle edge cases
- **[Exhaustive Checks](./06-exhaustive-checks.md)** - Ensuring all union variants are handled in switch statements

### Type Assertions (Use Sparingly)

- **[Type Assertion](./08-type-assertion.md)** - Using `as` to override TypeScript's type inference
- **[Double Assertion](./09-double-assertion.md)** - The escape hatch for asserting completely unrelated types
- **[Non-Null Assertion](./10-non-null-assertion.md)** - Using `!` to assert values aren't `null` or `undefined`

## Quick Reference

### Conditional Narrowing

TypeScript automatically narrows types in conditionals:

```typescript
type Response = { success: true; data: string } | { success: false; error: string };

function handleResponse(response: Response) {
  if (response.success) {
    // TypeScript knows: response is { success: true; data: string }
    console.log(response.data);
  } else {
    // TypeScript knows: response is { success: false; error: string }
    console.log(response.error);
  }
}
```

### The `unknown` Type

Use `unknown` instead of `any` for safer external data handling:

```typescript
function processData(data: unknown) {
  if (typeof data === "string") {
    return data.toUpperCase(); // ✅ Safe
  }
  throw new Error("Expected string");
}
```

### Type Hierarchy

Understanding assignability from narrower to wider types:

```
never → literals → unions → primitives → unknown
  ↑        ↑          ↑          ↑           ↑
narrowest                              widest
```

### Property Checks with `in`

Discriminate object types by checking property existence:

```typescript
type TextMsg = { content: string };
type ImageMsg = { imageUrl: string };
type Message = TextMsg | ImageMsg;

function display(msg: Message) {
  if ("content" in msg) {
    // TypeScript knows: msg is TextMsg
    console.log(msg.content);
  }
}
```

### Custom Type Guards

Create reusable type predicates for complex checks:

```typescript
function isString(value: unknown): value is string {
  return typeof value === "string";
}

function process(value: unknown) {
  if (isString(value)) {
    value.toUpperCase(); // ✅ TypeScript knows it's a string
  }
}
```

### Guard Clauses

Use early returns to narrow types and simplify control flow:

```typescript
function getName(name: string | null | undefined): string {
  if (name === null || name === undefined) {
    return ""; // or throw an error
  }
  // TypeScript knows: name is string
  return name.toUpperCase();
}
```

### Exhaustive Checks

Leverage TypeScript to ensure all union cases are handled:

```typescript
type Status = "idle" | "loading" | "success" | "error";

function getStatusMessage(status: Status): string {
  switch (status) {
    case "idle":
      return "Ready";
    case "loading":
      return "Loading...";
    case "success":
      return "Done!";
    case "error":
      return "Failed";
  }
  // TypeScript knows all cases are covered
  // Adding a new status will cause a compile error here
}
```

### Type Assertions (Use Cautiously)

Override TypeScript's inference when you have more information:

```typescript
// Basic assertion
const userId = route.query?.userId as string;

// Non-null assertion
const user = findUser(id)!; // Assert it's not null/undefined

// Double assertion (rarely needed)
const value = input as unknown as TargetType;
```

## Best Practices

1. **Prefer narrowing over assertions** - Use conditionals and type guards instead of `as` when possible
2. **Use `unknown` over `any`** - Force explicit type checking at I/O boundaries
3. **Design for exhaustiveness** - Structure unions so TypeScript catches missing cases
4. **Guard early, return early** - Handle edge cases at the start of functions
5. **Be specific with types** - Narrower types provide better tooling and catch more errors

## Key Takeaway

Type narrowing is about progressively refining what you know about a value as your code executes. Master these techniques to write safer, more maintainable TypeScript code that leverages the full power of the type system.
