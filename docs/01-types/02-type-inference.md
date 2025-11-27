# Type Inference

If you find typing long annotations tedious, good news — TypeScript is excellent at inferring types for you.

Instead of explicitly declaring the type:

```ts
const bootupLog: string = "Starting support.ai servers...";
```

you can rely on inference and write the shorter equivalent:

```ts
const bootupLog = "Starting support.ai servers...";
```

TypeScript is incredible at [type inference](https://www.typescriptlang.org/docs/handbook/type-inference.html). TypeScript infers the type of `bootupLog` as `string`, so the shorter form is just as safe (and less error-prone) than an explicit annotation. Prefer inference for local constants and variables unless you need a specific, broader, or intentionally different type.