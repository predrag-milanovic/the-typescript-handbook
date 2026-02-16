TypeScript Handbook
===================

This handbook is a practical, example‑driven guide to TypeScript.
It focuses on the language itself – the type system and core patterns –
so you can write safer, more maintainable JavaScript.

You should already be comfortable with JavaScript or another programming
language. The chapters move quickly and assume you know programming
fundamentals like variables, functions, and objects.

How to use this handbook
------------------------

- **Read in order** if you’re new to TypeScript – each chapter builds on
	the previous ones.
- **Dip into specific topics** if you already use TypeScript and want to
	sharpen one area (e.g. unions, generics, or utility types).
- **Follow the examples** – they are intentionally small, so you can copy
	and adapt them into your own codebase.

This README only gives a high‑level tour. The real content lives in the
chapter files listed below.

Chapter overview
----------------

### 01. Types

Foundations of the TypeScript type system: primitive types, basic
annotations, type inference, and the escape hatch of `any`. This chapter
gives you the vocabulary to describe the shapes of your values.

### 02. Functions

How to type functions: parameter and return types, `void`, function type
signatures, type aliases for reusable function shapes, and importing
types. You’ll learn to treat functions as first‑class, typed values.

### 03. Unions

Working with values that can be more than one type. Covers union types,
optional and default parameters, literal types, value unions, template
literal types, and large “enum‑like” unions.

### 04. Arrays

Typed arrays and lists of values. You’ll see how to describe arrays with
type parameters, work with heterogeneous arrays, use rest parameters,
and avoid accidentally “evolving” `any`.

### 05. Objects

Typing object literals and real‑world data structures: extra and optional
properties, discriminated unions, `Set` and `Map`, dynamic keys and
default properties, `PropertyKey`, `readonly`, `as const`, `satisfies`,
and function overloads.

### 06. Tuples

Fixed‑length, ordered collections of values. This chapter covers tuples
vs. objects, readonly tuples, destructuring, named tuples, optional
elements, and tuple rest elements.

### 07. Intersections

Combining types with intersections to build richer shapes, understanding
`never`, and what happens when you intersect incompatible types. You’ll
see how intersections compare to unions and how they interact.

### 08. Interfaces

Describing object contracts with interfaces. You’ll learn about
defining interfaces, extending them, extending multiple interfaces,
overriding properties, and how declaration merging works in TypeScript.

### 09. Enums

Enumerated values in TypeScript: numeric and string enums, how enums
compile to JavaScript, `const enum` and when to use it, and how enums
compare to union types.

### 10. Type Narrowing

Making union types more specific based on runtime checks. This includes
`typeof` and `in` checks, the `unknown` type and the type hierarchy,
user‑defined type predicates, exhaustive checks, and guard clauses.

### 11. Classes

Object‑oriented patterns in TypeScript. Covers defining classes,
constructors, fields, access modifiers, `readonly`, inheritance,
implementing interfaces, and how TypeScript’s type system models class
instances and statics.

### 12. Utility Types

Built‑in helpers for transforming types: picking and omitting
properties, making properties optional or required, mapping keys to
values, and other common patterns you’ll use when shaping API types.

### 13. Generics

Type parameters for reusable, type‑safe functions, classes, and
interfaces. You’ll see how to define generics, add constraints, use
defaults, and understand where generics improve both safety and
ergonomics.

### 14. Conditional Types

Types that depend on other types. This chapter introduces conditional
types, distributive behavior over unions, and using `infer` to extract
parts of complex types.

### 15. Local Development

Practical guidance for running TypeScript in real projects: installing
TypeScript, configuring `tsconfig.json`, working with declaration files
and JavaScript libraries, editor integration, ignore directives, and
integrating TypeScript into a modern build tool like Vite.

Further reading
---------------

For the full, official TypeScript documentation and language reference,
visit the [TypeScript docs](https://www.typescriptlang.org/docs/).
