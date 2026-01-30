# Generics

Generics are how you write **reusable, type‑safe code** in TypeScript.

Instead of hard‑coding a single type into a function, class, or object type, you add one or more **type parameters** (like `T` or `InputType`) and let callers plug in the concrete types they need. TypeScript then tracks those types all the way through your code.

You’ve already used generics in the standard library:

- `Array<T>` – arrays of `T` (e.g. `Array<number>`)
- `Promise<T>` – async values that eventually yield a `T`
- Utility types like `Partial<T>`, `Readonly<T>`, `Record<K, T>`, `Pick<T, K>`, `Omit<T, K>`

This chapter walks through how to **create and use your own generics**.

## What You’ll Learn

- **[01 – Generics](01-generics.md)**  
	Introduces generic functions and type parameters using a `fetchFromApi<T>` helper. You’ll see how `<T>` lets you keep precise result types (`Comment[]`, `User`, `Post[]`, etc.) without copying logic or falling back to `any`.

- **[02 – Multiple Type Parameters](02-multiple-type-parameters.md)**  
	Shows how to use more than one type parameter with a `transform<InputType, OutputType>` function (a typed `map`). You’ll reuse the same function for different input/output combos (e.g. `Human → string`, `number → number`).

- **[03 – Generic Constraints](03-generic-constraints.md)**  
	Adds constraints like `T extends HasCost` so your generic functions can safely assume certain properties exist. You’ll see how this lets you write helpers (like `applyDiscount`) that work for any type “with a `cost`”, while rejecting incompatible shapes.

- **[04 – Type Parameters for Types](04-type-parameters-for-types.md)**  
	Moves beyond functions to **generic object types**. You’ll build a `Store<T>` interface and reuse it for different domains (`Product`, `Homunculus`, …) while keeping implementations and helpers like `addAndGetItems` fully type‑safe.

- **[05 – Generic Type Inference](05-generic-type-inference.md)**  
	Shows that you rarely need to write type arguments at call sites. Using the `transform` example, you’ll see how TypeScript infers `InputType` and `OutputType` from the arguments you pass, and when you might still specify them explicitly.

- **[06 – Generic Classes](06-generic-classes.md)**  
	Applies the same ideas to classes. You’ll build an `InMemoryRepository<T>` that implements a generic `Repository<T>` interface, with a constraint `T extends { id: string }`. This demonstrates reusable, type‑safe behavior across many object types.

Taken together, these sections show how generics let you:

- Extract common patterns into **reusable building blocks**.
- Preserve **rich, specific types** instead of falling back to `any`.
- Scale your codebase without duplicating logic for every new type that comes along.

