# Destructuring Tuples

Tuples pair nicely with destructuring when you want to return multiple, well-typed values from a function without introducing a new object type. The values are positional, and TypeScript keeps their types aligned with each position.

```ts
function getName(fullName: string): [string, string] {
	const parts = fullName.split(" ");
	return [parts[0], parts[1]];
}

const [firstName, lastName] = getName("Frodo Baggins");
```

The tuple return type `[string, string]` ensures `firstName` and `lastName` are both `string`. Destructuring makes the intent clear and avoids manual indexing like `value[0]`.

## Nested Destructuring

You can destructure nested tuples and objects in a single statement. This is helpful when a tuple contains structured data.

```ts
type UserWithAddress = [string, { city: string; country: string }];

const userData: UserWithAddress = [
	"Aragorn",
	{ city: "Minas Tirith", country: "Gondor" },
];

const [userName, { city, country }] = userData;
console.log(city); // "Minas Tirith"
```

In this example, `userName` is a `string`, and the destructured `city` and `country` variables are strongly typed as `string` properties from the nested object. The `console.log(city)` statement prints "Minas Tirith".

### Tips
- Prefer explicit tuple types for clarity and safety.
- Use destructuring to name each position, which improves readability compared to numeric indices.
- Keep tuple sizes small; for larger records, a named object type is usually clearer.

