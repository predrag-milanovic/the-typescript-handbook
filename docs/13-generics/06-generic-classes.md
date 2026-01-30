# Generic Classes

By now you've seen that you can bolt type parameters onto almost anything in TypeScript: functions, type aliases, interfaces, and more.

Classes are no exception – they can be generic too.

In this section we'll combine a few ideas:

- `InMemoryRepository` is a **generic class**.
- It implements a **generic interface** (`Repository<T>`).
- The type parameter `T` is **constrained** to have an `id` property.

## A Generic Repository Interface

First, a plain generic interface that describes the behavior we want from a repository:

```ts
interface Repository<T> {
	getAll(): T[];
	getById(id: string): T | undefined;
	save(item: T): void;
}
```

- `Repository<T>` doesn't care what `T` is.
- It just says: "Give me some type `T`, and I'll describe how to get and save values of that type."

## A Generic Class With a Constraint

Now let's implement this interface with a class that stores everything in memory:

```ts
class InMemoryRepository<T extends { id: string }>
	implements Repository<T>
{
	private items: T[] = [];

	getAll(): T[] {
		return [...this.items];
	}

	getById(id: string): T | undefined {
		return this.items.find((item) => item.id === id);
	}

	save(item: T): void {
		const index = this.items.findIndex((i) => i.id === item.id);

		if (index >= 0) {
			this.items[index] = item;
		} else {
			this.items.push(item);
		}
	}
}
```

There are a few things to notice here:

- `InMemoryRepository` is a **generic class**: it has a type parameter `<T>`.
- `InMemoryRepository<T>` **implements** `Repository<T>`, so TypeScript makes sure all the methods and their types line up correctly. If we forget a method or change a return type, we'll get a type error.
- The type parameter has a **constraint**: `T extends { id: string }`.
	- Any `Repository<T>` is free to choose whatever `T` is.
	- But this particular implementation needs an `id` so it can store and look things up.

In other words: *any* object type can go into `InMemoryRepository`, as long as it has an `id` property of type `string`. All the implementation logic is shared for all those different possible types.

## Using the Generic Class

Let's use `InMemoryRepository` with a specific type:

```ts
interface Shinigami {
	id: string;
	name: string;
}

const deathNoteRepo = new InMemoryRepository<Shinigami>();

deathNoteRepo.save({ id: "1", name: "Ryuk" });
deathNoteRepo.save({ id: "2", name: "Rem" });

console.log(deathNoteRepo.getAll());
//    ^? Shinigami[]
```

TypeScript keeps track of the type argument you pass in:

- `deathNoteRepo` is inferred as `InMemoryRepository<Shinigami>`.
- `getAll()` returns `Shinigami[]`.
- `getById("1")` returns `Shinigami | undefined`.
- `save` only accepts values of type `Shinigami`.

## Violating the Constraint

If you try to create an `InMemoryRepository` for a type that **doesn't** have an `id` property, TypeScript will complain:

```ts
interface CharacterWithoutId {
	name: string;
}

// Error:
// Type 'CharacterWithoutId' does not satisfy the constraint '{ id: string; }'.
//   Property 'id' is missing in type 'CharacterWithoutId' but required in type '{ id: string; }'.
const characterRepo = new InMemoryRepository<CharacterWithoutId>();
```

This is exactly what we want: the constraint on `T` means you **can't** accidentally create an `InMemoryRepository` for a type that doesn't have the data it needs to function.

## Why Use `implements` With Generics?

In this example, the `implements` keyword is doing important work:

- It guarantees that `InMemoryRepository<T>` can be used anywhere a `Repository<T>` is expected.
- It keeps the implementation and the interface in sync, even as you refactor.
- It scales nicely: you can have multiple implementations (e.g. `SqlRepository<T>`, `ApiRepository<T>`) all implementing the same `Repository<T>` interface with different internals.

Generic classes like this are a great fit whenever you have **shared behavior** that should work the same way for many different types, but still be **fully type-safe**.

