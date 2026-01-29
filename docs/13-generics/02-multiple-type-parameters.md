# Multiple Type Parameters

[Type parameters](https://www.typescriptlang.org/docs/handbook/2/generics.html#generic-functions) are just parameters. You don’t have to stop at a single one — a generic function or type can use as many type parameters as it needs (within reason).

In examples, you’ll often see short names like `T`, `U`, or `V`. Those are only conventions: you can use longer, more descriptive names if you prefer.

## A Transform Function with Two Type Parameters

Let’s build a function that "transforms" its inputs. It should:

- Take an array of items of type `InputType`.
- Take a function that converts an `InputType` into an `OutputType`.
- Return a new array of `OutputType` values.

```ts
function transform<InputType, OutputType>(
	inputs: InputType[],
	update: (item: InputType) => OutputType,
): OutputType[] {
	const outputs: OutputType[] = [];

	for (const input of inputs) {
		const output = update(input);
		outputs.push(output);
	}

	return outputs;
}
```

That signature is a bit long — which is why many people prefer single-letter names like `T` and `U` for type parameters in real code.

If you’ve used JavaScript’s `Array.prototype.map`, you might recognize this pattern: `transform` is essentially a typed reimplementation of `map`.

## Using `transform` with Objects

First, define a `Human` type and an array of humans:

```ts
type Human = {
	name: string;
	age: number;
};

const humans: Human[] = [
	{ name: "Eren", age: 15 },
	{ name: "Mikasa", age: 16 },
	{ name: "Armin", age: 15 },
];
```

Now create a transformer that turns a `Human` into a `string`:

```ts
const titanTransformer = (human: Human): string =>
	`${human.name} is a titan!`;

const titanNames = transform<Human, string>(humans, titanTransformer);
console.log(titanNames);
// ['Eren is a titan!', 'Mikasa is a titan!', 'Armin is a titan!']
```

Here, TypeScript checks that:
- The `inputs` array is `Human[]`.
- The `update` function takes a `Human` and returns a `string`.
- The return type of `transform` is `string[]`.

## Reusing `transform` with Other Types

We don’t need to change `transform` to work with completely different data — we only change the type arguments and the `update` function.

```ts
const numbers = [1, 2, 3, 4, 5];

const double = (num: number): number => num * 2;

const doubledNumbers = transform<number, number>(numbers, double);
console.log(doubledNumbers);
// [2, 4, 6, 8, 10]
```

By using multiple type parameters, `transform` stays flexible and type-safe no matter what kinds of values you pass in and return.

