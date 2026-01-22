## Parameter Properties

TypeScript has a shorthand feature called [*parameter properties*](https://www.typescriptlang.org/docs/handbook/2/classes.html#parameter-properties) that lets you
declare and initialize class properties directly in the constructor parameter
list. This avoids having to both declare fields and then assign them inside the
constructor body.

### Without Parameter Properties

Normally, you might write a class like this:

```ts
class Hero {
	name: string;
	health: number;
	private level: number;

	constructor(name: string, health: number, level: number) {
		this.name = name;
		this.health = health;
		this.level = level;
	}
}
```

Here, each constructor parameter is manually copied into a class property.

### With Parameter Properties

With parameter properties, you can get the same result with much less code:

```ts
class Hero {
	constructor(
		public name: string,
		public health: number,
		private level: number,
	) {}
}
```

In this version, the constructor body `{}` is intentionally empty — the
parameter properties are doing both the *declaration* and the *initialization*
for you. Any other class members (methods, getters, setters, etc.) still belong
in the class body, outside the constructor.

By adding an access modifier to a constructor parameter — `public`, `private`,
`protected`, or `readonly` — TypeScript will automatically:

- Declare a property on the class with the same name and type
- Assign the argument passed to the constructor to that property

So the two `Hero` declarations above are equivalent from TypeScript’s
perspective.

### Limitations

Parameter properties work with TypeScript’s `private` keyword, but **not** with
JavaScript’s `#`-style private fields. If you need a `#` private field, you must
declare and initialize it separately:

```ts
class Hero {
	#secretPower: string;

	constructor(
		public name: string,
		secretPower: string,
	) {
		this.#secretPower = secretPower;
	}
}
```

In this example, `name` is a public parameter property, while `#secretPower` is
a separate, truly private field initialized inside the constructor body.

