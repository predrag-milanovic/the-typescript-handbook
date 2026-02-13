TypeScript Ignore Directives
============================

I try really hard to avoid using these, but sometimes they are the least-bad option.

TypeScript has a few special comments that can suppress type errors:

```ts
// @ts-ignore: Ignores the next line's errors.

// @ts-ignore
const x: number = "not a number"; // Error suppressed

// @ts-nocheck: Disables type checking for the entire file.

// @ts-nocheck

const y: number = "not a number"; // No error

function sum(x: number, y: number): string {
	return x + y; // No error
}
```

These comments do exactly what they say: they **turn off TypeScript's help**.

- `@ts-ignore` hides all errors on the *next* line.
- `@ts-nocheck` disables type checking for the *entire file*.

Use them **very sparingly**, or ideally, not at all.

When you feel tempted to reach for one of these, consider instead:

- Narrowing or refining the types so the error is genuinely fixed.
- Adding an explicit type assertion (with a comment explaining why) if you truly know more than the compiler.
- Isolating unsafe code behind a small, well-documented helper.

If you do end up using `@ts-ignore` or `@ts-nocheck`, treat it as technical debt:

- Add a short justification comment next to it.
- Prefer `@ts-ignore` on a single line over `@ts-nocheck` for an entire file.
- Revisit these directives periodically and remove them once the underlying issue is resolved.

These tools are escape hatches, not everyday instruments.

