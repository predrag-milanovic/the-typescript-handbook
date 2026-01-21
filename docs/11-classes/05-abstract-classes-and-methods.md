## Abstract Classes and Methods

An [abstract](https://www.typescriptlang.org/docs/handbook/2/classes.html#abstract-classes-and-members) class is a class that cannot be instantiated directly. It acts as a template for subclasses, enforcing that they implement certain methods or properties.

Here is a simple `Shape` abstract class:

```ts
abstract class Shape {
	size: "small" | "medium" | "large";

	constructor(size: "small" | "medium" | "large") {
		this.size = size;
	}

	abstract calculateArea(): number;

	displayArea(): void {
		console.log(`The area of this shape is ${this.calculateArea()}`);
	}
}
```

Because `Shape` is abstract, you cannot create instances of it directly:

```ts
// Error: Cannot create an instance of an abstract class
const shape = new Shape("small");
```

Within an abstract class, abstract methods (like `calculateArea` above) declare a required method signature, but do not provide an implementation. Subclasses must implement these abstract methods. The class can still include regular methods (like `displayArea`) that are shared by all subclasses.

Here is a `Circle` class that extends `Shape` and provides the required `calculateArea` implementation:

```ts
class Circle extends Shape {
	radius: number;

	constructor(size: "small" | "medium" | "large") {
		super(size);

		if (this.size === "small") {
			this.radius = 5;
		} else if (this.size === "medium") {
			this.radius = 10;
		} else {
			this.radius = 15;
		}
	}

	calculateArea(): number {
		return Math.PI * this.radius * this.radius;
	}
}
```

Unlike `Shape`, the `Circle` class can be instantiated normally:

```ts
const circle = new Circle("medium");
circle.displayArea();
// The area of this shape is 314.1592653589793
```

Like `protected`, the `abstract` keyword does not exist in JavaScript at runtime. It is a TypeScript-only feature that helps enforce rules on subclasses at compile time. When your TypeScript is compiled to JavaScript, the `abstract` keyword and abstract-only information are removed from the output.

