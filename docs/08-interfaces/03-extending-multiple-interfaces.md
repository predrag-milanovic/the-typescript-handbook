# Extending Multiple Interfaces

TypeScript allows an interface to extend multiple interfaces simultaneously, enabling you to compose complex types from smaller, focused interfaces. This is particularly useful for creating flexible type hierarchies and promoting code reuse.

## Basic Syntax

You can extend multiple interfaces by listing them after the `extends` keyword, separated by commas:

```typescript
type Character = {
  name: string;
  level: number;
};

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

The `BattleMage` interface now has all 7 properties and methods:

- `name` (from `Character`)
- `level` (from `Character`)
- `mana` (from `Magical`)
- `castSpell` (from `Magical`)
- `strength` (from `Physical`)
- `attack` (from `Physical`)
- `combineAttacks` (defined in `BattleMage`)

## Using the Extended Interface

```typescript
const player: BattleMage = {
  name: "Gandalf",
  level: 50,
  mana: 1000,
  strength: 45,
  castSpell(spell: string) {
    console.log(`Casting ${spell}!`);
  },
  attack() {
    console.log("Physical strike!");
  },
  combineAttacks() {
    console.log("Unleashing magical and physical fury!");
  }
};

player.castSpell("Fireball");     // Casting Fireball!
player.attack();                   // Physical strike!
player.combineAttacks();           // Unleashing magical and physical fury!
```

## Real-World Example: User Permissions

Multiple interface extension is excellent for modeling systems with layered capabilities:

```typescript
interface Identifiable {
  id: string;
  createdAt: Date;
}

interface Authenticatable {
  email: string;
  passwordHash: string;
  verifyPassword(password: string): boolean;
}

interface Permissioned {
  role: "admin" | "user" | "guest";
  permissions: string[];
  hasPermission(permission: string): boolean;
}

interface AdminUser extends Identifiable, Authenticatable, Permissioned {
  adminLevel: number;
  auditLog: string[];
}
```

An `AdminUser` must implement all properties and methods from all three parent interfaces, plus its own specific properties.

## Mixing Types and Interfaces

You can extend both type aliases and interfaces, as shown in the first example where `BattleMage` extends `Character` (a type) along with two interfaces.

## Conflict Resolution

If multiple parent interfaces define the same property with different types, TypeScript will raise an error:

```typescript
interface A {
  value: string;
}

interface B {
  value: number;
}

// ❌ Error: Interface 'C' cannot simultaneously extend types 'A' and 'B'
// Named property 'value' of types 'A' and 'B' are not identical
interface C extends A, B {
  extra: boolean;
}
```

However, if the types are compatible, TypeScript will create an intersection:

```typescript
interface Vehicle {
  speed: number;
  move(): void;
}

interface Electric {
  speed: number;
  batteryLevel: number;
}

// ✅ Works: both define speed as number
interface ElectricVehicle extends Vehicle, Electric {
  charge(): void;
}
```

## Benefits of Multiple Extension

1. **Composition over inheritance**: Build complex types from simple, reusable interfaces
2. **Separation of concerns**: Each interface can represent a distinct capability
3. **Type safety**: TypeScript ensures all contracts are fulfilled
4. **Flexibility**: Objects can satisfy multiple interface contracts simultaneously
