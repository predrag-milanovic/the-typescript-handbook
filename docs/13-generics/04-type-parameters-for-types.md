# Type Parameters for Types

Type parameters aren't just for functions and methods. You can also use them to create **generic object types** with interfaces or type aliases.

## A Generic Store Type

Here’s a simple `Store` interface that is generic over the kind of value it stores:

```ts
interface Store<T> {
	get(id: string): T;
	save(id: string, item: T): void;
	list(): T[];
}

// The same idea works with a type alias:
// type Store<T> = {
//   get(id: string): T;
//   save(id: string, item: T): void;
//   list(): T[];
// };
```

`Store<T>` describes any value that has `get`, `save`, and `list` methods. The concrete type of `T` is left open so different callers can plug in whatever they need.

## Using a Generic Store in a Function

We can now write a function that works with **any** `Store<T>` regardless of what `T` is:

```ts
function addAndGetItems<T>(
	store: Store<T>,
	id: string,
	newItem: T,
): T[] {
	store.save(id, newItem);
	return store.list();
}
```

`addAndGetItems` doesn’t care what is stored; it just uses the operations guaranteed by the `Store<T>` interface. TypeScript will infer `T` from the `store` and `newItem` arguments.

## A Store for Products

First, define a `Product` type, and then create an object whose shape matches `Store<Product>`:

```ts
type Product = {
	name: string;
	price: number;
};

const productStore = {
	products: {} as Record<string, Product>,

	get(id: string): Product {
		return this.products[id];
	},

	save(id: string, item: Product): void {
		this.products[id] = item;
	},

	list(): Product[] {
		return Object.values(this.products);
	},
};
```

Because `productStore` has `get`, `save`, and `list` methods with the right types, it is compatible with `Store<Product>`.

We can now call `addAndGetItems` and TypeScript will infer `T` as `Product`:

```ts
const newStore = addAndGetItems(productStore, "laneslaptop", {
	name: "Laptop",
	price: 999,
});
console.log(newStore);
// [{ name: "Laptop", price: 999 }]

const finalStore = addAndGetItems(productStore, "allanstoaster", {
	name: "Toaster",
	price: 50,
});
console.log(finalStore);
// [
//   { name: "Laptop", price: 999 },
//   { name: "Toaster", price: 50 },
// ]
```

## A Store for Something Else

The real power of generic types is reuse. We can define a completely different type and create another store that still works with `addAndGetItems`:

```ts
type Homunculus = {
	title: string;
	abilities: string[];
};

const homunculusStore = {
	homunculi: {} as Record<string, Homunculus>,

	get(id: string): Homunculus {
		return this.homunculi[id];
	},

	save(id: string, item: Homunculus): void {
		this.homunculi[id] = item;
	},

	list(): Homunculus[] {
		return Object.values(this.homunculi);
	},
};

const newHomunculus = addAndGetItems(homunculusStore, "laneslaptop", {
	title: "Laptop",
	abilities: ["fast", "strong"],
});
console.log(newHomunculus);
// [{ title: "Laptop", abilities: ["fast", "strong"] }]
```

Here, `addAndGetItems` is reused with `Homunculus` values simply because `homunculusStore` has the same `Store<T>` shape, but with `T` being `Homunculus` instead of `Product`.

This is the core idea of **type parameters for types**: you define one generic structure and let callers plug in the concrete type they need.

