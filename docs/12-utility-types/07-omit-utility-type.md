## Omit Utility Type

[`Omit<T, K>`](https://www.typescriptlang.org/docs/handbook/utility-types.html#omittype-keys) is the opposite of `Pick<T, K>`. Instead of choosing a set of properties to **keep**, it creates a new type by **excluding** a set of properties `K` from an existing type `T`.

This is especially handy when you want to hide sensitive fields (like passwords) or remove implementation details before sending data over an API or into another layer of your application.

```ts
interface DatabaseUser {
	id: string;
	username: string;
	email: string;
	passwordHash: string;
	createdAt: Date;
	updatedAt: Date;
}

// Create a safe user representation without sensitive or internal data
type PublicUser = Omit<DatabaseUser, "passwordHash" | "updatedAt">;

function getUserProfile(userId: string): PublicUser {
	// Imagine this was fetched from a database
	const dbUser: DatabaseUser = {
		id: userId,
		username: "predragmilanovic",
		email: "predrag@example.com",
		passwordHash: "${2a$12$...}",
		createdAt: new Date("2026-01-28"),
		updatedAt: new Date(),
	};

	// Convert to PublicUser (only allowed properties from PublicUser)
	const publicUser: PublicUser = {
		id: dbUser.id,
		username: dbUser.username,
		email: dbUser.email,
		createdAt: dbUser.createdAt,
	};

	return publicUser;
}

// If you accidentally try to include an omitted property,
// TypeScript will flag it as an error:
const invalidPublicUser: PublicUser = {
	id: "123",
	username: "predragmilanovic",
	email: "predrag@example.com",
	createdAt: new Date("2026-01-28"),
	// TypeScript error:
	// Object literal may only specify known properties,
	// and 'passwordHash' does not exist in type 'PublicUser'.
	passwordHash: "${2a$12$...}",
};
```

Because `PublicUser` is built with `Omit`, it **cannot** have the `passwordHash` or `updatedAt` properties from `DatabaseUser`. Trying to include them produces a type error, which helps prevent accidentally leaking sensitive information.

Use `Omit` when you want to:

- expose a “safe” version of a type without internal or sensitive fields
- remove fields not needed in a specific context (e.g., UI view models)
- derive input or response DTOs from a richer domain model while sharing the same base shape

