# Function Type Syntax

One of the most useful places for explicit types is a function signature. Each parameter can have a type annotation, and the function itself can declare a return type. Example with a regular function:

```ts
function createMessage(name: string, a: number, b: number): string {
  return `${name} scored ${a + b}`;
}
```

Here:
- `name: string`, `a: number`, and `b: number` annotate each parameter's type.
- The `: string` after the parameter list declares the return type.

Arrow functions use the same syntax for parameters and return type:

```ts
const createMessage = (name: string, a: number, b: number): string => {
  return `${name} scored ${a + b}`;
};
```

Notes and best practices:
- Prefer letting TypeScript infer the return type for short functions when the implementation is obvious; explicit return types are valuable for public APIs and when you want to enforce a contract.
- Use parameter annotations to make intent clear and to surface mistakes early during development.
- For more complex signatures consider using type aliases or interfaces for readability, e.g. `type Score = (name: string, a: number, b: number) => string;`.
