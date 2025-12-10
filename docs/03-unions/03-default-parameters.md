# Default Parameters

Default parameters provide fallback values for function arguments when the caller doesn't supply them.

## Basic Example

```ts
function newCharacter(name: string, role: string = "warrior"): string {
  return `${name} is a ${role}`;
}

console.log(newCharacter("Gandalf"));
// Gandalf is a warrior
console.log(newCharacter("Gandalf", "wizard"));
// Gandalf is a wizard
```

## Type Inference

When you use a default value, you don't need to mark the parameter as optional with `?`, and TypeScript can infer the parameter's type automatically:

```ts
function countdown(start = 10): void {
  // start is inferred as number (not number | undefined)
  console.log(`Counting down from ${start}...`);
}

countdown();    // uses default 10
countdown(5);   // uses provided 5
```

Notice that `start` has type `number`, not `number | undefined` — because a default value is always provided (either by the caller or by the function).

## Default vs Optional

| Feature | Optional (`?`) | Default Value |
|---------|---|---|
| Parameter type inside function | `Type \| undefined` | `Type` |
| Requires type annotation | No | No (inferred) |
| Must come after required params | Yes | Yes |
| Always has a value | No (can be `undefined`) | Yes |

```ts
// Optional: can be undefined
function greet(name: string, title?: string) {
  // title: string | undefined
}

// Default: never undefined inside function
function greetWithDefault(name: string, title: string = "Friend") {
  // title: string
}
```

## Type Widening

Sometimes you want a default value of one type but accept a wider type as parameter. Use an explicit type annotation:

```ts
// Without annotation: inferred as number (literal 0)
function add(a: number, b = 0) {
  return a + b;  // b: number
}

// With annotation: explicitly widen to accept string or number
function addWide(a: number | string, b: number | string = 0) {
  // b can be number or string
  return a + b;
}
```

## Key Takeaway

Use default parameters to provide sensible fallbacks. TypeScript infers the parameter type from the default value, so you usually don't need explicit annotations — unless you want to widen the type beyond what the default suggests.
