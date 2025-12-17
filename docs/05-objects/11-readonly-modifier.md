# Readonly Modifier

The [`readonly` modifier](https://www.typescriptlang.org/docs/handbook/2/objects.html#readonly-properties) works like `const` for object properties: once set, they cannot be reassigned.

```ts
type Point = {
	readonly x: number;
	y: number;
};

const point: Point = {
	x: 10,
	y: 20,
};

point.y = 30; // OK
// point.x = 15; // Error: Cannot assign to 'x' because it is a read-only property
```

Use `readonly` when a property should stay stable after initialization. It is most useful on data that rarely changes; overusing it can make updates noisy because you must create new objects instead of mutating existing ones.
