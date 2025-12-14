# Optional Object Properties

Optional properties allow you to define object types where some properties may or may not be present. Mark properties as optional using the [`?`](https://www.typescriptlang.org/docs/handbook/2/objects.html#optional-properties) operator.

## Basic Syntax

```typescript
type Superhero = {
  name: string;
  strength: number;
  cape?: boolean;  // optional property
};

const batman: Superhero = {
  name: "Batman",
  strength: 85,
  cape: true,
};

const clark: Superhero = {
  name: "Superman",
  strength: 100,
  // cape is optional, so it can be omitted
};
```

The `cape?` property means the field is optional—it can be present or absent.

## Optional Properties Are Union Types

When you mark a property as optional with `?`, TypeScript treats it as a union with `undefined`:

```typescript
type Superhero = {
  name: string;
  cape?: boolean;
};

// cape is actually: boolean | undefined
```

This means accessing an optional property requires checking for `undefined`:

```typescript
function useSuperpowers(hero: Superhero) {
  if (hero.cape) {
    console.log(`${hero.name} has a cape!`);
  } else {
    console.log(`${hero.name} has no cape.`);
  }
}
```

## Difference from Explicit Union

Two approaches can look similar but have different implications:

```typescript
// Approach 1: Optional property
type Hero1 = {
  name: string;
  power?: string;
};

// Approach 2: Union with undefined
type Hero2 = {
  name: string;
  power: string | undefined;
};

// Both are equivalent
const h1: Hero1 = { name: "Alice" };              // allowed
const h2: Hero2 = { name: "Bob" };                // Error: must include power

const h3: Hero2 = { name: "Bob", power: undefined };  // allowed
```

**Key difference**: Optional (`?`) allows omitting the property entirely. Union with `undefined` requires the property to exist (even if set to `undefined`).

## Required vs Optional Properties

```typescript
type Blog = {
  title: string;          // required
  author: string;         // required
  description?: string;   // optional
  publishedDate?: Date;   // optional
  viewCount?: number;     // optional
};

const post: Blog = {
  title: "Learning TypeScript",
  author: "Jane Doe",
  // description, publishedDate, and viewCount are optional
};

const fullPost: Blog = {
  title: "Advanced TypeScript",
  author: "John Smith",
  description: "Deep dive into advanced types",
  publishedDate: new Date("2025-01-15"),
  viewCount: 5420,
};
```

## Accessing Optional Properties Safely

Always check for `undefined` before using optional properties:

```typescript
type User = {
  id: number;
  name: string;
  email?: string;
  phone?: string;
};

function contactUser(user: User) {
  console.log(`User: ${user.name}`);

  // Check before using optional properties
  if (user.email) {
    console.log(`Email: ${user.email}`);
  }

  if (user.phone) {
    console.log(`Phone: ${user.phone}`);
  }
}

const guest: User = { id: 1, name: "Guest" };
contactUser(guest);  // no error, even without email or phone
```

## Optional Chaining

Use optional chaining (`?.`) to safely access nested optional properties:

```typescript
type Profile = {
  name: string;
  social?: {
    twitter?: string;
    github?: string;
  };
};

const profile: Profile = { name: "Alice" };

// Optional chaining safely accesses nested properties
const twitter = profile.social?.twitter;  // undefined, not an error
const github = profile.social?.github;    // undefined, not an error
```

## Nullish Coalescing

Provide default values for optional properties using `??`:

```typescript
type Settings = {
  theme?: string;
  fontSize?: number;
};

const userSettings: Settings = {};

const theme = userSettings.theme ?? "light";      // "light"
const fontSize = userSettings.fontSize ?? 16;     // 16

console.log(`Theme: ${theme}, Font: ${fontSize}`);
```

## Best Practices

### 1. Minimize Optional Properties

Only mark properties optional if they're genuinely optional. Too many optional properties make code harder to reason about:

```typescript
// Too permissive
type Profile = {
  name?: string;
  email?: string;
  bio?: string;
  website?: string;
};

// Better: require core fields
type Profile = {
  id: number;
  name: string;
  email: string;
  bio?: string;         // truly optional
  website?: string;     // truly optional
};
```

### 2. Avoid Deep Optional Nesting

Deeply nested optional properties create complexity:

```typescript
// Hard to reason about
type Config = {
  database?: {
    connection?: {
      timeout?: number;
    };
  };
};

// Better: separate concerns
type DatabaseConnection = {
  timeout: number;
};

type DatabaseConfig = {
  connection?: DatabaseConnection;
};

type AppConfig = {
  database?: DatabaseConfig;
};
```

### 3. Use Discriminated Unions Instead

For complex optional cases, consider discriminated unions:

```typescript
// Too many optionals
type Response = {
  success?: boolean;
  data?: unknown;
  error?: string;
  statusCode?: number;
};

// Better: discriminated union
type Response =
  | { status: "success"; data: unknown; statusCode: number }
  | { status: "error"; error: string; statusCode: number };
```

## Common Mistakes

### Don't Create Too Many Checks

```typescript
// Problematic: many optional fields create many checks
type Order = {
  id: number;
  items?: string[];
  subtotal?: number;
  tax?: number;
  shipping?: number;
  discount?: number;
};

function calculateTotal(order: Order) {
  if (order.subtotal && order.tax && order.shipping) {
    return order.subtotal + order.tax + order.shipping - (order.discount ?? 0);
  }
  // What if only some are present?
}
```

**Better approach**:

```typescript
type OrderPricing = {
  subtotal: number;
  tax: number;
  shipping: number;
  discount: number;
};

type Order = {
  id: number;
  items: string[];
  pricing?: OrderPricing;  // either all or none
};
```

### Don't Confuse Optional with Nullable

```typescript
// Optional: property may not exist
type Optional = { name?: string };
const obj1: Optional = {};  // allowed

// Nullable: property exists but can be null
type Nullable = { name: string | null };
const obj2: Nullable = { name: null };  // allowed
// const obj3: Nullable = {};  // Error: name is required
```

## Real-World Example

```typescript
type Article = {
  // Required fields
  id: number;
  title: string;
  content: string;
  author: string;
  createdAt: Date;

  // Optional fields
  coverImage?: string;
  summary?: string;
  tags?: string[];
  updatedAt?: Date;
  publishedAt?: Date;
};

function displayArticle(article: Article) {
  console.log(`${article.title} by ${article.author}`);

  if (article.coverImage) {
    console.log(`Image: ${article.coverImage}`);
  }

  if (article.summary) {
    console.log(`Summary: ${article.summary}`);
  }

  if (article.tags && article.tags.length > 0) {
    console.log(`Tags: ${article.tags.join(", ")}`);
  }
}
```

## Summary

- Mark properties optional with `?`: `property?: Type`
- Optional properties are unions with `undefined`
- Always check for `undefined` before using optional properties
- Use optional chaining (`?.`) and nullish coalescing (`??`) for safe access
- Minimize optional properties to reduce complexity and runtime checks
- Prefer required properties by default; make exceptions intentional

Optional properties are powerful for modeling real-world data structures, but use them judiciously. A well-designed type with mostly required properties is easier to work with than one with many optional fields requiring constant checks.
