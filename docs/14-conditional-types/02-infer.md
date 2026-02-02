Infer
=====

The [`infer` keyword](https://www.typescriptlang.org/docs/handbook/2/conditional-types.html#inferring-within-conditional-types) is a special feature you can only use **inside a conditional type**. It lets you *capture* a type from the `true` branch and give it a name so you can reuse it.

The classic example is extracting the **return type** of a function:

```ts
type GetReturnType<T> = T extends (...args: any[]) => infer R ? R : never;
```

You can read this as:

> "If `T` is a function type that takes any arguments and returns some type `R`, then `GetReturnType<T>` is `R`; otherwise it's `never`."

Using `GetReturnType`
----------------------

```ts
function greet() {
	return "Hello, world!";
}

function sum(a: number, b: number) {
	return a + b;
}

type GreetReturnType = GetReturnType<typeof greet>; // string
type SumReturnType = GetReturnType<typeof sum>;     // number
```

In real-world code you’d normally use the built-in [`ReturnType<T>`](https://www.typescriptlang.org/docs/handbook/utility-types.html#returntypetype) utility, but `GetReturnType` is a nice, small example of how `infer` works.

Why `infer R` instead of just `R`?
----------------------------------

You might be thinking: *"Why do we write `infer R` instead of just `R`?"* The short answer is: **because TypeScript’s syntax requires it.**

The conditional type is checking whether `T` matches this function shape:

```ts
T extends (...args: any[]) => any
```

But we don’t want the return type to be `any` – we want to **capture** whatever that return type actually is and reuse it in the `true` branch of the conditional.

So instead of writing `any`, we write:

```ts
T extends (...args: any[]) => infer R
```

Here’s what `infer R` is doing:

- It **introduces a new type variable** `R` right inside the conditional type.
- If `T` really is a function type, TypeScript **infers** what `R` should be from its return type.
- That inferred `R` is then available only in the `true` branch (`? R : never`).

So you can think of `infer R` as saying:

> "If this conditional is true, create a new type variable `R` for the part of the type I’ve marked, and let me use `R` on the right-hand side of the `?`." 

This same pattern works in more complex situations too – for example, inferring element types from arrays, parameter types from functions, and so on – but the basic idea is always the same: **use `infer` to name a piece of a matched type so you can reuse it.**

