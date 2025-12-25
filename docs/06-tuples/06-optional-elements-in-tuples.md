# Optional Elements in Tuples

Like object properties, tuple elements can be optional using the `?` modifier. This helps model values that may or may not be present while keeping the tuple’s fixed shape.

```ts
type HttpResponse = [statusCode: number, data: string, error?: string];

// Both of these work!
const successResponse: HttpResponse = [200, "Success!"];
const errorResponse: HttpResponse = [404, "", "Resource not found"];
```

## Optional Values Are Last

Just like optional function parameters, all required elements must come before optional elements.

```ts
// Invalid: required after optional
type BadResponse = [statusCode: number, data?: string, error: string];

// Valid: optional elements trail
type GoodResponse = [statusCode: number, data?: string, error?: string];
```

## Optional Types Include `undefined`

Optional elements are automatically unioned with `undefined`.

```ts
type UserInfo = [name: string, age: number, address?: string];

function handleUserInfo(user: UserInfo) {
  const [name, age, address] = user;
  // name: string
  // age: number
  // address: string | undefined
}
```

### Tips
- Keep optional elements at the end to avoid confusing access patterns.
- Destructure carefully; optional positions may be `undefined`.
- Prefer object types when you have many optional properties; objects are easier to extend and validate.
