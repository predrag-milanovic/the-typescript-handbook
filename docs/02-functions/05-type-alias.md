# Type Alias

Long, complex types can clutter your code. Type aliases let you name and reuse them, improving readability and maintainability.

## The Problem

Without type aliases, function signatures can become verbose and hard to read:

```ts
function setLoggerTimeout(
  loggerCallback: (s1: string, s2: string) => string,
  delay: number,
) {
  // do something
}
```

## The Solution

Use the `type` keyword to create a type alias:

```ts
type LoggerCallback = (s1: string, s2: string) => string;
```

Now you can use `LoggerCallback` anywhere you need this specific function type:

```ts
function setLoggerTimeout(loggerCallback: LoggerCallback, delay: number) {
  // do something
}
```

Much cleaner and easier to read!

## Benefits

- **Readability**: Named types communicate intent better than inline annotations.
- **Reusability**: Define once, use everywhere.
- **Maintainability**: Change the type definition in one place, and all usages update automatically — no risk of copy-paste errors.

## More Examples

Object types:

```ts
type User = {
  id: number;
  name: string;
  email: string;
};

function greetUser(user: User): string {
  return `Hello, ${user.name}!`;
}
```

Union types:

```ts
type Status = 'idle' | 'loading' | 'success' | 'error';

function setStatus(status: Status) {
  // ...
}
```

Generic type aliases:

```ts
type Result<T> = { ok: true; value: T } | { ok: false; error: string };

function fetchData(): Result<number> {
  // ...
}
```

## When to Use Type Aliases

- When a type is used in multiple places.
- When a type is complex or verbose.
- When you want to give a meaningful name to a type for clarity.

Prefer type aliases over repeating the same inline type annotations. Your future self (and your teammates) will thank you.
