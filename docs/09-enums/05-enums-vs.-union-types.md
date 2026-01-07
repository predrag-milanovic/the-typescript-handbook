# Enums vs. Union Types

Sometimes you’ll see code model a fixed set of options with an `enum`:

```typescript
enum CardSuit {
	Hearts = "Hearts",
	Diamonds = "Diamonds",
	Clubs = "Clubs",
	Spades = "Spades",
}
```

But you can represent the same idea with a union of string literals:

```typescript
type CardSuit = "Hearts" | "Diamonds" | "Clubs" | "Spades";
```

Both approaches let you constrain values and get good editor tooling. The choice mostly comes down to trade-offs in refactoring ergonomics and runtime behavior.

## Pros of Unions

- Consistency: You already use unions for complex types; using them for primitives keeps your type style consistent.
- Zero runtime: Unions are erased at compile time, so they add no JavaScript code or payload.
- Brevity: They’re concise to declare and easy to extend or narrow.

## Pros of Enums

- Refactor-friendly values: If you change an enum member’s value (e.g., `"Hearts"` → `"hearts"`), you don’t need to update every usage site—callers still reference `CardSuit.Hearts`.
- Numeric reverse mapping: Numeric enums provide reverse lookups, which can be handy in some scenarios.
- Namespaced context: `CardSuit.Hearts` can read clearer than a bare string like `"Hearts"`. That said, modern editors usually show the type on hover, so the benefit is modest.

## Practical Guidance

- Prefer unions for most “label-like” sets where you don’t need reverse mapping or extra runtime constructs.
- Reach for enums when you specifically want namespacing or numeric reverse mapping, or when changing the underlying serialized value without touching call sites is a priority.

Personally, I use unions over enums most of the time. Even Anders Hejlsberg (the creator of TypeScript) has noted that if they were starting over, enums might not be added. Video [here](https://www.youtube.com/watch?v=vBJF0cJ_3G0&t=1012s).

