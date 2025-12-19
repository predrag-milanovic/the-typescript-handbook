# Objects

Objects are fundamental to TypeScript. This section covers object literal types, structural typing rules, advanced patterns like discriminated unions, and practical tools for working with object data structures.

## Contents

1. **[Object Literal Types](01-object-literal-types.md)** — Define the shape and structure of objects with type aliases and inline annotations.

2. **[Extra Properties](02-extra-properties.md)** — Understand how TypeScript's excess property checking differs between variables and object literals.

3. **[Optional Object Properties](03-optional-object-properties.md)** — Use the `?` operator to make properties optional and handle `undefined` safely.

4. **[Empty Object Type](04-empty-object-type.md)** — Learn why `{}` behaves unexpectedly and how to define proper empty objects.

5. **[Discriminated Unions](05-discriminated-unions.md)** — Use tagged unions with discriminant properties to handle multiple object shapes safely.

6. **[Sets](06-sets.md)** — Work with typed `Set<T>` collections that enforce unique values.

7. **[Maps](07-maps.md)** — Use `Map<K, V>` for type-safe key-value pairs with flexible iteration.

8. **[Dynamic Keys](08-dynamic-keys.md)** — Define objects with unknown property names using index signatures.

9. **[Dynamic Default Properties](09-dynamic-default-properties.md)** — Combine index signatures with required properties for flexible yet constrained types.

10. **[PropertyKey](10-propertykey.md)** — Use the built-in `PropertyKey` union to accept string, number, and symbol keys.

11. **[Readonly Modifier](11-readonly-modifier.md)** — Prevent property reassignment with the `readonly` modifier.

12. **["As Const" and Object.freeze](12-as-const-and-object.freeze.md)** — Create deeply readonly types with `as const` and compare with runtime `Object.freeze()`.

13. **[Satisfies](13-satisfies.md)** — Validate object structure without widening types using the `satisfies` operator.

14. **[Function Overloads](14-function-overloads.md)** — Constrain parameter combinations with function overload signatures.
