# Maps

TypeScript has a [built-in](https://en.wikipedia.org/wiki/Function_(computer_programming)#Built-in_function) [`Map`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map) type for collections of key-value pairs. You can specify the types of keys and values using type parameters `<K, V>`.

## Creating Maps

```ts
// A Map with string keys and number values
const podracerSpeeds = new Map<string, number>();

podracerSpeeds.set("Anakin Skywalker", 947);
podracerSpeeds.set("Sebulba", 941);
```

TypeScript ensures type safety for both keys and values:

```ts
podracerSpeeds.set("R2-D2", true);
// Error: Argument of type 'true' is not assignable to parameter of type 'number'

podracerSpeeds.set(420, 69);
// Error: Argument of type 'number' is not assignable to parameter of type 'string'
```

## Size Property

Maps use the [`size`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map/size) property instead of `length`:

```ts
console.log(podracerSpeeds.size);
// 2
```

## Iterating Over Maps

You can easily iterate over a map using a `for...of` loop with destructuring:

```ts
for (const [racer, speed] of podracerSpeeds) {
  console.log(`${racer} raced at ${speed} speed`);
}
// Anakin raced at 947 speed
// Sebulba raced at 941 speed
```

## Common Methods

### [`get()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map/get)

Retrieve a value by key:

```ts
console.log(podracerSpeeds.get("Sebulba"));
// 941
```

### [`has()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map/has)

Check if a key exists in the map:

```ts
console.log(podracerSpeeds.has("Sebulba"));
// true
```

### [`delete()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map/delete)

Remove an entry by key:

```ts
podracerSpeeds.delete("Sebulba");
console.log(podracerSpeeds.get("Sebulba"));
// undefined
```
