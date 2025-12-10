# Literal Types

Literal types allow you to specify that a variable can only be a specific literal value. This is a powerful feature for constraining what values are accepted, making your code more type-safe.

## The Problem

Consider a `move` function that accepts a direction:

```ts
function move(direction: string) {
  // Implementation...
}
```

This accepts *any* string — "north", "south", "invalid", "anything" — which is too permissive. We need to narrow the possible values.

## The Solution: Literal Types

Use a literal value as a type to restrict to that exact value:

```ts
function move(direction: "north") {
  // Implementation...
}

move("north");  // valid
move("south");  // error
```

Now `direction` can only be the string `"north"`.

## Combining Literals with Unions

Literal types become powerful when combined with unions to restrict a variable to a specific set of values:

```ts
function move(direction: "north" | "south" | "east" | "west"): void {
  console.log(`Moving ${direction}`);
}

move("north");   // valid
move("south");   // valid
move("left");    // error
```

## Literal Type Examples

**String literals:**

```ts
type Status = "idle" | "loading" | "success" | "error";

function setStatus(status: Status): void {
  // ...
}

setStatus("loading");  // valid
setStatus("pending");  // error
```

**Number literals:**

```ts
function selectCard(cardNumber: 1 | 2 | 3 | 4): void {
  // ...
}

selectCard(2);  // valid
selectCard(5);  // error
```

**Boolean literals:**

```ts
type Mode = true | false;  // equivalent to just boolean, but useful when paired with other types
```

## With Type Aliases

Use `type` aliases to name common literal unions:

```ts
type HttpMethod = "GET" | "POST" | "PUT" | "DELETE";
type LogLevel = "debug" | "info" | "warn" | "error";

function request(method: HttpMethod, path: string): void {
  // ...
}

function log(level: LogLevel, message: string): void {
  // ...
}
```

## Type Narrowing with Literals

Literal types work with type narrowing:

```ts
function handleEvent(type: "click" | "hover" | "focus"): void {
  if (type === "click") {
    // type is narrowed to "click"
    console.log("clicked");
  } else if (type === "hover") {
    // type is narrowed to "hover"
    console.log("hovered");
  }
}
```

## vs Enums

While TypeScript has `enum`, literal type unions are lightweight and often preferable:

```ts
// Literal union (preferred for simple cases)
type Direction = "north" | "south" | "east" | "west";

// Enum (more verbose, but useful for complex scenarios)
enum DirectionEnum {
  North = "north",
  South = "south",
  East = "east",
  West = "west",
}
```

## Key Takeaway

Literal types restrict variables to specific exact values. Combine them with unions to create powerful, type-safe APIs that only accept intended values. They're a lightweight alternative to enums for many use cases.
