# Giant Unions

Complex union types can explode in size faster than expected. Understanding these limitations helps you design practical type systems.

## The Problem

Consider building a `MoveMessage` type for a game:

```typescript
type Distance = 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9;
type Class =
  | "Warrior"
  | "Rogue"
  | "Mage"
  | "Cleric"
  | "Paladin"
  | "Druid"
  | "Hunter"
  | "Shaman";
type MoveMessage =
  `The ${Class} moves ${Distance}, ${Distance}, ${Distance}, ${Distance}, then ${Distance}.`;

const message: MoveMessage = "The Warrior moves 6, 2, 5, 4, then 7.";
```

This will likely produce an error:

```
Error: Expression produces a union type that is too complex to represent.
```

## Why It Fails

The union above creates hundreds of thousands of combinations:

- 8 classes × 9^5 distances = **472,392 possible strings**

Even a simpler version with three distance values:

```typescript
type MoveMessage =
  `The ${Class} moves ${Distance}, ${Distance}, then ${Distance}.`;
```

Still generates over **5,800 combinations** (8 × 9^3).

TypeScript has internal limits to prevent performance degradation. Extremely large unions:

- Slow down editor responsiveness
- Increase compilation time dramatically
- Consume excessive memory
- Make type-checking impractical

## The Combinatorial Explosion

Template literal types with multiple unions create a Cartesian product:

```typescript
// 2 × 2 = 4 combinations
type Small = `${("a" | "b")} ${("x" | "y")}`;

// 3 × 3 × 3 = 27 combinations
type Medium = `${("a" | "b" | "c")} ${("x" | "y" | "z")} ${("1" | "2" | "3")}`;

// 10 × 10 × 10 × 10 = 10,000 combinations
type Large = `${TenOptions} ${TenOptions} ${TenOptions} ${TenOptions}`;
```

Growth is exponential, not linear.

## Practical Solutions

### Use Simpler Types

Sometimes a basic `string` is the right choice:

```typescript
type MoveMessage = string;

// Or add minimal constraints
type MoveMessage = `The ${string} moves ${string}`;
```

### Runtime Validation

Move validation from compile-time to runtime when types become impractical:

```typescript
type MoveMessage = string;

function validateMoveMessage(msg: MoveMessage): boolean {
  const pattern = /^The (Warrior|Rogue|Mage|...) moves \d, \d, \d, \d, then \d\.$/;
  return pattern.test(msg);
}
```

### Builder Patterns

Use functions to construct valid values instead of exhaustive type unions:

```typescript
type Class = "Warrior" | "Rogue" | "Mage";
type Distance = 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9;

function createMoveMessage(
  characterClass: Class,
  distances: Distance[]
): string {
  return `The ${characterClass} moves ${distances.join(", then ")}.`;
}
```

### Branded Types

Use branded types for nominal typing without exhaustive unions:

```typescript
type MoveMessage = string & { readonly __brand: "MoveMessage" };

function createMoveMessage(
  characterClass: Class,
  distances: Distance[]
): MoveMessage {
  return `The ${characterClass} moves ${distances.join(", then ")}.` as MoveMessage;
}
```

## Guidelines

**Keep unions manageable**: Aim for dozens or hundreds of combinations, not thousands.

**Consider alternatives**: If your union would be huge, there's usually a better approach.

**Balance precision with practicality**: Overly specific types can harm developer experience.

**Test compilation speed**: If types slow down your editor, simplify them.

## When to Stop

If you encounter "union type too complex" errors, it's a signal to reconsider your approach. TypeScript's type system is powerful, but it has pragmatic limits designed to maintain usability.

Not every constraint needs compile-time enforcement. Sometimes runtime validation or simpler types serve your codebase better than exhaustive type unions.