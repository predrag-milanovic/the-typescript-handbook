# Generic Constraints

Sometimes you need a generic function to know **something** about the types it operates on. In the examples so far, the type parameter could be anything:

```ts
async function fetchFromApi<T>(url: string): Promise<T | undefined>;
```

Here `T` is completely unconstrained. TypeScript doesn’t assume any properties or methods on `T`.

Generic **constraints** let you say, “`T` must at least have these members.” That way, your implementation can safely use those members while still being generic over everything else.

## Constraining with `extends`

Constraints are usually expressed with interfaces (or object types) and the `extends` keyword on a type parameter.

First, define a constraint type:

```ts
interface HasCost {
	cost: number;
}
```

Then constrain a generic type parameter to types that satisfy that interface:

```ts
function applyDiscount<T extends HasCost>(
	vals: T[],
	discount: number,
): T[] {
	const arr: T[] = [];

	for (const val of vals) {
		val.cost *= discount;
		arr.push(val);
	}

	return arr;
}
```

`T extends HasCost` means:
- `T` can be any type **as long as** it has a numeric `cost` property.
- Inside the function, `val.cost` is safe to access and mutate.
- The function still returns `T[]`, so you don’t lose type information.

## Using the Constrained Function

Because `HasCost` is just “anything with a `cost: number`,” lots of different shapes can work.

```ts
const shoes = [
	{
		size: 12.5,
		country: "BIH",
		cost: 120,
	},
	{
		size: 12.5,
		country: "US",
		cost: 110,
	},
];

const tvs = [
	{
		framerate: 120,
		brand: "Samsung",
		cost: 500,
	},
	{
		framerate: 240,
		brand: "Vizio",
		cost: 300,
	},
];

const people = [
	{
		name: "Predrag",
	},
	{
		name: "Breanna",
	},
];

const discountedShoes = applyDiscount(shoes, 0.3);
const discountedTVs = applyDiscount(tvs, 0.5);

// Error:
// Argument of type '{ name: string; }[]' is not assignable to
// parameter of type 'HasCost[]'.
// (Also, you can't buy people!)
const discountedPeople = applyDiscount(people, 0.2);
```

`shoes` and `tvs` are fine because every element has a `cost` property, so they satisfy `HasCost`. `people` fails the constraint because there is no `cost` property.

Generic constraints are a key tool for writing reusable functions that still make **safe assumptions** about the shapes of the values they work with.

