# Extending Interfaces

This is the exception to the previous rule of thumb that "you should prefer `type` over `interface`". Interfaces are a bit better when it comes to extending other interfaces (inheriting properties).

With types, you use the `&` (intersection) operator to extend types:

```typescript
type Character = {
  name: string;
  level: number;
};

type Wizard = Character & {
  spellbook: string[];
  mana: number;
};
```

With interfaces, you use the `extends` keyword:

```typescript
interface Character {
  name: string;
  level: number;
}

interface Wizard extends Character {
  spellbook: string[];
  mana: number;
}
```

In both cases, a `Wizard` now has all four properties: `name`, `level`, `spellbook`, and `mana`.

## Why Is "Interface Extends" Usually Better?

To quote [Microsoft's wiki](https://github.com/microsoft/TypeScript/wiki/Performance#preferring-interfaces-over-intersections):

> Interfaces create a single flat object type that detects property conflicts, which are usually important to resolve! Intersections on the other hand just recursively merge properties, and in some cases produce `never`. Interfaces also display consistently better, whereas type aliases to intersections can't be displayed in part of other intersections. Type relationships between interfaces are also cached, as opposed to intersection types as a whole. A final noteworthy difference is that when checking against a target intersection type, every constituent is checked before checking against the "effective"/"flattened" type.

For this reason, extending types with `interfaces`/`extends` is suggested over creating intersection types.

Put simply, with interfaces the developer ergonomics are a bit better and compilation is a bit faster.
