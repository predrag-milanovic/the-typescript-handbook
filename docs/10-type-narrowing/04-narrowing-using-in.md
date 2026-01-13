# Narrowing Using In

The [`in`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/in) operator checks if a property exists in an object, which is fantastic for type narrowing in object literals.

```typescript
type TextMessage = {
  content: string;
  sentAt: Date;
};

type ImageMessage = {
  caption: string;
  sentAt: Date;
};

type VideoMessage = {
  duration: number;
  sentAt: Date;
};

type Message = TextMessage | ImageMessage | VideoMessage;

function displayMessage(message: Message) {
  if ("content" in message) {
    // TypeScript knows this is a TextMessage
    // because it's the only one with a 'content' property
    console.log(`Text content is: ${message.content}`);
  } else if ("caption" in message) {
    // TypeScript knows this is an ImageMessage
    // because it's the only one with an 'caption' property
    console.log(`Image caption is ${message.caption}`);
  } else {
    // TypeScript knows this is a VideoMessage because
    // it's the only other option
    console.log(`Video length is ${message.duration}`);
  }
}
```

## Discriminated Unions vs. 'in' Checks

You might have noticed that this kind of logic feels very similar to using discriminated unions, and you're correct. Here's the same types with an explicit discriminant property:

```typescript
type TextMessage = {
  kind: "text";
  content: string;
  sentAt: Date;
};

type ImageMessage = {
  kind: "image";
  caption: string;
  sentAt: Date;
};

type VideoMessage = {
  kind: "video";
  duration: number;
  sentAt: Date;
};
```

My recommendation is to prefer a discriminated union when you have full control of the types, but if you're using types from a library or package, or have another reason you don't want extra properties, the `in` operator is a great alternative.
