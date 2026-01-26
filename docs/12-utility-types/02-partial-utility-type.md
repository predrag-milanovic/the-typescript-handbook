Partial Utility Type
====================

TypeScript includes several built-in [*utility types*](https://www.typescriptlang.org/docs/handbook/utility-types.html) that transform existing types into new ones. One of the most common and useful of these is [`Partial<T>`](https://www.typescriptlang.org/docs/handbook/utility-types.html#partialtype), which makes **all properties of a type optional**.

Consider this `User` type:

```ts
type User = {
	id: string;
	name: string;
	email: string;
};
```

Imagine we want a function that can update any subset of a user’s fields. Without `Partial<T>`, we might write something like this:

```ts
// Without Partial
function updateUser(
	userId: string,
	userInfo: {
		id?: string;
		name?: string;
		email?: string;
	},
) {
	// ...
}
```

This works, but it duplicates the `User` type structure and will quickly fall out of sync if `User` changes.

With `Partial<T>`, we can instead derive the type from `User` directly:

```ts
// With Partial
function updateUser(userId: string, userInfo: Partial<User>) {
	// ...
}
```

Now we have a *single source of truth*: `Partial<User>` is automatically updated whenever `User` changes. If we add a `username` field to `User`, `updateUser` will immediately accept `username` as an optional property too.

In other words, `Partial<T>` lets us generate a new type from an existing one, instead of copy/pasting and maintaining multiple versions by hand.

Nested Objects
--------------

It’s important to understand that `Partial<T>` only makes the **top-level properties** of `T` optional; it does **not** recursively make nested properties optional.

For example:

```ts
type User = {
	id: string;
	name: string;
	preferences: {
		theme: string;
		notifications: boolean;
	};
};
```

If we use `Partial<User>`, the resulting type looks like this:

```ts
// same as 'type LooseyGooseyUser = Partial<User>'
type LooseyGooseyUser = {
	id?: string;
	name?: string;
	preferences?: {
		theme: string;
		notifications: boolean;
	};
};
```

Here, `id`, `name`, and `preferences` are optional. But **inside** `preferences`, the `theme` and `notifications` properties are still required whenever `preferences` itself is present.


