# Void

The TypeScript `void` type represents functions that intentionally return nothing.

```ts
function logMessage(message: string): void {
	console.log(message);
	// explicitly returns nothing
}
```

In JavaScript a function with no `return` statement yields `undefined` at runtime, which is a bit vague. In TypeScript, `void` communicates intent: the function is not meant to produce a meaningful value.

When to use `void`:
- For event handlers, logging, or other side-effect-only functions.
- On function types when you want to signal "no useful return value" to callers, e.g. `(s: string) => void`.

Examples:

```ts
// event handler type
type ClickHandler = (event: MouseEvent) => void;

// callback that doesn't return a value
function withLogging(cb: (msg: string) => void) {
	console.log('before');
	cb('hi');
	console.log('after');
}

// async functions that don't return meaningful data: inferred Promise<void>
async function save(): Promise<void> {
	await db.write();
}
```

Notes:
- Prefer `void` when you really intend "no meaningful return". Don't use it to hide useful return values.
- `void` is different from `undefined` and from `any`; it's a signal about intent, not a full runtime guarantee.

```

