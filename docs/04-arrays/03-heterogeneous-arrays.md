# Heterogeneous Arrays

Heterogeneous arrays contain elements of different types. TypeScript handles this elegantly by using union types, allowing you to create arrays that mix multiple types safely.

## What Are Heterogeneous Arrays?

A heterogeneous array contains values of different types. Unlike languages that require all array elements to be the same type, TypeScript allows mixed-type arrays through union types:

```typescript
// TypeScript infers the type as (string | number)[]
let mixedValues = [1, 2, "hello", "world"];

// Explicit type annotation
let data: (string | number)[] = [42, "text", 100, "more"];
```

## Type Inference

TypeScript automatically infers union types from mixed-type array literals:

```typescript
// Inferred as (string | number)[]
const values = [1, "two", 3, "four"];

// Inferred as (string | boolean)[]
const flags = ["active", true, "inactive", false];

// Inferred as (number | null)[]
const numbers = [1, 2, null, 4];
```

## Working with Heterogeneous Arrays

When iterating over a heterogeneous array, you need to handle all possible types:

```typescript
function process(item: string | number): void {
  if (typeof item === "string") {
    console.log(`Text: ${item.toUpperCase()}`);
  } else {
    console.log(`Number: ${item * 2}`);
  }
}

const data: (string | number)[] = [10, "hello", 20, "world"];
data.forEach(process);
// Number: 20
// Text: HELLO
// Number: 40
// Text: WORLD
```

## Real-World Scenarios

### API Response Data

```typescript
// Mixed response data from an API
const responseData: (string | number | boolean)[] = [
  "success",
  200,
  true,
  "request_id_123",
  true,
];
```

### Configuration Arrays

```typescript
// Configuration with mixed types
const config: (string | number | boolean)[] = [
  "development",
  3000,
  true,
  "localhost",
  false,
];

function applyConfig(value: string | number | boolean): void {
  console.log(`Applying: ${value}`);
}

config.forEach(applyConfig);
```

### Event Data

```typescript
// Events with variable data
const logEntry: (string | number | Date)[] = [
  "error",
  500,
  new Date("2025-12-12"),
];

function logEvent(entry: string | number | Date): void {
  if (typeof entry === "string") {
    console.log(`Level: ${entry}`);
  } else if (typeof entry === "number") {
    console.log(`Code: ${entry}`);
  } else {
    console.log(`Time: ${entry.toISOString()}`);
  }
}

logEntry.forEach(logEvent);
```

## Multiple Type Handling

For arrays with more than two types, ensure you handle all cases:

```typescript
// Three-type union
const mixed: (string | number | boolean)[] = [
  "text",
  42,
  true,
  "more text",
  100,
];

function handleMixed(value: string | number | boolean): void {
  if (typeof value === "string") {
    console.log(`String: ${value.length} chars`);
  } else if (typeof value === "number") {
    console.log(`Number: ${value}`);
  } else {
    console.log(`Boolean: ${value ? "true" : "false"}`);
  }
}

mixed.forEach(handleMixed);
```

## Common Patterns

### Tuple Alternative

For a fixed number of known types, consider tuples instead:

```typescript
// Heterogeneous array (variable length, mixed types)
const array: (string | number)[] = ["a", 1, "b", 2];

// Tuple (fixed length, specific types per position)
const tuple: [string, number, string] = ["a", 1, "b"];
```

### Type Guards

Use type guards for safer type narrowing:

```typescript
function isSting(value: string | number): value is string {
  return typeof value === "string";
}

const data: (string | number)[] = ["hello", 42, "world"];

data.forEach((item) => {
  if (isString(item)) {
    console.log(item.toUpperCase());
  } else {
    console.log(item * 2);
  }
});
```

## Best Practices

**Be Explicit**: Always annotate heterogeneous arrays explicitly:

```typescript
// Good - clear intent
const mixed: (string | number)[] = [1, "two", 3];

// Avoid - too permissive
const vague: any[] = [1, "two", 3];
```

**Minimize Union Size**: Keep unions manageable:

```typescript
// Good - two types
const pair: (string | number)[] = [];

// Challenging - five types (hard to handle all cases)
const complex: (string | number | boolean | null | undefined)[] = [];
```

**Use Type Narrowing**: Always check types before using type-specific operations:

```typescript
function process(value: string | number) {
  // error: value might be number
  // console.log(value.toUpperCase());

  // correct: check type first
  if (typeof value === "string") {
    console.log(value.toUpperCase());
  }
}
```

## When to Use Heterogeneous Arrays

**Good use cases:**
- Processing API responses with mixed data
- Configuration arrays with various settings
- Event data with different property types
- Collections where element types vary logically

**Avoid when:**
- You can use typed objects or interfaces instead
- You have a fixed structure (use tuples)
- Types are too numerous (simplify or use classes)

## Summary

- Heterogeneous arrays use union types: `(T | U | V)[]`
- TypeScript infers union types from mixed-type literals
- Always use type guards to safely handle mixed types
- Consider tuples for fixed-length, fixed-type structures
- Keep unions simple and manageable for code clarity

Heterogeneous arrays give you the flexibility of dynamic languages while maintaining TypeScript's type safety.