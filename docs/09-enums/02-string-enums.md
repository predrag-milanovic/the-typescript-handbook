# String Enums

Numeric enums can be nice when:

- You actually want numbers
- You really want to eke out every last bit of performance (numbers use less memory than strings)

But often, string enums are easier to work with if you just want labels.

```typescript
enum LogLevel {
  ERROR = "ERROR",
  WARN = "WARN",
  INFO = "INFO",
  DEBUG = "DEBUG",
}

function structuredLog(message: string, level: LogLevel) {
  console.log(`[${level}] ${message}`);
}

structuredLog("User not found", LogLevel.ERROR);
// Outputs: [ERROR] User not found
```

## When to use string enums

When enums only exist within your code, numeric enums are totally fine. They start to get really hairy when you need to serialize them to JSON or store them in a database. There's nothing worse than debugging API responses and seeing this:

```json
{
  "id": "94e83b65-ae9c-47f4-b788-d3f4fd085067",
  "name": "Lane",
  "user_type": 7
}
```

What the heck is `7`?! String enums make your data much more readable and maintainable.
