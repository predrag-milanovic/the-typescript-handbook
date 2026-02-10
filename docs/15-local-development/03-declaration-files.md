# Declaration Files

If you've ever seen funky-looking `.d.ts` files and wondered what they are, they're declaration files. A declaration file only contains type information – no runtime code is allowed. They're extremely useful for describing the types of JavaScript code that exists in your app but doesn't ship with its own types.

TypeScript uses these files to understand the shape of values at compile time. At runtime, declaration files are completely erased.

## Why declaration files exist

Declaration files are most commonly used to:

- Add types for plain JavaScript libraries (especially ones loaded from a CDN).
- Describe globals that are provided by some script but not declared anywhere in your TypeScript source.
- Share type information across a project without bundling any extra JavaScript.

They let you keep the convenience of existing JavaScript libraries while still enjoying TypeScript's static checking and editor tooling.

## Example: typing a global `google` object

For example, at Boot.dev we support login with Google. The codebase is written in TypeScript, but we include Google's JavaScript library in our HTML as per their documentation.

Because we want static type hints in our editors, we add a `globals.d.ts` file to our project that describes the global `google` object on `window`:

```ts
declare global {
	interface Window {
		google: Google;
	}
}

interface Google {
	accounts: {
		id: {
			renderButton: (
				element: HTMLElement,
				options: {
					type?: string;
					theme?: string;
					size?: string;
					text?: string;
					shape?: string;
					width?: number;
				},
			) => void;
			prompt: () => void;
			cancel: () => void;
			initialize: (options: { client_id: string; callback: () => void }) => void;
			disableAutoSelect: () => void;
			revoke: (clientId: string, callback: () => void) => void;
		};
	};
}

export {};
```

This declaration file effectively says:

> "There's a global variable called `google` on the `window` object, and it has this shape."

Now when we use `window.google` in our TypeScript code, the compiler and our editor know exactly what properties and methods exist, and can provide autocomplete, type-checking, and inline documentation. The declaration file doesn't change how the code runs at all, but it makes our lives much easier when writing and maintaining the code.

