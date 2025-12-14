# Object Literal Types

[Object literal types](https://www.typescriptlang.org/docs/handbook/2/objects.html) describe the shape and structure of objects. They are one of TypeScript's most powerful upgrades from JavaScript, catching property typos and enforcing correct shapes at compile time.

## Basic Object Type Syntax

Define an object type inline using literal syntax:

```typescript
function displayCar(car: { brand: string; year: number }) {
  console.log(`${car.brand} from ${car.year}`);
}

displayCar({ brand: "Tesla", year: 2024 });
// Tesla from 2024

displayCar({ brand: "BMW", model: "M3" });
// Error: Object literal may only specify known properties, and 'model' does not exist
```

## Defining Type Aliases

For reusability and clarity, extract object types into type aliases:

```typescript
type Movie = {
  title: string;
  releaseYear: number;
};

function describeMovie(movie: Movie) {
  console.log(`${movie.title} (${movie.releaseYear})`);
}

describeMovie({ title: "Inception", releaseYear: 2010 });
```

This approach keeps your code organized and makes the type reusable across functions.

## Property Types

Object properties can be any valid TypeScript type:

```typescript
type Article = {
  id: number;
  title: string;
  published: boolean;
  tags: string[];
  timestamps: { created: Date; modified: Date };
};

const article: Article = {
  id: 42,
  title: "Learning TypeScript",
  published: true,
  tags: ["typescript", "tutorial"],
  timestamps: {
    created: new Date("2025-01-01"),
    modified: new Date(),
  },
};
```

## Optional Properties

Mark properties as optional with `?`:

```typescript
type Restaurant = {
  id: number;
  name: string;
  cuisine?: string;      // optional
  rating: number;
  website?: string;       // optional
};

const pizzeria: Restaurant = {
  id: 1,
  name: "Mario's Pizzeria",
  rating: 4.5,
  // cuisine and website are optional
};

const sushi: Restaurant = {
  id: 2,
  name: "Tokyo Sushi",
  rating: 4.8,
  cuisine: "Japanese",
  website: "https://tokyosushi.com",
};
```

## Readonly Properties

Prevent modifications to specific properties:

```typescript
type DatabaseConfig = {
  readonly host: string;
  readonly database: string;
  connectionTimeout: number;  // not readonly
};

const dbConfig: DatabaseConfig = {
  host: "localhost",
  database: "production",
  connectionTimeout: 5000,
};

dbConfig.connectionTimeout = 10000;  // allowed
dbConfig.host = "remote-server";      // Error: Cannot assign to readonly property
```

## Nested Objects

Objects can contain other objects:

```typescript
type Location = {
  latitude: number;
  longitude: number;
  timezone: string;
};

type Store = {
  name: string;
  founded: number;
  location: Location;
};

const store: Store = {
  name: "Tech Hub",
  founded: 2020,
  location: {
    latitude: 40.7128,
    longitude: -74.0060,
    timezone: "EST",
  },
};
```

## Using Unions in Objects

Combine union types with object properties for flexible shapes:

```typescript
type Response = {
  status: "ok" | "failed";
  payload?: unknown;
  message?: string;
};

const success: Response = {
  status: "ok",
  payload: { count: 42, items: [] },
};

const error: Response = {
  status: "failed",
  message: "Permission denied",
};
```

## Adding Methods to Objects

Object types can include methods:

```typescript
type Logger = {
  info(msg: string): void;
  error(msg: string): void;
};

const logger: Logger = {
  info: (msg) => console.log(`[INFO] ${msg}`),
  error: (msg) => console.error(`[ERROR] ${msg}`),
};

logger.info("Server started");  // [INFO] Server started
```

## Index Signatures

Allow dynamic property keys with a consistent value type:

```typescript
type ScoreBoard = {
  [key: string]: number;
};

const scores: ScoreBoard = {
  alice: 950,
  bob: 875,
  charlie: 1050,
};

scores["diana"] = 920;  // allowed
scores["eve"] = "pending";  // Error: must be number
```

## Comparing Object Literal Types

Two object types with the same shape are compatible:

```typescript
type Coordinate = { x: number; y: number };
type Position = { x: number; y: number };

const coord: Coordinate = { x: 10, y: 20 };
const pos: Position = coord;  // allowed - same shape
```

## Common Errors

**Missing properties:**

```typescript
type Book = { title: string; isbn: string };
const book: Book = { title: "1984" };
// Error: Property 'isbn' is missing
```

**Extra properties (with strict checking):**

```typescript
const item: Book = {
  title: "Brave New World",
  isbn: "978-0060850524",
  author: "Aldous Huxley",
};
// Error: Object literal may only specify known properties
```

**Typos in property names:**

```typescript
const item: Book = {
  titel: "Dune",       // typo: 'titel' instead of 'title'
  isbn: "978-0441172719",
};
// Error: Object literal may only specify known properties
```

## Best Practices

- Define object types as named type aliases for clarity and reuse
- Use optional properties (`?`) for truly optional data, not as a substitute for union types
- Apply `readonly` to properties that should not change after initialization
- Organize nested objects into separate types for readability
- Use index signatures sparingly—prefer exact property definitions when possible
- Avoid overly broad types like `{ [key: string]: any }`

## Summary

- Object literal types describe the exact shape of objects
- Use type aliases for reusable object types
- Optional properties help model incomplete data
- Readonly properties enforce immutability
- TypeScript catches property typos and shape mismatches at compile time

Object types are the foundation of type-safe object-oriented code in TypeScript. They combine the flexibility of JavaScript objects with compile-time safety and excellent editor support.
