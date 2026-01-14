# Guard Clauses

Guard clauses (a fancy way of saying "early returns") are my favorite way to quickly narrow types within a function. Peak production TypeScript code is often riddled with `undefined` and `null` types due to the nature of I/O and external APIs, so this is a classic pattern:

```typescript
function processName(name: string | null | undefined) {
  if (name === null || name === undefined) {
    return "";
  }
  // TypeScript knows name is a string here
  return name.toUpperCase();
}
```

Now, an empty string keeps `processName`'s behavior straightforward (always returning a string), but depending on your use case, it might make more sense to throw an error instead:

```typescript
function processName(name: string | null | undefined) {
  if (name === null || name === undefined) {
    throw new Error("Name is required");
  }
  // TypeScript knows name is a string here
  return name.toUpperCase();
}
```

Interestingly, throwing an error still narrows the type, but it doesn't change the function signature—this function still just returns a string. That's because errors in JavaScript and TypeScript are a control flow mechanism, not a type mechanism, so you do just kind of need to be aware, "hey this function can throw, I need to handle that".

In cases where my program won't break on an empty string, I might just coalesce to an empty string instead of throwing an error. This happens all the time with optional fields in web apps.
