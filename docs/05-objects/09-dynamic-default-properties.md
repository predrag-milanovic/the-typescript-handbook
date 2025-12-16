# Dynamic Default Properties

There's a useful pattern you'll see in the wild that combines index signatures with specific properties:

```ts
type FormData = {
  [field: string]: string;
  email: string;
  password: string;
};
```

## Why Require Specific Properties?

You might wonder why `email` and `password` are explicitly defined when the index signature already allows any string properties. The reason is to **require certain properties**.

This type says:
- The object **must** have `email` and `password` properties
- The object **can** have any number of additional string properties

## Combining Different Value Types

You can also combine index signatures with different types:

```ts
type FormData = {
  [field: string]: string | number | boolean;
  email: string;
  password: string;
  age: number;
};
```

This type says:
- The object **must** have `email` (string), `password` (string), and `age` (number)
- The object **can** have any number of additional string, number, or boolean properties

## Best Practices

⚠️ **Avoid overusing this pattern.** Only use dynamic keys when you truly need unknown keys. If you have optional properties, use the `?` operator instead:

```ts
// ✓ Prefer this for known optional properties
type FormData = {
  email: string;
  password: string;
  nickname?: string;
};

// ✗ Avoid this unless you need truly dynamic keys
type FormData = {
  [field: string]: string;
  email: string;
  password: string;
};
```
