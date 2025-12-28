# Intersections vs. Unions

So we've covered how [unions](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#union-types) (`|`) and [intersections](https://www.typescriptlang.org/docs/handbook/2/objects.html#intersection-types) (`&`) are both used to smoosh types together... but which should you use?

## Unions

- Use the `|` operator (suspiciously similar to the logical OR operator)
- Widen the resulting type (more possible values)
- Useful for modeling mutually exclusive options or states

## Intersections

- Use the `&` operator (like logical AND)
- Narrow the resulting type (fewer possible values)
- Useful for combining multiple constraints or adding more required properties to existing types

## Example

```typescript
type Human = {
  name: string;
  age: number;
};

type Elf = {
  name: string;
  ears: "pointy";
};

// Must have name, age, and pointy ears
type ElfHuman = Human & Elf;

// Must have name (shared between Human and Elf)
// Can have either age or ears (or both)
type ElfOrHuman = Human | Elf;
```

## Key Takeaways

- Use unions to say your type is "this OR that"
- Use intersections to say your type is "this AND that", or sometimes more simply, "this with the additional properties of that"
