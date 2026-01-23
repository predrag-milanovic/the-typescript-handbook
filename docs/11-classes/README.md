# Classes

Classes in TypeScript build on JavaScript's class syntax and add powerful type-system features: access modifiers, abstract classes, interface implementation, and more precise handling of `this` and constructor parameters.

## Contents

1. **[Classes](01-classes.md)** — Introduces TypeScript classes, including typed fields, constructors, and methods, and shows how static typing helps catch mistakes when creating and using class instances.

2. **[Private Class Members](02-private-class-members.md)** — Explains JavaScript's `#` private fields, how TypeScript understands them, and how compile-time errors prevent invalid access to truly private state.

3. **[TypeScript Public and Private](03-typescript-public-and-private.md)** — Covers TypeScript's `private` (and related) access modifiers, how they differ from `#` private fields, and guidance on when to prefer the JavaScript-native syntax.

4. **[Protected Data Members](04-protected-data-members.md)** — Describes the TypeScript-only `protected` keyword, allowing subclasses (but not outside code) to access certain members, and contrasts it with `private` and public members.

5. **[Abstract Classes and Methods](05-abstract-classes-and-methods.md)** — Shows how to use `abstract` classes and members to define shared templates that cannot be instantiated directly but enforce implementations in subclasses.

6. **[Classes Implement Interfaces](06-classes-implement-interfaces.md)** — Demonstrates using the `implements` clause so classes must satisfy one or more interfaces, enabling interchangeable behavior-based designs.

7. **[Classes vs. Interfaces and Types](07-classes-vs.-interfaces-and-types.md)** — Compares classes, interfaces, and type aliases for modeling object shapes, and explains when to reach for runtime-capable classes versus compile-time-only types.

8. **[The `this` Type](08-the-'this'-type.md)** — Explores how TypeScript types `this` inside class methods, including explicit `this` parameters that keep callbacks correctly typed when methods are passed around.

9. **[Parameter Properties](09-parameter-properties.md)** — Introduces constructor parameter properties for concise field declaration and initialization, and notes their limitations with `#`-style private fields.

