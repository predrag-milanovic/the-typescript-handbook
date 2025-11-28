# Types

I'm going to assume you're already familiar with JavaScript, if you're not, start with my [The JavaScript Handbook](https://github.com/predrag-milanovic/the-javascript-handbook) first.

TypeScript is a [superset](https://www.cuemath.com/algebra/superset/) of JavaScript, meaning that:

* All JavaScript code is valid TypeScript code,
* All TypeScript code is not necessarily valid JavaScript code.

TypeScript was developed internally at Microsoft by C# developers (led by [Anders Hejlsberg](https://en.wikipedia.org/wiki/Anders_Hejlsberg)) who wanted static typing in their JavaScript (C# being a statically typed language). It was released to the public in 2012.

Why should I use TypeScript instead of JavaScript? Well, TypeScript is fantastic because it:

* Catches a ton of bugs and errors at compile time,
* Makes your code more readable and maintainable,
* Makes it easier to refactor and scale your codebase.

In short, it adds static typing to JavaScript.

TypeScript is a language, but the official implementation of TypeScript is the [TypeScript compiler](https://code.visualstudio.com/docs/typescript/typescript-compiling), `tsc`. Its job is simple: take TypeScript code, ensure it's valid, and then compile it into JavaScript code.

TypeScript is not supported natively by most JavaScript engines, so it needs to be compiled into equivalent JavaScript code before it can be run. It's not compiled in the traditional (compiled to binary) sense. Instead, it's compiled to JavaScript. So it's not really compiled for performance reasons, but rather for compatibility reasons.

## Lessons
- [Basic Types](./01-basic-types.md)
- [Type Inference](./02-type-inference.md)
- [Any](./any.md)