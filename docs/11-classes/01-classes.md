# Classes

Classes in TypeScript work mostly the same way that they do in JavaScript, but with the added benefit of static typing. One of the biggest differences is that you'll see type annotations on all the class properties at the top level of the class declaration.

```typescript
class Hero {
  name: string;
  health: number;

  constructor(name: string, health: number) {
    this.name = name;
    this.health = health;
  }

  attack(damage: number): void {
    console.log(`${this.name} attacks for ${damage} damage!`);
  }

  getHealth() {
    return this.health;
  }
}

// Create an instance
const geralt = new Hero("Geralt", 100);
geralt.attack(25);
// "Geralt attacks for 25 damage!"
console.log(geralt.getHealth());
// 100
```

## Key Points

- **Property Declarations**: Class properties must be declared at the top of the class with their types
- **Constructor**: The constructor method initializes the instance properties
- **Methods**: Class methods can have typed parameters and return types
- **Type Safety**: TypeScript ensures all property assignments and method calls are type-safe
