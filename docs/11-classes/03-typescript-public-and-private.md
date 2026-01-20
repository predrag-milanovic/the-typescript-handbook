# TypeScript Public and Private

JavaScript's `#` private fields didn't come until ES2022, but TypeScript developers had wanted public/private/protected access modifiers for a long time, so TypeScript added support for `private` and `protected` before then. As a result, a lot of older TypeScript code uses the keyword syntax.

## Using the `private` Keyword

To create private members the TypeScript-only way, you use the `private` keyword:

```typescript
class SecretAgent {
  // private field using the private keyword
  private id: string;

  constructor(id: string) {
    this.id = id;
  }

  // a public method
  getCodeName(): string {
    const idToCodeNameMap: Record<string, string> = {
      "007": "James Bond",
      "006": "Alec Trevelyan",
      // Add more mappings as needed
    };
    return idToCodeNameMap[this.id] || "Unknown Agent";
  }
}

const bond = new SecretAgent("007");
console.log(bond.getCodeName()); // "James Bond"

// Property 'id' is private and only accessible within class 'SecretAgent'
console.log(bond.id); // This will cause a compilation error
```

## Which Syntax Should I Use?

The only reason TypeScript-specific syntax exists is because JavaScript didn't have the `#` syntax until ES2022. I recommend using the JavaScript `#` syntax because it's the JavaScript native way to do it. Remember, TypeScript is basically just tools for writing type-safe JavaScript, so conforming to JavaScript standards is the long-term play.

I only recommend using the TypeScript-specific syntax if you need to target an older version of JavaScript that doesn't support the `#` syntax yet.
