# Enums

[Enums](https://www.typescriptlang.org/docs/handbook/enums.html) are a set of defined constants. The simplest form of enum is a numeric enum:

```typescript
enum Direction {
  North, // 0
  East, // 1
  South, // 2
  West, // 3
}

let myDirection: Direction = Direction.North;
console.log(myDirection); // Outputs: 0
```

The killer feature of enums is that in your code you can have nicely named identifiers like `Direction.North`, and under the hood you can have simple unique values, like `0`. TypeScript automatically increments the underlying values for us as we define new enums.

You can also explicitly set the values, and TypeScript will ensure they're unique:

```typescript
enum StatusCode {
  OK = 200,
  Created = 201,
  BadRequest = 400,
  Unauthorized = 401,
  NotFound = 404,
}
```

## Bidirectional Mapping

Numeric enums are bidirectional, which just means you can easily convert from the underlying value to the name and vice versa:

```typescript
const directionValue: number = Direction.South;
// 2
const directionName: string = Direction[directionValue];
// "South"
```
