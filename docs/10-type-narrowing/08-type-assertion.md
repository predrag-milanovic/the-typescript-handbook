# Type Assertion

Sometimes you know more about a value's type than TypeScript does... it's rare but it happens. The [`as` keyword](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#type-assertions) is the "trust me, bro" of TypeScript.

In the Boot.dev codebase, we have some places where we know a query parameter is a string, but Vue (our front-end framework) uses `string | string[]` for query params... which makes sense because query params can be arrays, but we know in many cases (because our back-end controls this) that it's always a string.

So, we have something like this:

```typescript
// Property 'toLowerCase' does not exist on type 'string | string[]'
const userId = route.query?.userId.toLowerCase();
```

But we know it's never an array, so we just use `as string` to do this:

```typescript
const userId = (route.query?.userId as string).toLowerCase();
```

We also capture values that come across the network as `unknown` and then use `as` to assert them into the shape we expect a given network response to be:

```typescript
type User = {
  id: string;
  name: string;
};

async function getUserRaw(userId: string): Promise<unknown> {
  const response = await fetch(`/api/users/${userId}`);
  return response.json();
}

export async function getUser(userId: string) {
  const data = await getUserRaw(userId);
  // here data is still just "unknown"
  // so we assert it to a User type
  return data as User;
}
```

## Angle Bracket Syntax

There is an alternative syntax for type assertions using angle brackets and the type before the value:

```typescript
const userIdRaw = <string>route.query?.userId;
const userId = userIdRaw.toLowerCase();
```

## When to Do Type Assertions

- I try to avoid them. I'd rather use actual conditional narrowing over assertions unless I'm extremely confident. Conditional narrowing is safer because it doesn't involve assumptions.
- I prefer the `as` syntax over the angle bracket syntax. It's clearer, easier to read, and easier to write.
