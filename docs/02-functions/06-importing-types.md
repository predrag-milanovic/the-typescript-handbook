# Importing Types

When you need to use types from another module, TypeScript provides a dedicated syntax for importing types only — without importing runtime values.

## Basic Syntax

The `import type` syntax signals to TypeScript that you're importing only types:

```ts
import type { User, Post } from "./models";
```

Compare with a regular import (which might include runtime values):

```ts
import { User, Post } from "./models"; // may include runtime code
```

## Why Use `import type`?

TypeScript will strip out type-only imports during compilation, so they don't generate any JavaScript code. This keeps your bundle smaller and makes the intent clear: these are compile-time types, not runtime values.

## Alternative Syntax

You can also mix types and values in a single import using the `type` keyword on individual items:

```ts
import { type User, type Post } from "./models";
import { fetchUser } from "./models"; // runtime value
```

Or combined:

```ts
import { type User, fetchUser } from "./models";
```

## Recommendation

Prefer `import type { ... }` for all type-only imports. It's:
- **Concise**: all types in one dedicated import statement.
- **Clear**: explicitly signals "types only" to readers.
- **Organized**: separates type imports from value imports.

## Example

```ts
// models.ts
export type User = {
  id: number;
  name: string;
};

export function fetchUser(id: number): Promise<User> {
  // ...
}

// app.ts
import type { User } from "./models";
import { fetchUser } from "./models";

async function loadUser(id: number): Promise<User> {
  return fetchUser(id);
}
```

## Best Practice

Always use `import type` for types. It makes your code clearer, keeps bundles lean, and helps avoid circular dependency issues.
