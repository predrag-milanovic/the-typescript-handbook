# Arrays

Typed arrays are foundational in TypeScript. This section covers array syntax, generic type parameters, mixing types safely, variadic functions with rest parameters, and the special "evolving any" inference.

## Topics

- [01. Arrays](./01-arrays.md): Basic `T[]` syntax, inference, methods, unions, readonly arrays, arrays of objects, generic `Array<T>` alternative, nested arrays, and common mistakes.
- [02. Type Parameters](./02-type-parameters.md): `T[]` vs `Array<T>`—equivalent syntaxes, when to use each, complex and nested types, and best practices.
- [03. Heterogeneous Arrays](./03-heterogeneous-arrays.md): Mix different element types with unions, type guards, tuple alternatives, real-world scenarios, and pitfalls.
- [04. Rest Parameters](./04-rest-parameters.md): Variadic functions using `...param: T[]`, mixing with unions/optionals, spread at call sites, tuples with rest, and common errors.
- [05. Evolving Any](./05-evolving-any.md): How empty arrays infer `any[]` and evolve as you push values; patterns to build internally and enforce types externally.

## Quick Reference

- `T[]`: Preferred array type syntax (concise, readable).
- `Array<T>`: Generic alternative, useful near other generics.
- `(A | B)[]`: Array of union element types; parentheses required.
- `readonly T[]`: Prevent mutations (no `push`, no index assignment).
- `...args: T[]`: Rest parameter collects trailing arguments into an array.
- Empty `[]`: Starts as `any[]`, evolves as values are pushed.

## Common Patterns

```typescript
// Arrays of objects
interface User { name: string; age: number }
const users: User[] = [{ name: "Ada", age: 36 }];

// Union element arrays
const values: (string | number)[] = ["id", 42];

// Readonly arrays
function logLevels(levels: readonly string[]) {
  console.log(levels.join(", "));
}

// Rest + spread
function sum(...nums: number[]): number {
  return nums.reduce((a, n) => a + n, 0);
}
const parts = [1, 2, 3] as const;
sum(...parts);

// Evolving any inside a builder function
function build(): (string | number)[] {
  const acc = [];
  acc.push("token");
  acc.push(8080);
  return acc; // inferred as (string | number)[] outside
}
```

## Best Practices

- Prefer `T[]` for readability; use `Array<T>` near other generics.
- Be explicit with union element arrays: `(A | B)[]` (use parentheses).
- Use `readonly` to signal immutability and prevent accidental mutation.
- Rest must be the last parameter; type it as `T[]`.
- Avoid `any[]` unless intentionally building a union—otherwise annotate the element type.
- Consider tuples for fixed-length, position-specific heterogeneous data.

Arrays in TypeScript combine JavaScript flexibility with compile-time safety. Use the right syntax and patterns to keep your collections clear, efficient, and maintainable.
