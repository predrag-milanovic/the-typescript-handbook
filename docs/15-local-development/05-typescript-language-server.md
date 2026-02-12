## TypeScript Language Server

So far we’ve used `tsc` from the command line to compile TypeScript, but in most projects that’s not how you interact with TypeScript day‑to‑day.

Most of the time, TypeScript is running as a [**language server**](https://code.visualstudio.com/docs/languages/typescript) inside your editor, powering features like:

- Auto-completion and inline suggestions
- Type checking with underlined errors and quick fixes
- Go to definition / find references / rename symbol

This is why people sometimes joke that TypeScript is a “glorified linter” – you might never manually run `tsc`, but you rely on its analysis constantly through your editor.

The important thing to understand is that your **editor tooling** and your **build tooling** are separate things that both use TypeScript, and they can drift out of sync.

For example:

- Your editor might be using TypeScript 4.x and one `tsconfig.json`.
- Your build (Vite, Webpack, `tsc`, etc.) might be using TypeScript 5.x and a different `tsconfig.json`.

If that happens, you can end up in situations where:

- The editor shows no errors, but the build fails.
- The editor reports errors, but the build is totally fine.

You want your **editor** and **build** to agree about:

- The TypeScript version
- Which files are in the project
- The compiler options in `tsconfig.json`

### Which TypeScript Version Is the Editor Using?

Most editors will **prefer the TypeScript version installed in your project**. If you have a `node_modules` folder with `typescript` installed, the language server should use that version.

If your editor can’t find a workspace-local TypeScript, it will fall back to something else, usually one of:

- A globally installed `typescript` on your machine
- A TypeScript version bundled with the editor itself
- A TypeScript version explicitly configured in editor settings (for example: `.vscode/settings.json`, `.zed/settings.json`, etc.)

To avoid confusion:

- **Pin `typescript` in your project** (for example in `package.json`).
- **Open the editor at the project root**, so it can find `node_modules/typescript` and your `tsconfig.json`.
- **Check your editor’s TS version view** (most have a command or status bar item to show which TS it’s using).

Keeping your editor and build on the **same TypeScript version and config** will save you from a lot of “why does CI see an error that I don’t?” style bugs.

### Restarting the TypeScript Server

Language servers are notorious for sometimes getting stuck or out of sync. If you notice that:

- Errors aren’t updating
- Auto-completion stops working
- Go to definition behaves strangely

…then step one is often simply: **restart the TypeScript language server**.

A few examples:

- **VS Code**: `Cmd/Ctrl+Shift+P` → `TypeScript: Restart TS Server`
- **Zed**: `Cmd/Ctrl+Shift+P` → `Restart Language Server`
- **Neovim (built on LSP)**: `:LspRestart`

If something looks wrong in your TypeScript tooling, it’s always worth checking:

1. Am I using the TypeScript version from this project?
2. Is the right `tsconfig.json` being picked up?
3. Have I tried restarting the language server?

Those three checks solve a surprising number of problems.

