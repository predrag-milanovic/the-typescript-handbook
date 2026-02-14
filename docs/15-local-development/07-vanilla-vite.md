Vanilla Vite
============

So far we’ve built a small TypeScript script and compiled it manually with the TypeScript compiler (`tsc`). Now let’s scrap that setup and see what it looks like to scaffold a front‑end project using Vite instead.

These days it’s uncommon to build a front‑end application without some kind of build tool. You certainly *can* — we just did — but in real projects you’ll almost always reach for a tool, especially since most front‑end frameworks (React, Vue, Svelte, and others) ship with their own build setups.

What Is Vite?
-------------

[Vite](https://vite.dev/) is a relatively new build tool that focuses on speed and simplicity. It works great for framework projects, but it’s also a solid choice for “vanilla” TypeScript apps.

Vite gives you a few important pieces out of the box:

- **Fast tooling** – Vite uses [`esbuild`](https://esbuild.github.io/) (a super‑fast bundler written in Go) for much of the heavy lifting during development, which is a big part of why it feels so snappy. For production builds it uses [Rollup](https://rollupjs.org/) under the hood.
- **Simple configuration** – For a JS/TS tool, Vite’s configuration surface is small and approachable. Compared to older tools like [Webpack](https://webpack.js.org/), it’s usually much easier to get started.
- **Built‑in dev server** – Vite runs a development server for you, serving your files and handling hot module replacement (HMR) so that changes appear in the browser almost instantly.
- **On‑the‑fly compilation** – During development, Vite compiles and transforms your code on demand, so you don’t have to run `tsc` manually every time you make a change.


