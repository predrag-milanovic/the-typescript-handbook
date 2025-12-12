# Arrays

Arrays in TypeScript are typed collections of elements. Use bracket notation to specify the element type: `string[]`, `number[]`, `boolean[]`, etc.

## Basic Syntax

The simplest way to declare an array type is with bracket notation following the element type:

```typescript
let colors: string[] = ["red", "green", "blue"];
let scores: number[] = [95, 87, 92];
let active: boolean[] = [true, true, false];
```

TypeScript automatically infers the array type from values:

```typescript
let colors = ["red", "green"];  // inferred as string[]
let scores = [95, 87];           // inferred as number[]
```

## Working with Arrays

Iterate over arrays using standard JavaScript patterns:

```typescript
function logProducts(products: string[]) {
  for (let product of products) {
    console.log(`In stock: ${product}`);
  }
}

logProducts(["Laptop", "Mouse", "Keyboard"]);
// In stock: Laptop
// In stock: Mouse
// In stock: Keyboard
```

Use array methods with full type safety:

```typescript
const temperatures: number[] = [72, 68, 75, 71, 76];

// map preserves type safety
const celsius = temperatures.map(f => (f - 32) * 5/9);
// celsius is inferred as number[]

// filter also maintains types
const hot = temperatures.filter(t => t > 73);
// hot is number[]
```

## Array Methods

TypeScript provides type-safe access to all standard array methods:

```typescript
const languages: string[] = ["TypeScript", "Python", "Rust"];

languages.push("Go");             // valid
languages.push(2024);             // Error: type mismatch

const first = languages[0];       // string
const total = languages.length;   // number

const list = languages.join(" → "); // "TypeScript → Python → Rust → Go"
```

## Union Arrays

Arrays can contain union types when elements might be multiple types:

```typescript
let mixed: (string | number)[] = ["hello", 42, "world", 100];

// Proper syntax: parentheses required
let mixed: (string | number)[];   // correct

// Without parentheses
let wrong: string | number[];     // wrong! means string OR number[]
```

## Readonly Arrays

Prevent accidental modifications to arrays using `readonly`:

```typescript
function displayTags(tags: readonly string[]) {
  // tags.push("new-tag");  // Error: push not allowed on readonly array
  console.log(tags[0]);      // valid
}

const config: readonly string[] = ["dev", "test", "prod"];
// config[0] = "staging";  // Error: cannot modify readonly array
```

## Array of Objects

Arrays commonly hold objects with typed properties:

```typescript
interface Book {
  title: string;
  pages: number;
}

function summarizeBooks(books: Book[]) {
  for (const book of books) {
    console.log(`${book.title} has ${book.pages} pages`);
  }
}

summarizeBooks([
  { title: "Clean Code", pages: 464 },
  { title: "Design Patterns", pages: 416 },
]);
```

## Generic Array Type

TypeScript also supports the generic `Array<T>` syntax (less common):

```typescript
let cities: Array<string> = ["Tokyo", "Paris"];
let populations: Array<number> = [37400068, 2161000];

// Equivalent to:
let cities: string[] = ["Tokyo", "Paris"];
let populations: number[] = [37400068, 2161000];
```

The bracket notation `T[]` is preferred for clarity and readability.

## Common Mistakes

**Wrong union syntax without parentheses:**

```typescript
// This means: string OR array of numbers
let wrong: string | number[];

// This means: array of strings or numbers (correct)
let correct: (string | number)[];
```

**Forgetting readonly for immutable arrays:**

```typescript
// This allows mutations
let numbers: number[] = [1, 2, 3];
numbers.push(4); // allowed

// This prevents mutations
let immutable: readonly number[] = [1, 2, 3];
// immutable.push(4); // Error
```

## Empty Arrays

Empty array literals need type hints:

```typescript
let empty: string[] = [];     // valid
let empty = [];               // inferred as never[] (too permissive)

// Better: be explicit about intended type
let items: string[] = [];
```

## Nested Arrays

Arrays can contain other arrays:

```typescript
let board: number[][] = [
  [1, 0, 1],
  [0, 1, 0],
  [1, 1, 0],
];

// Or with generic syntax
let schedule: Array<Array<string>> = [
  ["Mon", "Wed", "Fri"],
  ["Tue", "Thu"],
];
```