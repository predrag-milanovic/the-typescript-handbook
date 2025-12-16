# Dynamic Keys

Sometimes you don't know all of an object's property names in advance. For example, imagine building a customer management system where employees can add custom key/value pairs to customer records:

- `favoriteColor: "green"`
- `favoriteFood: "burger"`
- `favoriteAnimal: "dog"`
- etc.

You can't predict what users will add ahead of time, but you still want type safety for the data structure.

## Index Signatures

You can define dynamic keys using an [**index signature**](https://www.typescriptlang.org/docs/handbook/2/objects.html#index-signatures):

```ts
type UserMetrics = {
  [key: string]: number;
};
```

This type says: "this object can have any number of properties where keys are strings and values are numbers."

## Using Dynamic Keys

Once defined, you can create objects that conform to the type:

```ts
const metrics: UserMetrics = {
  wordsPerMinute: 50,
  errors: 2,
  timeOnPage: 120,
};
```

You can add new properties dynamically:

```ts
metrics["refreshRate"] = 60; // OK
metrics["theme"] = "dark"; // Error: Type 'string' is not assignable to type 'number'
```

TypeScript enforces the value type even for dynamically added keys, ensuring type safety throughout your code.
