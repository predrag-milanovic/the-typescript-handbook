# PropertyKey

Dynamic keys are usually typed as `string`, but JavaScript objects can also use `number` and `symbol` keys. TypeScript provides the built-in [`PropertyKey`](https://www.typescriptlang.org/docs/handbook/2/mapped-types.html#handbook-content) union to cover every allowed key type:

```ts
// built-in type
type PropertyKey = string | number | symbol;
```

Using `PropertyKey` lets index signatures accept numbers and symbols in addition to strings:

```ts
type InfrastructureTags = {
	[key: PropertyKey]: any;
};

const janesServer: InfrastructureTags = {
	name: "Jane's Server",
	1: 420,
	[Symbol("role")]: "Admin",
};
```

A `symbol` is a unique, immutable value that can be used as a property key. Access symbol-keyed properties with the symbol itself and bracket notation; dot notation will not work.

```ts
const ROLE = Symbol("role");
const user = { [ROLE]: "Admin" };

user[ROLE]; // "Admin"
// user.ROLE; // undefined
```
