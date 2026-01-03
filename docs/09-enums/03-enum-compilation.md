# Enum Compilation

Unlike most TypeScript features, enums generate additional JavaScript code at runtime. Let's see what happens when we compile this enum:

```typescript
enum Class {
  Rogue,
  Mage,
  Warrior,
  Priest,
}
```

We get a JavaScript object that looks like this:

```javascript
var Class;
(function (Class) {
  Class[(Class["Rogue"] = 0)] = "Rogue";
  Class[(Class["Mage"] = 1)] = "Mage";
  Class[(Class["Warrior"] = 2)] = "Warrior";
  Class[(Class["Priest"] = 3)] = "Priest";
})(Class || (Class = {}));
```

This generated code creates the **bidirectional mapping** that we talked about before:

- From name to value: `Class["Rogue"] = 0`
- From value to name: `Class[0] = "Rogue"`

## String Enum Compilation

Strings compile in a similar way:

```typescript
enum Class {
  Rogue = "Rogue",
  Mage = "Mage",
  Warrior = "Warrior",
  Priest = "Priest",
}
```

Compiles to:

```javascript
var Class;
(function (Class) {
  Class["Rogue"] = "Rogue";
  Class["Mage"] = "Mage";
  Class["Warrior"] = "Warrior";
  Class["Priest"] = "Priest";
})(Class || (Class = {}));
```

**String enums do not support reverse mapping** — the compiled JavaScript only maps from name to string value, not the other way around.
