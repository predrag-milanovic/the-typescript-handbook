# Tuples

Tuples are fixed-length arrays where each position has a specific type. They provide a way to express structured data with known types at each index position.

```ts
const cityLocation: [string, number] = ["Tokyo", 13960000];
```

## Overview

This section covers all aspects of working with tuples in TypeScript:

1. **[Tuples](./01-tuples.md)** – Basics of defining and using tuple types with explicit annotations
2. **[Readonly](./02-readonly.md)** – Making tuples immutable with the `readonly` modifier
3. **[Tuples vs. Objects](./03-tuples-vs.-objects..md)** – When to use tuples versus object types
4. **[Destructuring Tuples](./04-destructuring-tuples.md)** – Extracting values from tuples with destructuring syntax
5. **[Named Tuples](./05-named-tuples.md)** – Labeling tuple elements for better readability
6. **[Optional Elements in Tuples](./06-optional-elements-in-tuples.md)** – Making tuple positions optional with `?`
7. **[Tuple Rest Elements](./07-tuple-rest-elements.md)** – Allowing variable-length tuple endings with `...` syntax

## Key Concepts

### Why Tuples Matter

Tuples are safer than plain arrays for small, structured collections because:
- Length is fixed and known
- Each index has a specific, expected type
- TypeScript can catch type mismatches at each position

### Always Be Explicit

Without explicit tuple annotations, TypeScript infers a general array type instead of a tuple:

```ts
// Tuple (with annotation): [string, number]
const coordinates: [string, number] = ["Latitude", 40.7128];

// Array (inferred): (string | number)[]
const coordinates2 = ["Longitude", -74.0060];
```

### Tuples vs. Objects

Choose tuples when order is conventional (e.g., `[latitude, longitude]`). Choose objects for named, self-documenting access (e.g., `{ lat, lng }`).

### Readonly by Default

Consider using `readonly` tuples to prevent accidental mutations:

```ts
const nameAndAge: readonly [string, number] = ["Martha", 24];
// nameAndAge.push("Extra"); // Error!
```

### Destructuring

Tuples work great with destructuring to name positional values:

```ts
const [firstName, lastName] = getName("Frodo Baggins");
```

### Advanced Features

- **Named tuples** – Add labels to positions for clarity
- **Optional elements** – Mark positions as `?` (must be at the end)
- **Rest elements** – Use `...type[]` for variable-length endings
