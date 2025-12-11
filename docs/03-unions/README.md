# Unions and Literal Types

This section covers TypeScript's union types and literal types — powerful features for creating flexible yet type-safe APIs. Learn how to combine types, constrain values, and leverage advanced patterns like template literal types.

## Overview

Union types allow values to be one of several types, while literal types restrict values to specific constants. Together, they enable precise type definitions that catch errors at compile time while maintaining code flexibility.

## Topics Covered

### [01. Unions](./01-unions.md)

Introduction to union types using the pipe (`|`) operator to allow multiple type possibilities. Covers type narrowing with `typeof` checks to safely work with different types in the same variable.

**Key Concepts:**
- Union syntax: `string | number`
- Type narrowing with `typeof`
- Safely handling multiple types

### [02. Optional Parameters](./02-optional-parameters.md)

Function parameters marked with `?` that can be omitted by callers, receiving `undefined` when not provided. Essential for creating flexible function signatures.

**Key Concepts:**
- Optional parameter syntax: `param?`
- Must follow required parameters
- Equivalent to `param: Type | undefined`

### [03. Default Parameters](./03-default-parameters.md)

Provide fallback values for function parameters when callers don't supply them. TypeScript automatically infers types from default values.

**Key Concepts:**
- Default value syntax: `param = defaultValue`
- Automatic type inference
- No need for `?` when defaults are provided

### [04. Literal Types](./04-literal-types.md)

Constrain variables to specific literal values instead of broad types. Use exact strings, numbers, or booleans as types for maximum precision.

**Key Concepts:**
- String literals: `"north"`
- Numeric literals: `42`
- Boolean literals: `true`
- `const` declarations create literal types

### [05. Value Unions](./05-value-unions.md)

Combine literal types with unions to create APIs accepting only specific values. Use type aliases for reusability and self-documenting code.

**Key Concepts:**
- Combining literals: `"north" | "south" | "east" | "west"`
- Type aliases for value sets
- Autocomplete and compile-time validation
- Real-world patterns: status values, HTTP methods

### [06. Template Literal Types](./06-template-literal-types.md)

Generate unions of string types programmatically using template literal syntax. Automatically expand combinations and enforce string patterns.

**Key Concepts:**
- Template syntax: `` `prefix ${Union}` ``
- Cartesian products of multiple unions
- Pattern matching with primitives
- Event names, CSS properties, API endpoints

### [07. Giant Unions](./07-guant-unions.md)

Understand the limitations of complex union types. Learn when unions become impractical and how to use alternative approaches.

**Key Concepts:**
- Combinatorial explosion in template literals
- "Union type too complex" errors
- Performance considerations
- Practical alternatives: runtime validation, builder patterns, branded types
