# "As Const" and Object.freeze

The [`as const` assertion](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#literal-inference) creates a deeply readonly type using literal values.

```ts
const priorities = ["low", "medium", "high"] as const;

// Error: Property 'push' does not exist on type 'readonly ["low", "medium", "high"]'
priorities.push("urgent");
```

It also works with objects and makes every nested property readonly automatically.

```ts
const configConst = {
	baseUrl: "https://api.library.io",
	featureFlags: {
		search: true,
		sync: false,
	},
	timeouts: [200, 500, 1000],
} as const;

// Error: Cannot assign to 'baseUrl' because it is a read-only property
configConst.baseUrl = "https://api.alt.io";

// Error: Cannot assign to 'search' because it is a read-only property
configConst.featureFlags.search = false;

// Error: Property 'push' does not exist on type 'readonly [200, 500, 1000]'
configConst.timeouts.push(1500);
```

## Object.freeze()

[`Object.freeze()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze) is a runtime helper that prevents top-level mutations of an object. TypeScript infers those top-level properties as readonly, but nested objects and arrays stay mutable unless you freeze them too.

```ts
const frozenProfile = Object.freeze({
	username: "neo",
	stats: {
		level: 5,
		xp: 8000,
	},
	badges: ["operator", "architect"],
});

// Error (type-level): Cannot assign to 'username' because it is a read-only property
frozenProfile.username = "trinity";

// OK: nested properties are not frozen automatically
frozenProfile.stats.level = 6;

// OK: the array itself is still mutable
frozenProfile.badges.push("sentinel");
```

Because `Object.freeze()` runs at runtime, attempts to change top-level properties will also fail at runtime (silent in [non-strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode), `TypeError` in strict mode). For deep immutability, combine `as const` or additional freezes on nested values.
