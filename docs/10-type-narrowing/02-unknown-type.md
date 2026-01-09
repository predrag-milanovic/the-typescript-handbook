# Unknown Type

We've talked about the [`any`](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#any) type in TypeScript, and how it can represent anything - it's the "widest" type.

The [`unknown`](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-0.html#new-unknown-top-type) type can be used for similar purposes, but it's a much safer alternative because it forces you to explicitly assert the type before using it in a specific way.

## The "any" Problem

The `any` type basically turns off TypeScript's type checking:

```ts
function processData(data: any) {
  // TypeScript allows this even though it might crash
  console.log(data.toLowerCase());

  // TypeScript allows this too - it's like we're using plain JavaScript
  return data.nonExistentMethod();
}

// No errors when calling the function
processData(42); // Will crash at runtime
```

When you take plain JavaScript code and run it through TypeScript tooling, almost everything is `any` by default.

## The "unknown" Solution

The `unknown` type doesn't allow that kind of tomfoolery:

```ts
function processData(data: unknown) {
  // Error: Object is of type 'unknown'
  console.log(data.toLowerCase());

  // Error: Object is of type 'unknown'
  return data.nonExistentMethod();
}
```

With `unknown`, you can still assign any value to it (e.g. call this function with any value), but you can't use that value in a meaningful way without first checking its type:

```ts
function processData(data: unknown) {
  // We do a type assertion
  if (typeof data === "string") {
    // Now TypeScript knows data is a string
    console.log(data.toLowerCase());
    return data;
  }
  if (typeof data === "number") {
    // Now TypeScript knows data is a number
    return data * 2;
  }

  // Throw an error for other types
  // that we can't handle
  throw new Error("Expected string data");
}
```

## When to Use unknown

`unknown` is a fantastic alternative to `any` when it comes to dealing with values that are coming into your program from the outside world (e.g. user input, API responses, etc.). It forces you to add type checks at that I/O boundary so that you can then be confident working with the data inside your program.
