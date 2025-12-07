# Function Types

Functions are values in JavaScript — and TypeScript — so they have types too. But function types aren't just "function"; they include information about parameters and return values.

## Syntax

A function type is written as:

```
(param1: type1, param2: type2, ...) => returnType
```

For example, a function that takes two numbers and returns a number:

```ts
(a: number, b: number) => number
```

Both of these functions match that type:

```ts
const add = (a, b) => a + b;
const subtract = (a, b) => a - b;
```

## Using Function Types

Name function types with a `type` alias for reuse:

```ts
type MathOp = (a: number, b: number) => number;

const multiply: MathOp = (x, y) => x * y;
const divide: MathOp = (x, y) => x / y;
```

Assign function types to variables or parameters:

```ts
// variable holding a function of type (name: string) => string
const greet: (name: string) => string = (n) => `Hello, ${n}!`;

// callback parameter
function execute(cb: (x: number) => void) {
  cb(42);
}
```

Function types in higher-order functions (functions that take or return functions):

```ts
type Mapper<T, U> = (item: T) => U;

function map<T, U>(arr: T[], transform: Mapper<T, U>): U[] {
  return arr.map(transform);
}

const nums = [1, 2, 3];
const strs = map(nums, (n) => n.toString()); // inferred: string[]
```

## Optional and Default Parameters in Function Types

```ts
// optional param: ? suffix
type Logger = (msg: string, level?: string) => void;

// default param
type Multiply = (a: number, b?: number) => number;
```

## Key Takeaway

Function types capture the shape of a function: its parameter types and return type. Use them to annotate callbacks, higher-order functions, and to enforce contracts across your codebase.
