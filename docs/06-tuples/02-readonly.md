# Readonly

Tuples in TypeScript are still arrays under the hood, so counterintuitively you can still push to them and pop from them. This is a bit of a gotcha, tuples in most languages are fixed length.

```ts
const nameAndAge: [string, number] = ["Martha Jones", 24];
nameAndAge.push("Donna Noble");
```

So you still need to be careful about underlying array length... that is, unless you use [readonly](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes-func.html#readonly-and-const) tuples, which is really the only way I use tuples.

```ts
const nameAndAge: readonly [string, number] = ["Martha Jones", 24];
// Error: Property 'push' does not exist on type 'readonly [string, number]'.
nameAndAge.push("Donna Noble");
```

Much better! I use `readonly` any time I possibly can, its kinda like using `const` over `let` whenever possible. However, keep in mind that `readonly` is TypeScript specific, which means it's enforced at compile time, but not at runtime (like `const` is).
