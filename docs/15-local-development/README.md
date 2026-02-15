Local Development
=================

In projects, you’ll run TypeScript directly on your machine, wire it into a build tool, and rely on your editor’s integration to give you fast feedback.

This section walks through the practical pieces you need to be productive with TypeScript in a real codebase.

What you’ll learn
------------------

- **[Install TypeScript](./01-install-typescript.md)** – How to install the TypeScript compiler on your machine, verify the `tsc` command works, and understand where npm puts global binaries.
- **[tsconfig.json](./02-tsconfig.json.md)** – How to configure the TypeScript compiler, choose `lib` and `target` settings, and enable high‑value options like `strict`, `skipLibCheck`, and `verbatimModuleSyntax`.
- **[Declaration Files](./03-declaration-files.md)** – How `.d.ts` files describe the shape of values without shipping any runtime code, and how to use them to type globals and other JavaScript that doesn’t have built‑in types.
- **[Using JavaScript Libraries](./04-using-js-libraries.md)** – Strategies for working with untyped JavaScript packages, from reaching for `@types` on DefinitelyTyped to writing your own declaration files for external and internal modules.
- **[TypeScript Language Server](./05-typescript-language-server.md)** – How your editor uses TypeScript under the hood, how it can drift from your build configuration, and how to make sure both use the same TypeScript version and `tsconfig.json`.
- **[TypeScript Ignore Directives](./06-typescript-ignore.md)** – The escape hatches (`@ts-ignore`, `@ts-nocheck`) that suppress type errors, when they might be necessary, and why they should be treated as technical debt.
- **[Vanilla Vite](./07-vanilla-vite.md)** – How to move from manually running `tsc` to using Vite as a fast, modern build tool for a vanilla TypeScript front‑end project.

Quick setup checklist
---------------------

If you’re starting a new TypeScript project on your machine, a sensible sequence is:

1. **Install Node.js and npm**, then **install TypeScript** so the `tsc` command is available (see *Install TypeScript*).
2. **Create a `tsconfig.json`** with reasonable defaults for your environment – start with modern `lib` and `target` values, then enable stricter options as you’re comfortable (see *tsconfig.json*).
3. **Open the project in your editor** and make sure the **language server is using the workspace TypeScript version** from `node_modules`, not some global or bundled version (see *TypeScript Language Server*).
4. **Decide on a build tool**. For front‑end work, scaffolding a project with Vite is a great default (see *Vanilla Vite*). For smaller scripts, running `tsc` directly might be enough.
5. **Add types for JavaScript libraries** you depend on – prefer `@types` packages from DefinitelyTyped, and fall back to writing your own `.d.ts` files when necessary (see *Declaration Files* and *Using JavaScript Libraries*).
6. **Avoid turning off the type checker**. Reach for `@ts-ignore` or `@ts-nocheck` only as a last resort, with comments explaining why they’re there and a plan to remove them later (see *TypeScript Ignore Directives*).

