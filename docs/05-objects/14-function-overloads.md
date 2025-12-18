# Function Overloads

[Function overloads](https://www.typescriptlang.org/docs/handbook/2/functions.html#function-overloads) let you constrain which parameter combinations are valid while maintaining flexibility. They provide type safety for functions that accept different argument patterns.

Define overload signatures above the implementation to specify allowed call patterns:

```ts
type Product = {
  id: string;
  name: string;
  price: number;
};

// Overload signatures
function createOrder(product: Product): string;
function createOrder(
  product: Product,
  expedited: true,
  deliveryDate: Date,
): string;

// Implementation signature
function createOrder(
  product: Product,
  expedited?: boolean,
  deliveryDate?: Date,
): string {
  if (!expedited) {
    return `Order for ${product.name} ($${product.price}) - Standard Shipping`;
  }
  return `Order for ${product.name} ($${product.price}) - Expedited: ${deliveryDate?.toLocaleDateString()}`;
}
```

Without overloads, the implementation would accept any combination of arguments. The overloads restrict calls to exactly two patterns: either one argument or three arguments where `expedited` must be `true`.

```ts
const laptop: Product = { id: "L123", name: "ThinkPad", price: 1200 };

// OK: one argument
const order1 = createOrder(laptop);
// Order for ThinkPad ($1200) - Standard Shipping

// OK: three arguments
const order2 = createOrder(laptop, true, new Date("2024-12-20"));
// Order for ThinkPad ($1200) - Expedited: 12/20/2024

// Error: No overload expects 2 arguments, but overloads do exist that expect either 1 or 3 arguments.
const order3 = createOrder(laptop, true);
```

Use overloads to enforce relationships between parameters, like requiring a delivery date when expedited shipping is requested.
