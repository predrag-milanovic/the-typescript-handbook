# Rest Parameters

[Rest parameters](https://www.typescriptlang.org/docs/handbook/2/functions.html#rest-parameters) allow a function to accept an indefinite number of trailing arguments and collect them into an array. They are denoted by three dots `...` before the parameter name.

## Basic Syntax

```typescript
function gatherParty(partyName: string, ...adventurers: string[]): string {
	return `${partyName} consists of: ${adventurers.join(", ")}`;
}

const msg = gatherParty("The Fellowship", "Frodo", "Sam", "Gandalf");
console.log(msg);
// "The Fellowship consists of: Frodo, Sam, Gandalf"
```

- `partyName`: regular parameter
- `...adventurers`: rest parameter, typed as `string[]`

## Type Safety with Rest

Rest parameters are fully typed, so array operations are type-safe:

```typescript
function sum(...nums: number[]): number {
	return nums.reduce((acc, n) => acc + n, 0);
}

sum(1, 2, 3);     // 6
// sum("4");     // Error: argument must be number
```

You can mix regular and rest parameters, but rest must be last:

```typescript
function tag(label: string, ...values: (string | number)[]): string {
	return `${label}: ${values.join(", ")}`;
}

tag("ids", 10, 20, 30);
tag("names", "Aragorn", "Legolas");
```

## Using Spread at Call Sites

Rest parameters are often paired with spread syntax when calling:

```typescript
const party = ["Frodo", "Sam", "Gandalf"] as const;

gatherParty("The Fellowship", ...party);
```

Note: spread (`...array`) is used at call sites; rest (`...param`) is used in function definitions.

## Optional + Rest

Optional parameters must appear before a rest parameter:

```typescript
function log(prefix?: string, ...messages: string[]): void {
	const p = prefix ?? "LOG";
	messages.forEach(m => console.log(`${p}: ${m}`));
}

log(undefined, "started", "running");
log("WARN", "disk low");
```

## Tuples with Rest

Rest parameters align well with tuple types for structured variadic functions:

```typescript
type Command = [name: string, ...args: (string | number)[]];

function execute(...cmd: Command): void {
	const [name, ...args] = cmd;
	console.log(`Executing ${name} with`, args);
}

execute("upload", "file.txt", 3);
```

## Common Pitfalls

- Rest parameter must be last: `function f(a: string, ...rest: number[], b: string)` // Error
- Rest parameter is always an array: treat it as `T[]`, not a single `T`
- Avoid `any[]` for rest—prefer specific unions like `(string | number)[]`

## Built-ins Using Rest

You've likely used rest parameters without noticing. For example, `console.log` accepts rest arguments:

```typescript
// Declaration style
declare function consoleLog(...data: unknown[]): void;
consoleLog("Users", 3, { active: true });
```

## Summary

- Define variable-length parameters with `...param: T[]`
- Rest must be the final parameter
- Combine with unions and tuples for flexible, type-safe APIs
- Spread at call sites complements rest in definitions

Don't confuse rest parameters with [spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax): rest collects into an array in parameter lists; spread expands arrays/iterables at call sites.
