# Tuples vs. Objects

So why would you use a tuple instead of an object? For example, this:

```ts
function getCoordinates(): [number, number] {
	return [40.7128, -74.006]; // latitude, longitude
}
```

Instead of this:

```ts
function getCoordinatesAsObject(): { lat: number; lng: number } {
	return { lat: 40.7128, lng: -74.006 };
}
```

Coordinates have a conventional order (latitude, then longitude), so a tuple’s positional semantics fit well. Objects are clearer for named access (e.g., `coords.lat`).

## Counterexample

I would probably model a user as an object:

```ts
type User = { name: string; age: number; email: string };
const user: User = { age: 60, name: "Lane", email: "super@secret.com" };
```

A tuple like `[string, number, string]` would be confusing — `user[0]` for name? `user[2]` for email? Objects’ descriptive keys are more intuitive.

