## Record Utility Type

[`Record<K, T>`](https://www.typescriptlang.org/docs/handbook/utility-types.html#recordkeys-type) creates an object type with keys of type `K` and values of type `T`.

It is especially useful when you:

- want a dictionary-like object with consistent value types
- need to ensure that **all** members of a union of keys are present
- want TypeScript to prevent extra keys from being added

### Basic dictionary usage

```ts
// Using string as the key type
type StringKeyDictionary = Record<string, number>;

const karateScores: StringKeyDictionary = {
	"Ralph Macchio": 60,
	"William Zabka": 100,
	"Jackie Chan": 82,
};

// We can add any string key
karateScores["Pat Morita"] = 85;

// But values must be numbers
// Type 'string' is not assignable to type 'number'
karateScores["Eve"] = "A+";
```

### Using unions for required keys

One of the most powerful uses of `Record` is with a union of literal types. This ensures that **every key in the union exists** in the object, and that no extra keys are allowed.

```ts
// Using a union of literal types as keys
type PlayerRole = "tank" | "healer" | "dps";
type RoleCapacity = Record<PlayerRole, number>;

const partyRequirements: RoleCapacity = {
	tank: 1,
	healer: 2,
	dps: 3,
};

// TypeScript error if any role is missing
const invalidRequirements: RoleCapacity = {
	tank: 1,
	dps: 3,
	// Property 'healer' is missing in type '{ tank: number; dps: number; }'.
};

// We can't add additional keys not in the union
// Property 'support' does not exist on type 'RoleCapacity'.
partyRequirements["support"] = 1;
```

### Lookup tables and configuration

`Record` shines for exhaustive lookup tables and configuration objects where you want every possible key to be handled.

```ts
type HttpStatusCode = 200 | 201 | 400 | 401 | 403 | 404 | 500;

const statusMessages: Record<HttpStatusCode, string> = {
	200: "OK",
	201: "Created",
	400: "Bad Request",
	401: "Unauthorized",
	403: "Forbidden",
	404: "Not Found",
	500: "Internal Server Error",
};

function getStatusMessage(code: HttpStatusCode): string {
	return statusMessages[code];
}

getStatusMessage(404); // "Not Found"
```

By combining `Record` with unions of keys, you get strongly typed, exhaustive maps that are easy to refactor and hard to misuse.

