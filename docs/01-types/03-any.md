# Any

When you compile plain JavaScript code using `tsc`, your codebase is full of [any](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#any) types.

The any type is exactly what it sounds like - a type that can be anything. The purpose of types, really, is to narrow down the possible values that a variable can hold. From that perspective, `any` is the most useless type because it doesn't narrow anything down at all! But it's important because it allows you to opt out of type-checking for a variable.

The any type is super useful when you migrate an existing JavaScript codebase to TypeScript. The (very simplified) process is:

- Change file extensions from `.js` to `.ts`,
- Get `tsc` running without errors (often works out of the box, due to `any`),
- Slowly over time, replace `any`'s with more specific types.