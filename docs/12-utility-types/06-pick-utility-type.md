## Pick Utility Type

[`Pick<T, K>`](https://www.typescriptlang.org/docs/handbook/utility-types.html#picktype-keys) creates a new type by selecting a subset of properties from an existing type `T`.

```ts
interface Product {
	id: string;
	name: string;
	price: number;
	description: string;
	category: string;
	inStock: boolean;
	images: string[];
	reviews: { user: string; rating: number; text: string }[];
}

type ProductSummary = Pick<Product, "id" | "name" | "price">;

const productList: ProductSummary[] = [
	{ id: "p1", name: "Headphones", price: 79.99 },
	{ id: "p2", name: "Mouse", price: 49.99 },
];

const invalidProduct: ProductSummary = {
	id: "p3",
	name: "Keyboard",
	price: 99.99,
	// TypeScript error:
	// Object literal may only specify known properties,
	// and 'description' does not exist in type 'ProductSummary'.
	description: "Noise cancelling headphones",
};
```

Because `ProductSummary` is built with `Pick`, it only allows the `id`, `name`, and `price` properties from `Product`. Any extra properties (like `description`) cause a type error.

`Pick` is handy for creating focused “views” of a larger type, such as:

- return types from APIs that don’t need to expose every field
- DTOs or lightweight objects passed between layers
- narrowing a type for UI components that only read a few properties

