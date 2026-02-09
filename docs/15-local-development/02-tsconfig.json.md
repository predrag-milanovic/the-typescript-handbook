tsconfig.json
==============

The [`tsconfig.json`](https://www.typescriptlang.org/tsconfig/) file configures how the TypeScript compiler behaves. It controls what JavaScript gets emitted, which libraries are available, and what kinds of errors the compiler will report.

Because there are so many configuration options, it is rarely accurate to say that "TypeScript will always error on X". In practice, whether something is an error or not often depends on how your `tsconfig.json` is set up.

A simple tsconfig.json
----------------------

Here is a minimal example that is reasonable for a brand‑new project:

```json
{
	"compilerOptions": {
		"lib": ["esnext"],
		"target": "esnext"
	}
}
```

This configuration sets two important options under `compilerOptions`:

- `lib` specifies which JavaScript library definitions are included during compilation. This determines which built‑in APIs (such as `Promise`, `Map`, or `Array.prototype.find`) TypeScript knows about and can type‑check.
- `target` specifies which ECMAScript version TypeScript should emit. This affects the shape of the JavaScript that gets written to disk.

Using `"esnext"` for both `lib` and `target` is convenient when you are starting a new project and want to write against the latest JavaScript features. However, before you ship a 1.0 release, it is a good idea to pin these to a specific version that matches the runtime environments you intend to support. For example:

```json
{
	"compilerOptions": {
		"lib": ["es2024"],
		"target": "es2024"
	}
}
```

Locking your configuration to a specific ECMAScript year makes your build more predictable and avoids surprises if the meaning of `"esnext"` changes as the language evolves.

More tsconfig.json options
--------------------------

The full list of `tsconfig.json` options is quite large, so you will usually refer to the official documentation when you need something specific. That said, there are a few high‑value `compilerOptions` that are worth understanding early on.

Here is a sketch of what a more fleshed‑out configuration might look like:

```json
{
	"compilerOptions": {
		"lib": ["es2024", "dom", "dom.iterable"],
		"target": "es2024",
		"strict": true,
		"skipLibCheck": true,
		"verbatimModuleSyntax": true,
		"esModuleInterop": true,
		"moduleDetection": "force",
		"noUncheckedIndexedAccess": true
	}
}
```

Some of the most common and useful options are:

- [`lib`](https://www.typescriptlang.org/tsconfig/#lib): Adds built‑in library definitions. If you are writing browser code, include `"dom"` and `"dom.iterable"` (note the lowercase) so that TypeScript knows about the DOM APIs like `document`, `window`, and friends.
- [`strict`](https://www.typescriptlang.org/tsconfig/#strict): When `true`, enables all strict type‑checking options. This catches many bugs at compile time. It is strongly recommended for new codebases, though you may temporarily disable it when migrating a large existing JavaScript project.
- [`skipLibCheck`](https://www.typescriptlang.org/tsconfig/#skipLibCheck): When `true`, TypeScript skips type‑checking `.d.ts` declaration files (for example, everything in `node_modules`). This can drastically reduce compile times without meaningfully affecting type safety for most projects.
- [`verbatimModuleSyntax`](https://www.typescriptlang.org/tsconfig/#verbatimModuleSyntax): When `true`, TypeScript preserves your import and export syntax more literally and requires that type‑only imports and exports use the `import type` / `export type` form. This removes some of the historical quirks around how imports are transformed and makes it clearer which imports exist only at type‑checking time.
- [`esModuleInterop`](https://www.typescriptlang.org/tsconfig/#esModuleInterop): When `true`, makes it easier to interoperate with CommonJS modules by allowing default‑style imports (`import fs from "fs"`) from modules that were originally written for `require`. This is especially handy when working with Node‑style packages.
- [`moduleDetection`](https://www.typescriptlang.org/tsconfig/#moduleDetection): When set to `"force"`, treats every file as a module, even if it does not explicitly use `import` or `export`. This avoids some legacy script‑mode behavior and is generally what you want for modern TypeScript projects.
- [`noUncheckedIndexedAccess`](https://www.typescriptlang.org/tsconfig/#noUncheckedIndexedAccess): When `true`, any indexed access like `obj[key]` or `arr[index]` gets `undefined` added to its type. This nudges you to handle missing values explicitly and can prevent subtle runtime errors.

You do not need to memorize all of these at once, but having a mental model of what they do will help you understand example `tsconfig.json` files you encounter in the wild.

