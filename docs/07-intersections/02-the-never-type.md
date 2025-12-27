# The Never Type

In TypeScript, the [`never`](https://www.typescriptlang.org/docs/handbook/2/functions.html#never) type represents values that can't occur. It sounds useless, but it's actually a powerful tool for ensuring exhaustive handling of all cases.

## Detecting Unhandled Cases

Consider a function that should handle 3 cases:

```ts
function handleStatusCode(code: 200 | 404 | 500) {
  if (code === 200) {
    console.log("OK");
    return;
  }
  if (code === 404) {
    console.log("Not Found");
    return;
  }
  throw new Error(`Unknown status code: ${code}`);
}
```

This function only handles `200` and `404`, but TypeScript doesn't complain. However, you can catch this by tracking type narrowing. After each conditional, the type of `code` is narrowed down:

```ts
function handleStatusCode(code: 200 | 404 | 500) {
  if (code === 200) {
    console.log("OK");
    return;
  }
  // code is now 404 | 500
  if (code === 404) {
    console.log("Not Found");
    return;
  }
  // code is now 500
  throw new Error(`Unknown status code: ${code}`);
}
```

## Using Never for Exhaustive Checks

If you assign `code` to a variable of type `never`, TypeScript will complain unless `code` has actually been narrowed to no possible values:

```ts
function handleStatusCode(code: 200 | 404 | 500) {
  if (code === 200) {
    console.log("OK");
    return;
  }
  if (code === 404) {
    console.log("Not Found");
    return;
  }
  // Error: Type '500' is not assignable to type 'never'.
  const err: never = code;
  return err;
}
```

This error tells you that not all cases were handled. Fix it by handling every case properly:

```ts
function handleStatusCode(code: 200 | 404 | 500) {
  if (code === 200) {
    console.log("OK");
    return;
  }
  if (code === 404) {
    console.log("Not Found");
    return;
  }
  if (code === 500) {
    console.log("Internal Server Error");
    return;
  }
  // No errors! code is never
  const err: never = code;
  return err;
}
```

Now the type system confirms that all cases are covered. This pattern is invaluable for maintaining code safety as you add new union members.
