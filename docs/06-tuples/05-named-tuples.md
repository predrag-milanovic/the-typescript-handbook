# Named Tuples

Position-based access in tuples can be hard to read. You can label tuple elements (often called "named tuples") to make types more descriptive in your editor and tooling.

```ts
// Unlabeled
type UserData = [string, number, boolean];

// Labeled (named tuple)
type UserDataLabeled = [name: string, age: number, isAdmin: boolean];
```

Labels make the type self-descriptive and improve editor hints:

```ts
// Your editor shows the full type:
// [name: string, age: number, isAdmin: boolean]
function getUser(): UserDataLabeled {
	return ["Frodo", 33, false];
}
```

## Labels Are Documentation Only

Labels are for TypeScript tooling; they don't change how values are accessed. Tuple access and destructuring are still positional.

```ts
const user: [name: string, age: number] = ["Bilbo", 111];

// Destructure in reverse order
const [age, name] = user;
console.log(age); // "Bilbo"
console.log(name); // 111
```

Even though the labels say `name` then `age`, the variables you choose in destructuring don't matter—only the positions do. In this example, `age` is inferred as `string` and `name` as `number` because they map to the 0th and 1st elements respectively.

### Tips
- Use labels to improve readability and editor tooltips.
- Remember: labels do not affect runtime or access order—tuples remain positional.
- Prefer objects for larger or evolving data structures; use tuples for small, fixed shapes.

