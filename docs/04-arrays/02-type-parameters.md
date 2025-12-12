# Type Parameters

TypeScript offers two syntaxes for declaring array types: the bracket notation `T[]` and the generic type parameter syntax `Array<T>`. Both are equivalent and you'll see both in real-world code.

## Two Equivalent Syntaxes

The bracket notation and generic syntax are interchangeable:

```typescript
// Using bracket notation
function assignColors(name: string, colors: string[]): void {
  // Implementation...
}

// Using generic type parameter syntax
function assignColors(name: string, colors: Array<string>): void {
  // Implementation...
}
```

Both function declarations are identical in behavior and type safety.

## Variable Declarations

Use either syntax when declaring variables:

```typescript
// Bracket notation (preferred)
const colors: string[] = [
  "blue",
  "green",
  "purple",
  "red",
  "orange",
  "white",
  "black",
];

// Generic syntax
const measurements: Array<number> = [
  1000, 5000, 12000, 20000, 27000, 40000,
];
```

Both declarations are equally valid. Choose whichever feels more natural to your team.

## When to Use Each Syntax

### Bracket Notation (`T[]`)

**Advantages:**
- Visually resembles an array with square brackets
- Faster to type
- More concise and readable
- Preferred in most TypeScript codebases

```typescript
const scores: number[] = [95, 87, 92];
const users: User[] = [...];
const flags: boolean[] = [true, false];
```

### Generic Syntax (`Array<T>`)

**Advantages:**
- Consistent with other generic types
- Useful when working with complex generic types
- May feel more familiar if coming from languages like Java or C#

```typescript
const data: Array<Record<string, unknown>> = [...];
const promises: Array<Promise<string>> = [...];
const callbacks: Array<(x: number) => string> = [...];
```

## Complex Types

For complex element types, either syntax works, but choose based on readability:

```typescript
// Union types
const mixed1: (string | number)[] = [];
const mixed2: Array<string | number> = [];

// Function types
const handlers1: ((event: Event) => void)[] = [];
const handlers2: Array<(event: Event) => void> = [];

// Object types
const users1: { name: string; id: number }[] = [];
const users2: Array<{ name: string; id: number }> = [];
```

## Nested Arrays

Both syntaxes can represent nested arrays:

```typescript
// Bracket notation
let matrix1: number[][] = [[1, 2], [3, 4]];
let matrix2: string[][] = [["a", "b"], ["c", "d"]];

// Generic syntax
let matrix3: Array<Array<number>> = [[1, 2], [3, 4]];
let matrix4: Array<Array<string>> = [["a", "b"], ["c", "d"]];

// Mixed (avoid - confusing)
let matrix5: Array<number[]> = [[1, 2], [3, 4]];
```

## Best Practices

**Prefer `T[]` notation because:**
- It's more concise and readable
- It's the dominant style in TypeScript communities
- The square brackets visually represent an array
- It's slightly faster to type

**Use `Array<T>` when:**
- You're defining complex generic types (we'll cover this later)
- Your team has established a standard for complex types
- You need consistency with other generic syntax in your codebase

## Real-World Examples

```typescript
// API response handling
const apiData: string[] = [];
const users: Array<User> = [];

// Event handlers
const listeners: ((event: Event) => void)[] = [];
const promises: Array<Promise<Response>> = [];

// Configuration
const ports: number[] = [3000, 3001, 3002];
const environments: Array<"dev" | "test" | "prod"> = [];
```

## Summary

- `T[]` and `Array<T>` are equivalent
- `T[]` is preferred for its simplicity and readability
- `Array<T>` becomes more useful when working with advanced generics
- Choose consistency within your codebase

Both syntaxes are valid. The choice is largely about consistency and readability rather than correctness.