Required Utility Type
=====================

Where `Partial<T>` makes all properties of a type optional, the [`Required<T>`](https://www.typescriptlang.org/docs/handbook/utility-types.html#requiredtype) utility type does the **opposite**: it forces all properties of a type to be required, even ones that were originally optional.

Using `Required<T>`
-------------------

Here’s a practical example:

```ts
interface BlogPost {
	title: string;
	content: string;
	tags?: string[];
	publishDate?: Date;
	author?: {
		id: string;
		name?: string;
	};
}

// All top-level properties are now required
type MyRequiredBlogPost = Required<BlogPost>;
```

The `MyRequiredBlogPost` type is equivalent to:

```ts
type MyRequiredBlogPost = {
	title: string;
	content: string;
	tags: string[];
	publishDate: Date;
	author: {
		id: string;
		name?: string;
	};
};
```

Notice that:

- The **top-level** properties `tags`, `publishDate`, and `author` are now required.
- The `name` property inside `author` is still optional, because `Required<T>` only affects the properties directly on `T` itself.

Just like `Partial<T>`, `Required<T>` is **not recursive**. It does a single level of transformation, leaving any nested objects unchanged. Later sections will explore more advanced patterns when you need deeper control over nested structures.

