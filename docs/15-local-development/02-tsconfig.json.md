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

