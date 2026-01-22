## Classes vs. Interfaces and Types

When you design object shapes in TypeScript, you often have three different
tools that can describe the same structure:

```ts
class Hero {
	name: string;
	health: number;
}

interface Hero {
	name: string;
	health: number;
}

type Hero = {
	name: string;
	health: number;
};
```

All three `Hero` definitions describe values with a `name` and `health`, but
they come with different capabilities and tradeoffs.

### When to Use Classes

If you come from an object-oriented background, you might prefer classes.
Compared to interfaces and type aliases, classes can:

- Declare `private`, `protected`, `static`, and `abstract` members
- Define one or more constructors
- Provide concrete method implementations shared by all instances
- Participate in inheritance chains with `extends`

Because classes have runtime behavior (constructors, methods, static members),
they are a good fit when you need both a *type* and a *runtime value* that work
together.

### When to Use Interfaces or Type Aliases

Interfaces and type aliases are purely compile-time constructs: they disappear
after TypeScript compiles to JavaScript.

Some advantages of interfaces and type aliases are:

- No runtime overhead — they only exist for type checking
- Simpler to work with when you just need a shape for plain objects
- More flexible for modeling data that is not tied to a specific class
- Interfaces support extension and declaration merging in ways that classes and
	type aliases do not

In many codebases, it is common to start with interfaces or type aliases for
data shapes, and introduce classes only when you need shared behavior,
constructors, or other object-oriented features.

