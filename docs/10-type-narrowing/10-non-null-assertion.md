# Non-Null Assertion

It's common for TypeScript libraries to assume that a value can be `null` or `undefined` even when you know it can't be. You can assert that it's not with the **non-null assertion** ([`!`](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-0.html#non-null-assertion-operator)) operator. It tells the compiler that a value cannot be `null` or `undefined`, even when the type system thinks it might be.

```ts
// assume getCleanedText returns a string | null
import { getCleanedText, sendText } from "./text-utils";

const cleanedText = getCleanedText("some text");
// cleanedText is string | null
// but we know that it's not null because we passed in a valid string

// sendText expects a string, so we use a non-null assertion
sendText(cleanedText!);
```

You'll also see this fairly often when working with optional properties that you know exist:

```ts
interface User {
  id: string;
  name?: {
    first: string;
    last: string;
  };
}

// we don't control the User type (it's imported from a library)
// but we know that we always use the `name` property
sendText(user.name!.first);
```

The same rules-of-thumb as type assertions apply here. Only use non-null assertions when you're **absolutely confident** that the value can't be `null` or `undefined`. Just use a conditional guard clause if there is any uncertainty. This is always safer, albeit more verbose:

```ts
function sendTextSafely(text: string | null) {
  if (text === null) {
    throw new Error("Text is required");
  }
  sendText(text);
}
```
