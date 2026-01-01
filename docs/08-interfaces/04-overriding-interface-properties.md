Overriding Interface Properties
===============================

You can replace a property from a base interface as long as the new type is **compatible** with the original.

```ts
interface Character {
	rank: string | number;
	name: string;
	level: number;
}

interface Wizard extends Character {
	// Narrowing is allowed because number is assignable to string | number
	rank: number;
	mana: number;
}
```

Trying to override with an incompatible type fails:

```ts
interface Character {
	rank: string;
	name: string;
	level: number;
}

interface Wizard extends Character {
	// Error: number is not assignable to string
	rank: number;
	mana: number;
}
```
