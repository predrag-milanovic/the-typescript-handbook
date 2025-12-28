# Super Set Unions

So we know we can drastically narrow a primitive type like `number` by using a union of literal types. For example, maybe only 3 error codes are valid:

```typescript
type ErrorSlugs = "OK" | "NOT_FOUND" | "INTERNAL_ERROR";
```

This works great if these are the only valid error codes, but what if:

- Any string can be used as an error slug
- `"OK"`, `"NOT_FOUND"`, and `"INTERNAL_ERROR"` are the most common values and we like to have them show up in autocomplete

TypeScript has a hacky way for us to express this: super set unions.

```typescript
type ErrorCodes = "OK" | "NOT_FOUND" | "INTERNAL_ERROR" | (string & {});
```

## Why Not Just Use `string`?

You might be wondering, "Why wouldn't I just use `string` - the set of allowed values is the same?"

And you're right, but there's one subtle difference. By adding `(string & {})`, TypeScript won't change which values are allowed. Any string is allowed. But it will still give us autocomplete in our editor for the values `"OK"`, `"NOT_FOUND"`, and `"INTERNAL_ERROR"`.
