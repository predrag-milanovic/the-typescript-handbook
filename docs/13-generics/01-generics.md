Generics
========

Generics are one of TypeScript’s most powerful features. They let you write reusable logic that works with **many types** instead of just one, while still preserving precise type information.

For example, a data structure like a queue or stack shouldn’t care *what* kind of values it stores:

- `NumberQueue`
- `StringQueue`
- `UserQueue`
- etc.

Rather than re‑implementing each of these, we can write a single `Queue<T>` that works for any type `T`. When we use it as `Queue<number>` or `Queue<User>`, TypeScript keeps track of that concrete type everywhere we interact with the queue.

Generics are how we reuse behavior **across types** without falling back to `any`.

You’ve already seen many generics in the standard library and earlier chapters:

- `Array<T>` – arrays of `T` (`Array<number>`, `Array<string>`, etc.)
- `Promise<T>` – an async computation that eventually yields a `T`
- Utility types like `Partial<T>`, `Required<T>`, `Readonly<T>`, `Record<K, T>`, `Pick<T, K>`, and `Omit<T, K>`

In all of these, the `<T>` (or `<K, T>`) part is called a **generic type parameter**. `T` is just a variable name for “some type” – we could call it anything – but `T` is a very common convention.

Creating Custom Generic Functions
---------------------------------

Let’s build a simple but realistic example. Imagine some client‑side code that makes lots of `fetch` requests to a backend. We might start with a helper like this:

```ts
async function fetchFromApi(url: string) {
	try {
		const response = await fetch(url);
		if (!response.ok) {
			throw new Error("Network response was not ok");
		}
		return await response.json();
	} catch (error) {
		console.error("Error fetching data:", error);
		return undefined;
	}
}
```

This works, but TypeScript infers the return type as `Promise<any>` (or `Promise<unknown>`), which doesn’t give us much help when we use it.

We can improve this by making the function **generic** over the type of data we expect back:

```ts
async function fetchFromApi<T>(url: string): Promise<T | undefined> {
	try {
		const response = await fetch(url);
		if (!response.ok) {
			throw new Error("Network response was not ok");
		}
		return (await response.json()) as T;
	} catch (error) {
		console.error("Error fetching data:", error);
		return undefined;
	}
}
```

Here:

- `<T>` declares a **type parameter** `T` for the function.
- The return type `Promise<T | undefined>` says “this returns a `T` (or `undefined` if something goes wrong).”

Now, whenever we call `fetchFromApi`, we specify the type we expect to receive:

```ts
type Comment = { id: string; body: string };
type User = { id: string; name: string };
type Post = { id: string; title: string };

const comments = await fetchFromApi<Comment[]>(
	"https://api.example.com/posts/1/comments",
);

const user = await fetchFromApi<User>(
	"https://api.example.com/user/1",
);

const posts = await fetchFromApi<Post[]>(
	"https://api.example.com/posts",
);
```

In each call, `T` is inferred from the explicit type argument:

- `fetchFromApi<Comment[]>` → `T` is `Comment[]`
- `fetchFromApi<User>` → `T` is `User`
- `fetchFromApi<Post[]>` → `T` is `Post[]`

Everywhere we use `comments`, `user`, or `posts`, TypeScript now knows their exact shapes. That’s the core value of generics: **reusable logic plus precise types**, without sacrificing safety or falling back to `any`.

