Mapped Types
============

Remember **dynamic properties**?

```ts
type UserMetrics = {
	[key: string]: number;
};
```

This kind of type is called an **index signature** – it says:

> "For *any* string key, the value will be a `number`."

[Mapped types](https://www.typescriptlang.org/docs/handbook/2/mapped-types.html) are a more precise and powerful version of this idea.

Instead of allowing *any* key, a mapped type lets us create **new types with dynamic properties based on the keys of an existing type**.

From `Soldier` to `OptionalSoldier`
------------------------------------

Say we have a `Soldier` type:

```ts
type Soldier = {
	name: string;
	age: number;
	branch: "garrison" | "military police" | "survey corps";
};
``;

Now imagine we want a new type with **the same properties**, but where **all of them are optional**. We *could* write it out by hand, but that would be repetitive and easy to forget to update later.

Instead, we can use a **mapped type**:

```ts
type OptionalSoldier = {
	[K in keyof Soldier]?: Soldier[K];
};
```

Let’s break that down:

- `keyof Soldier` gets the **union of keys** of `Soldier` → `"name" | "age" | "branch"`.
- `K in ...` iterates over each of those keys.
- The `?` after the property name makes each property **optional**.
- `Soldier[K]` looks up the **value type** for each key in `Soldier`.

The result is exactly the same as writing:

```ts
type OptionalSoldier = {
	name?: string;
	age?: number;
	branch?: "garrison" | "military police" | "survey corps";
};
```

The big win is that if we **add, remove, or change** properties on `Soldier`, the `OptionalSoldier` type **automatically stays in sync**.

Changing the Value Types
------------------------

Mapped types are often used to make properties `optional` or `readonly`, but they can also **change the value type entirely**.

For example, we can create a version of `Soldier` where every property is a `string`:

```ts
type StringifiedSoldier = {
	[K in keyof Soldier]: string;
};
```

Which is equivalent to:

```ts
type StringifiedSoldier = {
	name: string;
	age: string;
	branch: string;
};
```

Again, this stays **automatically up to date** if `Soldier` changes, because it's defined in terms of `keyof Soldier` and its keys.

Generic Mapped Types
--------------------

In real-world code, we usually turn patterns like this into **reusable generic helpers**:

```ts
// Make all properties of T optional
type Optional<T> = {
	[K in keyof T]?: T[K];
};

// Turn all property values into strings
type Stringified<T> = {
	[K in keyof T]: string;
};

type OptionalSoldier2 = Optional<Soldier>;
type StringifiedSoldier2 = Stringified<Soldier>;
```

Many of TypeScript's built‑in utility types (like `Partial<T>` and `Readonly<T>`) are built using this same **mapped type** pattern.

