# Value Unions

Value unions combine literal types with union types to create precise, constrained APIs. They're particularly useful for parameters that should only accept a specific set of string or numeric values.

## From Literal to Union

Start with a simple literal type:

```typescript
function move(direction: "north") {
  // Implementation...
}
```

This function only accepts one value, which isn't very useful.

## Expanding with Unions

Combine literal types using unions to allow multiple specific values:

```typescript
function move(direction: "north" | "south" | "east" | "west") {
  // Implementation...
}
```

Now the function accepts exactly four directions, nothing more, nothing less.

## Type Alias for Reusability

Extract the union into a type alias for better code organization:

```typescript
type Direction = "north" | "south" | "east" | "west";

function move(direction: Direction) {
  // Implementation...
}
```

## Benefits

**Type Safety**: TypeScript catches invalid values at compile time:

```typescript
move("north");     // valid
move("northeast"); // Error: not assignable to type 'Direction'
```

**Autocomplete**: Editors provide intelligent suggestions for valid values.

**Self-Documenting**: The type clearly communicates what values are acceptable.

**Refactoring**: Changing the type definition updates all usages automatically.

## Real-World Patterns

### Status Values

```typescript
type Status = "pending" | "approved" | "rejected";

function updateStatus(status: Status) {
  // Implementation...
}
```

### HTTP Methods

```typescript
type HttpMethod = "GET" | "POST" | "PUT" | "DELETE";

function request(method: HttpMethod, url: string) {
  // Implementation...
}
```

### Numeric Unions

```typescript
type DiceRoll = 1 | 2 | 3 | 4 | 5 | 6;

function rollDice(): DiceRoll {
  return (Math.floor(Math.random() * 6) + 1) as DiceRoll;
}
```

## When to Use

- Function parameters with a fixed set of options
- Configuration values with predefined choices
- State machines with known states
- API responses with specific status codes

Value unions create contracts between different parts of your code, making it impossible to pass invalid values while keeping the code readable and maintainable.