Conditional Types
=================

We're now getting into some pretty advanced stuff that, while very useful in tricky modelling situations, is not something you'll usually need in everyday application code.

As a general rule, advanced TypeScript features are more useful in **library code** that needs to be flexible, abstract, and reusable. Application-level TypeScript code is generally much simpler and more concrete...

[Conditional types](https://www.typescriptlang.org/docs/handbook/2/conditional-types.html) let us create **new types based on conditions** inside the type system itself.

Basic Syntax
------------

The general form of a conditional type looks like this:

```ts
type NewType = SomeType extends OtherType ? TrueType : FalseType;
```

You can read this just like a ternary expression in JavaScript:

> "If `SomeType` extends (satisfies) `OtherType`, then `NewType` is `TrueType`; otherwise, it's `FalseType`."

Simple Example: `IsString`
--------------------------

Here's a very small but clear example:

```ts
type IsString<T> = T extends string ? true : false;

// Usage
type Result1 = IsString<"hello">; // true
type Result2 = IsString<42>;       // false
type Result3 = IsString<string>;   // true
```

In this example, `IsString` is a conditional type that checks whether the type parameter `T` extends `string`. If it does, the resulting type is `true`; otherwise, it's `false`.

This might not look immediately useful on its own, but this same pattern powers a lot of the more advanced utility types in the standard library.

Built-in Conditional Utility Types
----------------------------------

TypeScript actually ships with some built-in conditional types. Here are three important ones (simplified):

```ts
type Extract<T, U> = T extends U ? T : never;
type Exclude<T, U> = T extends U ? never : T;
type NonNullable<T> = T extends null | undefined ? never : T;
```

Roughly speaking:

- [`Extract<T, U>`](https://www.typescriptlang.org/docs/handbook/utility-types.html#extracttype-union) keeps only the parts of `T` that are assignable to `U`.
- [`Exclude<T, U>`](https://www.typescriptlang.org/docs/handbook/utility-types.html#excludeuniontype-excludedmembers) removes from `T` anything that is assignable to `U`.
- [`NonNullable<T>`](https://www.typescriptlang.org/docs/handbook/utility-types.html#nonnullabletype) removes `null` and `undefined` from `T`.

We'll focus on [`Extract`](https://www.typescriptlang.org/docs/handbook/utility-types.html#extracttype-union) for a practical example.

Practical Example: Filtering Event Unions
----------------------------------------

As usual, the question is: **"When the heck is this useful?"**

Imagine we have some events that can fire in a front-end application:
```ts
type ClickEvent = { type: "click"; x: number; y: number };
type KeyEvent = { type: "key"; key: string };
type MouseMoveEvent = { type: "mousemove"; x: number; y: number };
type FormEvent = { type: "submit"; formId: string };

type Event = ClickEvent | KeyEvent | MouseMoveEvent | FormEvent;
```

It might be useful to **dynamically create a type** that only includes the "mouse-related" events – the ones that have both `x` and `y` properties. We can use the `Extract` conditional type to do that.

First, here’s the (simplified) implementation of `Extract` again, just for reference:

```ts
type Extract<T, U> = T extends U ? T : never;
```

Now we can use it to filter our `Event` union:
```ts
type MouseRelatedEvents = Extract<Event, { x: number; y: number }>;
```

`MouseRelatedEvents` is now the same as:
```ts
type MouseRelatedEvents = ClickEvent | MouseMoveEvent;
```

The key difference is that it's **dynamic**. If we add more events to the `Event` union in the future, `MouseRelatedEvents` will automatically include them as long as they match the condition (i.e., they have `x` and `y` properties).

This is where conditional types really shine: they let you express relationships *between* types so that when one type changes, the others automatically stay in sync.
