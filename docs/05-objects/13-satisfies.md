# Satisfies

The [`satisfies` operator](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-4-9.html#the-satisfies-operator) validates that a value matches a type without widening the inferred type. It solves a common dilemma:

- Type inference keeps narrow types but may miss structural errors
- Explicit type annotations catch errors but widen types and lose precision

Here's plain inference, which misses a typo:

```ts
const colors = {
  red: "#ff0000",
  green: "#00ff00",
  blue: 255,
  yelow: "#ffff00", // typo not caught
};
```

Adding an explicit type catches the typo but widens the value types:

```ts
type ColorMap = {
  red: string | number;
  green: string | number;
  blue: string | number;
  yellow: string | number;
};

const colorsTyped: ColorMap = {
  red: "#ff0000",
  green: "#00ff00",
  blue: 255,
  // Error: "yelow" is not in type ColorMap
  yelow: "#ffff00",
};

// redHex is widened to 'string | number'
type redHex = typeof colorsTyped.red;

// Error: Property 'toUpperCase' does not exist on type 'string | number'
const redUpper = colorsTyped.red.toUpperCase();
```

Using `satisfies` validates the structure while preserving narrowed types:

```ts
const colorsSatisfies = {
  red: "#ff0000",
  green: "#00ff00",
  blue: 255,
  yellow: "#ffff00",
  // Error: "yelow" is not in type ColorMap
  // yelow: "#ffff00"
} satisfies ColorMap;

// red stays narrowed to 'string'
type RedHexSatisfies = typeof colorsSatisfies.red;
const redUpper = colorsSatisfies.red.toUpperCase(); // "#FF0000"
```

Use `satisfies` when you need both structural validation and precise type inference.
