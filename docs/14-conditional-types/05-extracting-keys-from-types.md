## Extracting keys from types

Mapped types dont just let you build new object types  you can also use them together with conditional types to _extract_ keys that match some condition.

Start with a simple object type:

```ts
type Soldier = {
	name: string;
	age: number;
	branch: "garrison" | "military police" | "survey corps";
};
```

Imagine you want a union of just the keys whose values are `string`. One way to do this is to first build a helper mapped type that keeps the key name when the value type matches, and otherwise produces `never`:

```ts
type StringKeys<T> = {
	[K in keyof T]: T[K] extends string ? K : never;
};

type Result = StringKeys<Soldier>;
/*
type Result = {
	name: "name";
	age: never;
	branch: "branch";
}
*/
```

Now we can turn that object type into a union of its values by indexing it with `keyof T`:

```ts
type StringKeyUnion<T> = StringKeys<T>[keyof T];

type Keys = StringKeyUnion<Soldier>;
//    ^? "name" | "branch"
```

This pattern  _"map, then index"   is a common way to use conditional and mapped types together:

- The mapped type `StringKeys<T>` walks over every property key `K` in `T` and conditionally keeps it or replaces it with `never`.
- Indexing with `keyof T` (`StringKeys<T>[keyof T]`) collects all of those property values into a single union.

By changing the condition inside `StringKeys<T>`, you can extract keys for numbers, booleans, arrays, and more.

