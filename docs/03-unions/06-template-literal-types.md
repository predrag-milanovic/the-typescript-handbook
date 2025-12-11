# Template Literal Types

Template literal types are one of TypeScript's most powerful features for creating string-based type constraints. They use JavaScript's template literal syntax to generate unions of string literal types programmatically.

## Basic Usage

Start with a simple union type:

```typescript
type Class = "wizard" | "warrior" | "rogue";
```

Use template literal syntax to create derived types:

```typescript
type Hero = `elf ${Class}`;
```

TypeScript automatically expands the template to all possible combinations:

```typescript
// Equivalent to:
type Hero = "elf wizard" | "elf warrior" | "elf rogue";
```

## Combining Multiple Unions

Template literals can combine multiple union types, creating a Cartesian product of all possibilities:

```typescript
type Class = "wizard" | "warrior" | "rogue";
type Race = "elf" | "human" | "dwarf";
type Hero = `${Race} ${Class}`;
```

This generates all nine combinations:

```typescript
// "elf wizard" | "elf warrior" | "elf rogue" 
// | "human wizard" | "human warrior" | "human rogue" 
// | "dwarf wizard" | "dwarf warrior" | "dwarf rogue"
```

## Pattern Matching with Primitives

Use primitive types in templates to enforce string patterns:

```typescript
type LogRecord = `${string}: ${number}`;
```

This creates a type that matches any string following the pattern "text: number":

```typescript
const criticalErr: LogRecord = "CRITICAL: 69";     // valid
const warningMsg: LogRecord = "WARNING: 404";      // valid

const invalid1: LogRecord = "CRITICAL 92";         // Error: missing colon
const invalid2: LogRecord = "CRITICAL: 92a";       // Error: not a number
const invalid3: LogRecord = "92: CRITICAL";        // Error: number before string
```

## Practical Applications

### Event Names

```typescript
type Events = "click" | "focus" | "blur";
type EventHandler = `on${Capitalize<Events>}`;
// "onClick" | "onFocus" | "onBlur"
```

### CSS Properties

```typescript
type Color = "red" | "blue" | "green";
type Shade = "light" | "dark";
type CssColor = `${Shade}-${Color}`;
// "light-red" | "light-blue" | "light-green" | "dark-red" | "dark-blue" | "dark-green"
```

### API Endpoints

```typescript
type Method = "GET" | "POST" | "PUT" | "DELETE";
type Resource = "users" | "posts" | "comments";
type Endpoint = `/${Resource}`;
type Route = `${Method} ${Endpoint}`;
// "GET /users" | "POST /users" | "PUT /users" | ...
```

### Version Strings

```typescript
type Version = `${number}.${number}.${number}`;

const validVersion: Version = "1.2.3";   // valid
const invalidVersion: Version = "1.2";   // Error: doesn't match pattern
```

## Performance Considerations

Be cautious when combining large unions—the number of generated types grows exponentially:

```typescript
// This creates 3 * 3 * 3 = 27 combinations
type A = "a" | "b" | "c";
type B = "x" | "y" | "z";
type C = "1" | "2" | "3";
type Combined = `${A}${B}${C}`;
```

For very large unions, consider alternative approaches to avoid performance issues.

## When to Use

- Creating string enums with systematic naming patterns
- Enforcing string format constraints
- Building type-safe routing or event systems
- Generating related types from base unions
- Validating structured string formats like logs or IDs

Template literal types combine TypeScript's type system with string manipulation, enabling compile-time validation of string patterns that would otherwise require runtime checks.