# Enums

Enums provide named constants for a fixed set of options. They come in two main flavors—numeric and string—and have unique runtime behavior compared to most TypeScript types.

## Quick Primer

```typescript
// Numeric enum (auto-incremented values, reverse mapping available)
enum Direction {
	North, // 0
	East,  // 1
	South, // 2
	West,  // 3
}

const d: Direction = Direction.North; // 0 under the hood
const name = Direction[d]; // "North"

// String enum (readable values, no reverse mapping)
enum LogLevel {
	ERROR = "ERROR",
	WARN = "WARN",
	INFO = "INFO",
	DEBUG = "DEBUG",
}

function log(msg: string, level: LogLevel) {
	console.log(`[${level}] ${msg}`);
}
```

## Runtime and Compilation

Unlike most TypeScript features, enums emit JavaScript. Numeric enums generate code that supports reverse mapping (value → name). String enums emit name → value mappings only. This makes enums convenient, but they add runtime weight; unions do not. See [03-enum-compilation.md](03-enum-compilation.md).

## Const Enums

`const enum` inlines values and erases the enum at compile time—no runtime object is emitted. This is great for size/perf, but you lose reverse mapping and face restrictions (no arbitrary computed members). See [04-const-enums.md](04-const-enums.md).

## Enums vs. Union Types

Many enum use cases can be modeled as unions of string literals:

```typescript
// Equivalent to a string enum for many cases
type CardSuit = "Hearts" | "Diamonds" | "Clubs" | "Spades";
```

- Prefer unions for label-like sets where you want zero runtime and concise syntax.
- Prefer enums when you need namespacing (`CardSuit.Hearts`), numeric reverse mapping, or you want to change underlying values without touching call sites.

More details in [05-enums-vs.-union-types.md](05-enums-vs.-union-types.md).

## In This Section

- [01-enums.md](01-enums.md): Basics of numeric enums and reverse mapping.
- [02-string-enums.md](02-string-enums.md): When and why to use string enums.
- [03-enum-compilation.md](03-enum-compilation.md): What JavaScript enums compile to.
- [04-const-enums.md](04-const-enums.md): Compile-time-only enums and their trade-offs.
- [05-enums-vs.-union-types.md](05-enums-vs.-union-types.md): Choosing between enums and unions.

