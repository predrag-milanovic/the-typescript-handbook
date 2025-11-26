# Basic Types

TypeScript has static types. This TypeScript code:

```ts
const bootupMessage: string = "Starting support.ai servers...";
```

is equivalent to this JavaScript code:

```js
const bootupMessage = "Starting support.ai servers...";
```

The `: string` annotation specifies the variable's type. The same pattern works for other primitive types like `number`, `boolean`, `null`, and `undefined`:

```ts
const bootupMessage: string = "Starting support.ai servers...";
const port: number = 3000;
const isServerOnline: boolean = true;
const noValue: null = null;
const notDefined: undefined = undefined;
```

If a value doesn't match its annotated type, TypeScript will report an error at compile time. For example, this is invalid:

```ts
const bootupMessage: string = 123;
// Error: Type 'number' is not assignable to type 'string'.
```

Notes:
- TypeScript will often infer types if you omit annotations (e.g., `const x = 1` infers `number`).
- Use annotations when you want an explicit contract or when the inferred type is too broad.

