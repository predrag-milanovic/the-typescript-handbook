# Intersections of Types

An [intersection type](https://www.typescriptlang.org/docs/handbook/2/objects.html#intersection-types) combines multiple types into one with the `&` operator. The resulting intersection type satisfies all the component types simultaneously.

```ts
type IndividualContributor = {
  id: number;
  name: string;
  tasks: string[];
};

type Manager = {
  directReports: number[];
};

type GoodManager = IndividualContributor & Manager;

const predrag: GoodManager = {
  id: 1,
  name: "Predrag Milanovic",
  tasks: ["Fixing B*llsh*t code", "Vibe Coding"],
  directReports: [2, 3, 4],
};
```

A `GoodManager` must have all the properties of both an `IndividualContributor` and a `Manager`. When you intersect object types, TypeScript merges their properties:

```ts
type Point2D = {
  x: number;
  y: number;
};

type Point3D = Point2D & {
  z: number;
};

// Equivalent to:
// type Point3D = {
//   x: number;
//   y: number;
//   z: number;
// };
```
