## Readonly Utility Type

[`Readonly<T>`](https://www.typescriptlang.org/docs/handbook/utility-types.html#readonlytype) creates a new type where all top-level properties of `T` are marked as [`readonly`](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes-func.html#readonly-and-const), preventing them from being reassigned after initialization.

```ts
interface UserProfile {
	id: string;
	name: string;
	preferences: {
		readonly theme: "light" | "dark";
		notifications: boolean;
	};
}

type ConstantUserProfile = Readonly<UserProfile>;

// This is the same as:
// type ConstantUserProfile = {
//   readonly id: string;
//   readonly name: string;
//   readonly preferences: {
//     readonly theme: "light" | "dark";
//     notifications: boolean;
//   };
// };
```

`Readonly` is **shallow**: it makes the top-level properties of `UserProfile` readonly, but it does not automatically make every nested property readonly. In this example, the `preferences` object itself is readonly (you can’t reassign `preferences`), but inside it only `theme` is readonly because it was declared that way in `UserProfile`.

Use `Readonly<T>` when you want to:

- expose immutable views of otherwise mutable objects
- prevent accidental reassignment of configuration or settings objects
- make API return values read-only to consumers

