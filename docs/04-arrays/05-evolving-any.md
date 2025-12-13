# Evolving Any

When you create a new empty array, TypeScript infers it as `any[]`. As you push values into it, the array's element type evolves to include the types of the pushed values.

## Basic Behavior

```typescript
let inventory = [];
// inventory: any[]

inventory.push(42);
// inventory: number[]

inventory.push("robe");
// inventory: (number | string)[]
```

If you explicitly type the array, TypeScript enforces that constraint:

```typescript
let numbers: number[] = [];
numbers.push("robe");
// Error: Argument of type 'string' is not assignable to parameter of type 'number'
```

## What Is "Evolving Any"?

"Evolving any" is a special type inference behavior for empty array literals. The array starts as `any[]`, then narrows as values are added, accumulating a union of all inserted element types.

- Starts as `any[]`
- After first push of a `T`: becomes `T[]`
- After subsequent pushes of different types: becomes `(T | U | ...)[]`

This is convenient when building arrays progressively, but it doesn't help restrict inputs within the immediate scope of construction.

## Useful Pattern: Build Internally, Enforce Externally

Evolving any shines when you construct an array inside a function, then return it. Outside the function, the resulting type is fixed, so further mutations must respect the inferred union.

```typescript
function getConfig() {
  let config = [];
  // config: any[]
  config.push("api-key");
  // config: string[]
  config.push(8080);
  // config: (string | number)[]
  return config;
}

const cfg = getConfig();
// cfg: (string | number)[]

cfg.push(false);
// Error: Argument of type 'boolean' is not assignable to parameter of type 'string | number'
```

Inside `getConfig`, you can push various types freely, and TypeScript evolves the type. Once returned, the element type is locked to the inferred union, preventing incompatible pushes.

## Best Practices

- Prefer explicit types for public APIs to avoid surprises:
  
  ```typescript
  const items: Array<string | number> = [];
  ```

- Use evolving any for local array construction where flexibility helps, then return a well-defined union.
- Avoid starting arrays as `any[]` if you already know the intended element type — annotate directly for clarity.

## Common Pitfalls

- Starting with `any[]` may hide mistakes during construction. If the array is meant to be homogeneous, annotate it:
  
  ```typescript
  const ids: number[] = [];
  ```

- Evolving any applies specifically to empty array literals. If initialized with values, TypeScript infers from those values instead:
  
  ```typescript
  const mixed = [1, "two"]; // inferred as (number | string)[]
  ```

## Summary

- Empty arrays start as `any[]` and evolve as values are pushed.
- Explicit annotations enforce element types immediately.
- Construct flexibly inside functions, but rely on the inferred union outside to maintain type safety.
