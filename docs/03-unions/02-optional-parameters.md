# Optional Parameters

Function parameters can be marked optional with a question mark (`?`) after the parameter name. When a caller omits an optional parameter, it receives the value `undefined`.

## Basic Example

```ts
function greet(name: string, title?: string): string {
  if (title) {
    return `Hello, ${title} ${name}!`;
  }
  return `Hello, ${name}!`;
}

greet("Gandalf");           // "Hello, Gandalf!"
greet("Gandalf", "Wizard"); // "Hello, Wizard Gandalf!"
```

## Key Rules

**1. Optional parameters must come after required parameters.**

This won't compile:

```ts
// Error: Required parameter cannot follow optional parameter
function greet(title?: string, name: string): string {
  // ...
}
```

**2. Optional parameters have `undefined` automatically unioned with their type.**

Inside the function, an optional parameter has type `Type | undefined`:

```ts
function greet(name: string, title?: string): string {
  // Inside the function, title has type: string | undefined
  
  if (title) {
    // Here, title is narrowed to string
    return `Hello, ${title} ${name}!`;
  }
  // Here, title is narrowed to undefined
  return `Hello, ${name}!`;
}
```

## Optional vs Default Parameters

Optional parameters default to `undefined`, but you can provide an explicit default value:

```ts
// Optional: defaults to undefined
function logMessage(msg: string, level?: string) {
  console.log(`[${level || "INFO"}] ${msg}`);
}

// Default value: defaults to "INFO"
function logMessageWithDefault(msg: string, level: string = "INFO") {
  console.log(`[${level}] ${msg}`);
}

logMessage("Error occurred");           // "[INFO] Error occurred"
logMessageWithDefault("Error occurred"); // "[INFO] Error occurred"
```

## Type Narrowing with Optional Parameters

Always check for `undefined` before using an optional parameter:

```ts
function formatDate(date: Date, format?: string): string {
  if (format === undefined) {
    return date.toDateString();
  }
  // Safe to use format here — it's narrowed to string
  return date.toLocaleString("en-US", { dateStyle: format });
}
```

## Key Takeaway

Use `?` for optional parameters; they automatically union with `undefined`. Always place optional parameters after required ones, and use type narrowing to safely access them.
