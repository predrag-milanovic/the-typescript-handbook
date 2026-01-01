Interfaces
==========

Interfaces are one of two ways to define object types in TypeScript. The other way is using the `type` keyword with type aliases. In most scenarios they work the same way, but there are key differences that make each better in specific situations.

## Basic Syntax

Both approaches define the same structure:

**Type Alias:**
```ts
type Superhero = {
  name: string;
  powers: string[];
  isAvenger: boolean;
};
```

**Interface:**
```ts
interface Superhero {
  name: string;
  powers: string[];
  isAvenger: boolean;
}
```

In general, `type` is recommended in most cases, but interfaces shine when extending other interfaces.

## Extending Interfaces

Interfaces are superior when it comes to inheritance. Use the `extends` keyword to add properties from a base interface:

**With Interfaces (Recommended):**
```ts
interface Character {
  name: string;
  level: number;
}

interface Wizard extends Character {
  spellbook: string[];
  mana: number;
}
```

**With Types (Using Intersection):**
```ts
type Character = {
  name: string;
  level: number;
};

type Wizard = Character & {
  spellbook: string[];
  mana: number;
};
```

Interface extension is better because it creates a single flat object type, detects property conflicts, and has better performance during type checking.

## Extending Multiple Interfaces

An interface can extend multiple interfaces simultaneously, enabling composition of complex types:

```ts
interface Character {
  name: string;
  level: number;
}

interface Magical {
  mana: number;
  castSpell(spell: string): void;
}

interface Physical {
  strength: number;
  attack(): void;
}

interface BattleMage extends Character, Magical, Physical {
  combineAttacks(): void;
}
```

The `BattleMage` now has all properties and methods from its parent interfaces.

You can also mix types and interfaces in inheritance:

```ts
interface BattleMage extends Character, Magical, Physical {
  // ...
}
```

## Overriding Interface Properties

When extending an interface, you can override properties as long as the new type is **compatible** with the original:

```ts
interface Character {
  rank: string | number;
  name: string;
  level: number;
}

interface Wizard extends Character {
  // Narrowing is allowed—number is assignable to string | number
  rank: number;
  mana: number;
}
```

Overriding with an incompatible type causes an error:

```ts
interface Character {
  rank: string;
  name: string;
  level: number;
}

interface Wizard extends Character {
  // Error: number is not assignable to string
  rank: number;
  mana: number;
}
```

## Declaration Merging

A unique feature of interfaces is **declaration merging**: multiple declarations with the same name are automatically combined.

```ts
interface Spaceship {
  name: string;
}

interface Spaceship {
  engines: number;
}

interface Spaceship {
  lightSpeed: boolean;
}

// Results in:
// interface Spaceship {
//   name: string;
//   engines: number;
//   lightSpeed: boolean;
// }
```

This can be useful in niche cases (like extending the global `Window` type in browsers), but it's often a source of confusion and bugs. This is another reason `type` is usually preferred—types cannot be redeclared:

```ts
type Spaceship = {
  name: string;
};

// Error: Duplicate identifier 'Spaceship'
type Spaceship = {
  engines: number;
};
```

## When to Use Interfaces vs Types

- **Use `interface`**: When building inheritance hierarchies or extending other interfaces. Interfaces have better performance and error messages.
- **Use `type`**: For most other cases. Types are more flexible and declaration merging is prevented by default.
