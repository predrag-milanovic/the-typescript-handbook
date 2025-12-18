# Tuples

A tuple is a fixed-length array where each position has a specific type.

```ts
const cityLocation: [string, number] = ["Tokyo", 13960000];
```

Tuples are safer than arrays for small, structured collections because the length is fixed and each index has a known type.

## Be Explicit With Tuples

Always provide explicit tuple types. Without an annotation, TypeScript infers a general array type instead of a tuple.

```ts
// Tuple: [string, number]
const coordinates: [string, number] = ["Latitude", 40.7128];

// Array: (string | number)[]
const coordinates2 = ["Longitude", -74.0060];
```

An inferred array allows mutations that break the intended structure:

```ts
const productInfo = ["Laptop", 1299];
productInfo[1] = "Desktop"; // OK, but probably not what you want
```

With an explicit tuple type, TypeScript catches type mismatches:

```ts
const productInfo: [string, number] = ["Laptop", 1299];
// Error: Type 'string' is not assignable to type 'number'.
productInfo[1] = "Desktop";
```

Use tuples when you need a fixed structure with known types at each position.
