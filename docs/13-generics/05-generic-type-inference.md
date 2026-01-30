# Generic Type Inference

When you call a generic function, you can usually **skip** writing the type arguments yourself. TypeScript can infer them from the values you pass in.

Let's revisit our "titan transformer" example:

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

type Human = {
	name: string;
	age: number;
};

const humans: Human[] = [
	{ name: "Eren", age: 15 },
	{ name: "Mikasa", age: 16 },
	{ name: "Armin", age: 15 },
];

const titanTransformer = (human: Human): string => `${human.name} is a titan!`;
```

## Explicit Type Arguments

We *can* call `transform` by explicitly specifying the type parameters:

```ts
const titanNames = transform<Human, string>(humans, titanTransformer);
console.log(titanNames);
//    ^? string[]
```

Here we are telling TypeScript: `InputType` is `Human` and `OutputType` is `string`.

## Letting TypeScript Infer the Types

But we don't have to. In most real code you just write:

```ts
const titanNames = transform(humans, titanTransformer);
//    ^? string[]
```

TypeScript looks at the arguments you passed in and figures out the type parameters:

- `humans` is `Human[]`, so `InputType` is `Human`.
- `titanTransformer` takes a `Human` and returns a `string`, so `OutputType` is `string`.

Once the type parameters are inferred, the rest of the function body and the return type are all fully typed as if you had written `<Human, string>` yourself.

In practice, **generic type inference** means you usually:

- Declare the type parameters on the function.
- Let TypeScript infer the actual type arguments at call sites.

You only need to write the type arguments manually when inference can't figure them out or when you want to override what it would infer.

