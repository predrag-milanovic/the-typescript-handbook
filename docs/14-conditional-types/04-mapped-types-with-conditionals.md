Mapped Types With Conditionals
==============================

If mapped types are a step toward type-level wizardry, **conditional mapped types** are one step further.

They’re powerful and genuinely useful in some situations – but they can also become hard to read if you’re not careful. As always with advanced type features: use them when they clearly improve correctness or maintainability, not just because they’re clever.

Starting Point: `OptionalSoldier`
---------------------------------

From the previous section, recall our `Soldier` and `OptionalSoldier` types:

```ts
type Soldier = {
	name: string;
	age: number;
	branch: "garrison" | "military police" | "survey corps";
};

type OptionalSoldier = {
	[K in keyof Soldier]?: Soldier[K];
};
```

`OptionalSoldier` is a **mapped type** that:

- Iterates over each key in `Soldier` with `K in keyof Soldier`.
- Uses `Soldier[K]` to get the value type for that key.
- Marks each property as optional with `?`.

Filtering Properties by Value Type
---------------------------------

What if, instead of making properties optional, we wanted to **filter out any non-string properties**?

In other words, we want a type that:

- Keeps only the properties whose value type is assignable to `string`.
- Drops everything else.

That’s exactly what **conditional mapped types** are for:

```ts
type FilteredSoldier = {
	[K in keyof Soldier]: Soldier[K] extends string ? Soldier[K] : never;
};
```

Here’s what’s happening inside the mapped type:

- For each key `K` in `keyof Soldier`:
	- We check the value type `Soldier[K]`.
	- If `Soldier[K] extends string`, we keep it as `Soldier[K]`.
	- Otherwise, we use `never`.

Because `never` is treated as "no possible value" in many mapped-type contexts, properties with `never` often end up effectively **filtered out** in downstream usage (for example, when indexing by the value type or combining with other mapped types).

The resulting type is:

```ts
type FilteredSoldier = {
	name: string;
	// age: never;
	branch: "garrison" | "military police" | "survey corps";
};
```

Two important details:

- `age` becomes `never` because `number` is not assignable to `string`.
- The `branch` property **keeps its specific union type**, not just `string`, because we checked `Soldier[K] extends string` and then *reused that same `Soldier[K]`* in the `true` branch of the conditional.

This pattern – using a conditional inside a mapped type and then reusing the more specific type – is very common in advanced utility types in the TypeScript standard library.

