# Inferred Return Types

Much like preferring `const x = 1` over `const x: number = 1`, it's usually fine — and often preferable — to let TypeScript infer a function's return type instead of annotating it explicitly.

Simple example:

```ts
function divide(a: number, b: number) {
	return a / b; // inferred as number
}

const result = divide(10, 2); // result: number
```

Arrow functions work the same way:

```ts
const toUpper = (s: string) => s.toUpperCase(); // inferred return: string
```

Async functions and promises:

```ts
async function fetchCount(): Promise<number> {
	return 42;
}

// If you omit the return annotation, TypeScript still infers Promise<number>
async function fetchCountInferred() {
	return 42; // inferred as Promise<number>
}
```

When inference can be problematic
- Complex conditional returns — if different branches produce values that require manual narrowing, an explicit return type documents intent and catches accidental regressions.

```ts
function parseAmount(src: string) {
	if (src === '') return null; // inferred: string | null
	return Number(src);
}

// If you wanted to enforce always returning number | null, you might annotate it:
function parseAmountExplicit(src: string): number | null {
	if (src === '') return null;
	return Number(src);
}
```

- Any `any`-producing operations (e.g., `JSON.parse`) — you may want explicit annotations to avoid leaking `any` into your API.

Generic helpers and callbacks — return types are often inferred and remain useful without explicit annotations:

```ts
function identity<T>(v: T) {
	return v; // inferred return: T
}

const mapped = [1, 2, 3].map(n => n * 2); // inferred number[]
```

When to prefer explicit return types
- Public APIs, library code, or exported functions where the declared contract matters.
- When inference would produce an overly broad type (e.g., `any`) or hide complexity.
- When using function overloads — the overload signatures are the public contract and the implementation may have a broader parameter/return shape.

In practice, prefer inference for small, internal helpers and use explicit return types for exported or critical functions. This keeps code concise while preserving clear API boundaries.

