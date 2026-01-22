## The `this` Type

The `this` keyword in JavaScript can be tricky to reason about, but TypeScript
helps by giving `this` a precise type inside class methods.

### Implicit `this` in Classes

Inside a class method, TypeScript automatically infers the type of `this` as the
class itself:

```ts
class Counter {
	private count: number = 0;

	increment(): void {
		// `this` is implicitly typed as Counter
		this.count++;
	}

	getCount(): number {
		// `this` is implicitly typed as Counter
		return this.count;
	}
}
```

In most cases, this implicit typing is all you need — `this` is understood to be
an instance of `Counter` whenever you call `counter.increment()` or
`counter.getCount()`.

### Explicit `this` Parameters

Sometimes you want more control over the type of `this`, for example when
methods might be passed around as callbacks. TypeScript lets you declare an
*explicit* [`this` parameter](https://www.typescriptlang.org/docs/handbook/2/functions.html#declaring-this-in-a-function) to do exactly that.

The `this` parameter:

- Appears as the first parameter in a function or method signature
- Is only used for type checking; it does **not** exist at runtime

```ts
class Counter {
	private count: number = 0;

	increment(this: Counter, n: number): void {
		// `this` is explicitly typed as Counter
		this.count += n;
	}

	getCount(this: Counter): number {
		// `this` is explicitly typed as Counter
		return this.count;
	}
}

const counter = new Counter();
counter.increment(5);
console.log(counter.getCount());
// 5
```

Here, both `increment` and `getCount` declare `this: Counter`, so TypeScript can
enforce that they are only called with a `Counter` instance as `this`, even if
you pass them around as standalone functions.

