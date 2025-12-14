# Extra Properties

TypeScript distinguishes between passing objects through variables versus passing object literals directly. This distinction affects how "excess property checking" is applied.

## The Rule

When passing objects to functions:

- **With a variable**: Extra properties are allowed (structural typing)
- **With an object literal**: Extra properties cause errors (excess property checking)

## Variables with Extra Properties

When you assign an object to a variable and then pass it to a function, TypeScript allows extra properties:

```typescript
type Dog = {
  name: string;
  breed: string;
};

function describeDog(dog: Dog) {
  console.log(`${dog.name} is a ${dog.breed}`);
}

// Create object with extra property
const myDog = {
  name: "Max",
  breed: "Golden Retriever",
  age: 3,  // extra property
};

// This is allowed
describeDog(myDog);
// Max is a Golden Retriever
```

The function `describeDog` only needs `name` and `breed`. Since we're passing through a variable, TypeScript allows the extra `age` property.

## Object Literals with Extra Properties

When you pass an object literal directly (without a variable), TypeScript enforces strict excess property checking:

```typescript
const myDog = {
  name: "Max",
  breed: "Golden Retriever",
  age: 3,
};

// Error: Object literal may only specify known properties, 
// and 'age' does not exist in type 'Dog'
describeDog({
  name: "Max",
  breed: "Golden Retriever",
  age: 3,
});
```

TypeScript rejects the literal because it contains `age`, which is not in the `Dog` type.

## Why the Difference?

**With variables**: TypeScript applies structural typing. If an object has at least the required properties, it's compatible, even if it has extras.

**With literals**: TypeScript applies excess property checking to catch typos and potential mistakes early.

```typescript
// Scenario 1: Maybe you meant 'age' as a different property?
describeDog({ name: "Max", breed: "Golden Retriever", agee: 3 });
// Error helps catch this typo

// Scenario 2: Maybe you're using the wrong type?
describeDog({ name: "Max", breed: "Golden Retriever", owner: "Alice" });
// Error flags that 'owner' is unexpected
```

## Workarounds

### 1. Use a Variable (Bypass Checking)

```typescript
const input = {
  name: "Max",
  breed: "Golden Retriever",
  age: 3,
};

describeDog(input);  // allowed
```

### 2. Use Type Assertion (Explicitly Tell TypeScript)

```typescript
describeDog({
  name: "Max",
  breed: "Golden Retriever",
  age: 3,
} as Dog);  // explicitly assert it's a Dog
```

### 3. Add the Property to the Type

```typescript
type Dog = {
  name: string;
  breed: string;
  age?: number;  // make it optional
};

describeDog({
  name: "Max",
  breed: "Golden Retriever",
  age: 3,
});  // now allowed
```

## Real-World Examples

### API Request Bodies

```typescript
type CreateUserRequest = {
  email: string;
  password: string;
};

function registerUser(req: CreateUserRequest) {
  // Process registration
}

// This works (variable)
const newUser = {
  email: "alice@example.com",
  password: "secure123",
  referralCode: "FRIEND2025",
};
registerUser(newUser);

// This fails (literal)
registerUser({
  email: "bob@example.com",
  password: "secure456",
  referralCode: "FRIEND2025",  // Error: not in type
});
```

### Configuration Objects

```typescript
type ServerOptions = {
  port: number;
  hostname: string;
};

function startServer(opts: ServerOptions) {
  // Start server
}

// Variable: allowed
const config = {
  port: 3000,
  hostname: "localhost",
  ssl: true,  // extra property
};
startServer(config);

// Literal: not allowed
startServer({
  port: 3000,
  hostname: "localhost",
  ssl: true,  // Error
});
```

## Best Practices

**Be aware of the behavior**: Understand when excess property checking applies.

**Prefer variables for flexibility**: If you genuinely have extra properties, use a variable.

**Update types when needed**: If extra properties are intentional, add them to the type as optional.

**Use `as const` for specific types**:

```typescript
const config = {
  port: 3000,
  hostname: "localhost",
} as const;

startServer(config);  // TypeScript infers exact literal types
```

## Configuration Note

This behavior can be configured in [`tsconfig.json`](https://www.typescriptlang.org/tsconfig/#strict). We'll cover TypeScript configuration later in the course. For now, remember the default behavior:

- Variables: extra properties allowed
- Object literals: extra properties rejected

## Summary

- **Variables bypass excess property checking**: Extra properties are allowed if the required properties exist.
- **Object literals trigger strict checking**: Extra properties cause compile errors.
- **The difference helps catch typos**: Excess property checking is a feature, not a bug.
- **You have workarounds**: Use variables, type assertions, or update the type.

This behavior is a balance between flexibility (structural typing) and safety (catching mistakes early). Understanding when each applies helps you write TypeScript that catches bugs before they reach production.
