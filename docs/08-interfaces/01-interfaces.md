# Interfaces

There are two ways to define object types: the `type` keyword (as we've seen with type aliases) and `interface`:

```typescript
type Superhero = {
  name: string;
  powers: string[];
  isAvenger: boolean;
};

interface Superhero {
  name: string;
  powers: string[];
  isAvenger: boolean;
}
```

I'm a huge fan of having multiple ways to do the same things in a language.

In 9/10 scenarios, they work the same way, but there are a few key differences that we'll cover in this chapter. For now, just know that I recommend using `type` in [most cases](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#differences-between-type-aliases-and-interfaces), but there are a few scenarios where `interface` is the better choice, which we'll talk about later.
