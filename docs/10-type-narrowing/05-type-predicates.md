# Type Predicates

Sometimes the built-in type guards ([`typeof`](https://www.typescriptlang.org/docs/handbook/2/typeof-types.html), [`instanceof`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/instanceof), etc.) aren't enough.

TypeScript allows you to create your own type guards using [type predicates](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#using-type-predicates). We do that by creating a function that:

- Accepts a wide type that we want to narrow
- Returns a boolean indicating if the value is of the desired type
- Uses the type predicate syntax `value is Type` in the return type

For example, here's a function that reports if a value is a string:

```typescript
function isString(value: unknown): value is string {
  return typeof value === "string";
}

function processValue(value: unknown) {
  if (isString(value)) {
    // TypeScript knows value is a string here
    console.log(value.toUpperCase());
  }
}
```

For simple stuff like this, we could have just inlined the `typeof` check:

```typescript
function processValue(value: unknown) {
  if (typeof value === "string") {
    // TypeScript knows value is a string here
    console.log(value.toUpperCase());
  }
}
```

But type predicates become really useful when the logic to check the type is a bit more complex. So we have a situation where one type, in this case, the `ManagerAdmin` type, shares properties with both other types:

```typescript
interface ManagerAdmin {
  accessLevel: number;
  numEmployees: number;
}

interface Admin {
  accessLevel: number;
  payrollDate: Date;
}

interface Manager {
  numEmployees: number;
}
```

We can encapsulate the slightly more complex logic in a type predicate function:

```typescript
function isManagerAdmin(
  boss: ManagerAdmin | Admin | Manager,
): boss is ManagerAdmin {
  return "numEmployees" in boss && "accessLevel" in boss;
}

// boss is a `ManagerAdmin | Admin | Manager`
if (isManagerAdmin(boss)) {
  // TypeScript knows boss is a ManagerAdmin here
  console.log(`Managing ${boss.numEmployees} employees`);
}
```
