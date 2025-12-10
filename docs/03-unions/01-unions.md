# Unions

Union types let you specify that a value can be one of several types. Use the pipe symbol (`|`) to separate types:

```ts
// userId is a string OR a number
let userId: string | number;
userId = "user_42";  // valid
userId = 42;         // valid
userId = true;       // error
```

## Type Narrowing

One powerful feature of TypeScript is **type narrowing**: when you check a value's type, TypeScript automatically refines the type in that branch. This makes it safe to access type-specific properties or call type-specific methods.

Example with `typeof`:

```ts
function safeSquare(val: string | number): number {
  if (typeof val === "string") {
    // Inside this block, val is narrowed to string
    val = parseInt(val, 10);
  }
  // Now val is only a number
  return val * val;
}

let result = safeSquare("5");
console.log(result);  // 25

result = safeSquare(5);
console.log(result);  // 25
```

## More Narrowing Examples

Using `instanceof` for objects:

```ts
class Dog {
  bark() { console.log("Woof!"); }
}

class Cat {
  meow() { console.log("Meow!"); }
}

function makeSound(pet: Dog | Cat) {
  if (pet instanceof Dog) {
    pet.bark();  // safe: pet is narrowed to Dog
  } else {
    pet.meow();  // safe: pet is narrowed to Cat
  }
}
```

Checking for property existence:

```ts
type Bird = { fly: () => void };
type Fish = { swim: () => void };

function move(animal: Bird | Fish) {
  if ("fly" in animal) {
    animal.fly();
  } else {
    animal.swim();
  }
}
```

## Use Cases

- **API responses**: A field might be `User | Error`
- **Configuration**: A setting might accept `string | number | boolean`
- **Flexible parameters**: Functions that accept multiple input types
- **Optional values**: `T | null` or `T | undefined`

## Key Takeaway

Unions let you express that a value can be multiple types. Use type narrowing (conditionals) to safely access type-specific operations without casts or assertions.
