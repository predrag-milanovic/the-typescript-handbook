Using JavaScript Libraries
==========================

When you start a new TypeScript project, it’s easy to imagine that you’ll have perfect type safety everywhere.

Then reality hits: you’re asked to `npm install` a JavaScript library that doesn’t ship with type definitions.

What do you do when that happens?

You generally have three options:

1. **Let `any` flow through your code** (fast, but you lose type safety).
2. **Create your own type definitions** for the library.
3. **Use community-maintained types** from [DefinitelyTyped](https://github.com/DefinitelyTyped/DefinitelyTyped).

DefinitelyTyped is a large, community-driven repository of type definitions for popular JavaScript libraries. In practice, your first step should be to check there, usually via an `@types/...` package on npm.

However, this handbook is about understanding how things work under the hood, so let’s focus on **writing your own type definitions** for an existing JavaScript library.


Creating a `.d.ts` file for an external module
---------------------------------------------

Suppose you’re using a JavaScript package called `pregnantgoku` that is published on npm but has no type declarations.

You can teach TypeScript about this package by adding a declaration file alongside your code. For example, create a file called `pregnantgoku.d.ts` somewhere in your project that’s picked up by TypeScript (e.g. inside `src` or another included folder) and write:

```ts
declare module "pregnantgoku" {
	export function kamehameha(target: [number, number]): void;

	export type Saiyan = {
		name: string;
		monthsAlong: number;
		powerLevel: number;
	};
}
```

Now when you write code like this:

```ts
import { kamehameha, Saiyan } from "pregnantgoku";

const goku: Saiyan = {
	name: "Goku",
	monthsAlong: 9,
	powerLevel: 9001,
};

kamehameha([0, 1]);
```

TypeScript will use the declarations from `pregnantgoku.d.ts` to type-check your usage.


Declaration files for internal JavaScript modules
-------------------------------------------------

Sometimes you’re not consuming a third-party package from `node_modules`, but rather a JavaScript file that lives inside your own project, for example `pregnantgoku.js`.

In that case, you can create a sibling declaration file called `pregnantgoku.d.ts` that exports the same surface area as your JavaScript module:

```ts
export function kamehameha(target: [number, number]): void;

export type Saiyan = {
	name: string;
	monthsAlong: number;
	powerLevel: number;
};
```

Because these are **file-based** declarations, you don’t need the `declare module "..." {}` wrapper. TypeScript will automatically match `pregnantgoku.d.ts` to `pregnantgoku.js` and use the types whenever you import from that file.


Summary
-------

- Prefer existing types from DefinitelyTyped when they’re available.
- When they aren’t, you can write your own `.d.ts` files to describe JavaScript libraries.
- Use `declare module "name" { ... }` for packages from `node_modules`.
- Use plain `export` declarations in a `.d.ts` file that sits next to a JavaScript file in your own project.

