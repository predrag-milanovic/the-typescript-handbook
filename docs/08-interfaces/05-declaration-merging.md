Declaration Merging
===================

Declaration merging is a feature where multiple declarations with the same name are automatically combined into one. While useful in niche cases, it's often a source of confusion and bugs. This is one reason why `type` is often preferred over `interface`.

## How It Works

When you declare the same interface multiple times, all declarations merge:

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
```

The above is equivalent to:

```ts
interface Spaceship {
  name: string;
  engines: number;
  lightSpeed: boolean;
}
```

## Types Don't Merge

If you use `type` instead, redeclaring it is an error:

```ts
type Spaceship = {
  name: string;
};

// Error: Duplicate identifier 'Spaceship'
type Spaceship = {
  engines: number;
};
```

This prevents accidental redeclaration and makes the code more predictable.
