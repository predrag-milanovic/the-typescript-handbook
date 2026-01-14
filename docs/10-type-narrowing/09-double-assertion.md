# Double Assertion

TypeScript won't allow you to assert absolute nonsense:

```typescript
const num = 42;

// Error: Conversion of type 'number' to type
// 'string' may be a mistake because neither
// type sufficiently overlaps with the other.
const str = num as string;
```

The `number` and `string` types have no overlap, making this assertion likely to be a mistake, so TypeScript complains. We can get around this with a double assertion:

```typescript
const id = 42;

// This works - but is very unsafe!
const userId = id as unknown as string;

// Now TypeScript treats this as a string
console.log(userId.toUpperCase());
// Compiles, but still CRASHES at runtime!
```

I've never used this in production code. If you see this in the wild, pray that the author was a 100x engineer that knew what they were doing.
