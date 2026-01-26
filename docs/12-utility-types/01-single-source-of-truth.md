Single Source of Truth
======================

As a TypeScript codebase grows, it’s incredibly common to accumulate a *lot* of custom type definitions – hundreds of interfaces and type aliases that all describe roughly the same concepts, but with slightly different shapes.

For example, you might see something like this:

```ts
interface User {
	id: string;
	name: string;
	email: string;
	age: number;
}

interface UserWithoutId {
	name: string;
	email: string;
	age: number;
}
```

This is not ideal. We’re duplicating information: if we ever add, remove, or change a field, we now need to remember to do it in multiple places. Instead, we generally want to follow a [**single source of truth**](https://en.wikipedia.org/wiki/Single_source_of_truth) approach.

In this simple example, we can refactor by defining the common shape once and then building on top of it:

```ts
interface UserWithoutId {
	name: string;
	email: string;
	age: number;
}

interface User extends UserWithoutId {
	id: string;
}
```

Now `UserWithoutId` is our source of truth for the shared fields, and `User` simply extends it with an `id`. If we later decide to add a `username` field or remove `age`, we only need to update `UserWithoutId`. The `User` type automatically stays in sync.

The rest of this chapter will introduce utility types and type transformations that let you apply this idea more systematically. The goal is to define core types once, then derive the variants you need — so when requirements change, you can update a single definition and have the rest of your type system follow along.

