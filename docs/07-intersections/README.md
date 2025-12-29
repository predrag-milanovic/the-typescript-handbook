# Intersections

Intersection types combine multiple types into one using the `&` operator, creating a type that must satisfy all component types simultaneously. This chapter explores how intersections work, their relationship to unions, and important edge cases to watch for.

## Contents

1. **[Intersections of Types](01-intersections-of-types.md)** - Learn how to combine multiple types using the `&` operator and merge object properties
2. **[The Never Type](02-the-never-type.md)** - Understand how `never` helps ensure exhaustive case handling
3. **[Intersecting Incompatible Types](03-intersecting-incompatible-types.md)** - Discover what happens when intersecting types with conflicting properties
4. **[Intersections vs. Unions](04-intersections-vs-unions.md)** - Learn when to use `&` versus `|` for combining types
5. **[Super Set Unions](05-super-set-unions.md)** - Master the technique for providing autocomplete hints while accepting any string value

## Quick Reference

### Basic Intersection Syntax

```ts
type A = { x: number };
type B = { y: string };
type C = A & B; // { x: number; y: string; }
```

### Intersections vs. Unions

| Feature | Intersection (`&`) | Union (`\|`) |
|---------|-------------------|--------------|
| Operator | `&` (AND) | `\|` (OR) |
| Effect | Narrows type | Widens type |
| Result | Must satisfy ALL types | Must satisfy ANY type |
| Use case | Combine requirements | Alternative options |

### Key Concepts

- **Intersection types** require values to satisfy all component types simultaneously
- **The `never` type** represents impossible values and helps catch unhandled cases
- **Incompatible intersections** result in `never` when property types conflict
- **Super set unions** like `"a" | "b" | (string & {})` provide autocomplete while accepting any string

## Common Patterns

### Combining Object Types

```ts
type Person = {
  name: string;
  age: number;
};

type Employee = {
  id: number;
  department: string;
};

type EmployeePerson = Person & Employee;
// Has all properties: name, age, id, department
```

### Exhaustive Type Checking with `never`

```ts
function handleStatus(status: "success" | "error" | "pending") {
  if (status === "success") return "✓";
  if (status === "error") return "✗";
  if (status === "pending") return "...";
  
  // Ensures all cases handled
  const exhaustive: never = status;
  return exhaustive;
}
```

### Super Set Union for Autocomplete

```ts
type StatusCode = 200 | 404 | 500 | (number & {});
// Accepts any number but suggests 200, 404, 500 in autocomplete
```

## When to Use What

**Use Intersections (`&`) when you want to:**
- Combine multiple object types
- Add properties to an existing type
- Create a type that must satisfy multiple constraints
- Model "this AND that"

**Use Unions (`|`) when you want to:**
- Represent alternative options
- Model "this OR that"
- Create types with multiple possible shapes
- Narrow primitive types to specific literals

## Important Notes

**Incompatible Property Types**: When intersecting types with the same property name but different types, the result is `never` if the types can't be satisfied simultaneously.

**Never Type Safety**: Use `never` assignments to ensure all union cases are handled exhaustively. The compiler will error if cases are missing.

**Union Widening**: Unlike intersections, unions widen the set of possible values. Choose based on whether you need more or fewer possible values.
