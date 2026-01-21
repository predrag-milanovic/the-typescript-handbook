## Protected Data Members

The [`protected` keyword](https://www.typescriptlang.org/docs/handbook/2/classes.html#protected) is a TypeScript-only feature – it is not part of the ECMAScript standard. A `protected` member is accessible inside the class where it is declared, and inside any subclasses, but **not** from outside those classes.

You can think of `protected` as "`private`, but also accessible to subclasses".

```ts
class Character {
	protected health: number;

	constructor(health: number) {
		this.health = health;
	}

	protected takeDamage(amount: number): void {
		this.health -= amount;
		if (this.health < 0) {
			this.health = 0;
		}
	}
}

class Fighter extends Character {
	constructor(health: number) {
		super(health);
	}

	public fight(damage: number): void {
		// Can access protected members inherited from Character
		this.takeDamage(damage);
		console.log(`Fighter took ${damage} damage. Health: ${this.health}`);
	}
}

const fighter = new Fighter(100);
fighter.fight(30);

// Error: Property 'health' is protected and only accessible
// within class 'Character' and its subclasses
console.log(fighter.health);

// Error: Property 'takeDamage' is protected and only accessible
// within class 'Character' and its subclasses
fighter.takeDamage(10);
```

Here, `Fighter` can use the `health` property and `takeDamage` method because it extends `Character`. Code outside the class hierarchy cannot access those members.

Like `abstract`, the `protected` keyword has no direct equivalent in JavaScript at runtime. It exists only in TypeScript's type system to help you express and enforce class APIs. In JavaScript output, the `protected` keyword is erased.

In many codebases, you might see alternatives such as:

- Using `#` private fields when you want runtime-enforced privacy.
- Leaving members `public` when you are comfortable with subclasses and external code accessing them.

`protected` is most useful when you want to clearly signal an API that is meant only for subclasses, while still preventing access from the rest of your program at the type-checking level.

