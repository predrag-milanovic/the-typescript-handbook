## Empty Object Type

Say I innocently create a new empty object:

```ts
let newUser = {};
```

Then go to add properties to it later:

```ts
// Property 'name' does not exist on type '{}'
newUser.name = "Predrag";
```

TypeScript doesn't like that!

It makes sense—we never told TypeScript which properties to allow... but here's what's really crazy: this is actually allowed:

```ts
let newUser = {};
newUser = "Predrag";
```

Yup. You can reassign the variable, which initially held an empty object to a string. In fact, you can reassign it to anything except `null` or `undefined`, because everything else is technically an object!

So, to get back to our first example, what you probably want to do is just predefine the allowed field(s):

```ts
type User = {
	name: string;
};

let newUser: User = {
	name: "Predrag",
};
```

Defining the shape up front ensures TypeScript enforces the intended properties and prevents unsafe reassignment.
