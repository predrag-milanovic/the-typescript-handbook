# Conditional Types

Conditional types are one of TypeScript's most powerful **type‑level building blocks**. They let you say things like _"if this type extends that type, then produce this other type"_ entirely within the type system.

You’ll mostly see them in **libraries and reusable helpers** (often alongside generics and mapped types), but understanding the basics will also help you read and debug real‑world TypeScript code.

## What You’ll Learn

- **[01 – Conditional Types](./01-conditional-types.md)**  
	Introduces the core syntax `T extends U ? X : Y`, shows how to read conditional types like a ternary expression, and walks through practical helpers such as an `IsString<T>` check and filtering unions with utilities like `Extract`, `Exclude`, and `NonNullable`.

- **[02 – Infer](./02-infer.md)**  
	Explains the special `infer` keyword, which you can only use inside conditional types. You’ll build a `GetReturnType<T>` helper (a simplified `ReturnType<T>`) and see how `infer R` lets you capture and reuse parts of a matched type, like a function’s return type.

- **[03 – Mapped Types](./03-mapped-types.md)**  
	Builds up from index signatures to mapped types that transform object shapes. Using examples like `Soldier`, `OptionalSoldier`, and `Stringified<T>`, you’ll see how `[K in keyof T]` and `T[K]` let you create reusable helpers such as `Optional<T>` and `Stringified<T>`.

- **[04 – Mapped Types With Conditionals](./04-mapped-types-with-conditionals.md)**  
	Combines mapped types with conditional logic to selectively keep or change properties. You’ll write types like `FilteredSoldier` that keep only properties whose values satisfy a constraint (for example, all properties whose type extends `string`).

- **[05 – Extracting Keys From Types](./05-extracting-keys-from-types.md)**  
	Shows how to use the "map, then index" pattern—first creating a mapped type that marks some keys as `never`, then indexing with `[keyof T]`—to produce unions like _"all keys whose values are strings"_. This ties together conditionals, mapped types, and indexing to derive key unions from existing object types.

## Quick Reference

### Basic Conditional Type

```ts
// General form
type NewType<T> = T extends Condition ? TrueType : FalseType;

// Example
type IsString<T> = T extends string ? true : false;

type A = IsString<string>;  // true
type B = IsString<number>;  // false
```

### Inferring Inside Conditionals

```ts
// Extract a function's return type
type GetReturnType<T> = T extends (...args: any[]) => infer R ? R : never;

function greet() {
  return "hello";
}

type GreetReturn = GetReturnType<typeof greet>; // string
```

### Mapped Types and Conditionals

```ts
// Make all properties optional
type Optional<T> = {
  [K in keyof T]?: T[K];
};

// Keep only string-valued properties
type StringProperties<T> = {
  [K in keyof T]: T[K] extends string ? T[K] : never;
};

// Turn matching properties into a key union
type StringPropertyKeys<T> = StringProperties<T>[keyof T];
```

## When to Reach for Conditional Types

- When you need **derived types** that stay in sync with a source type (for example, all mouse events, all string properties, or non‑nullable fields).
- When you’re building **reusable helpers or libraries** that must work across many different input types.
- When the built‑in utilities (`Extract`, `Exclude`, `NonNullable`, `ReturnType`, `Partial`, etc.) get you partway there but you need a custom variation.

They are incredibly powerful, but they can also become hard to read. Prefer the **simplest type that clearly expresses your intent**, and reach for conditional types (and `infer`) when they give you a clear correctness or maintainability win.

