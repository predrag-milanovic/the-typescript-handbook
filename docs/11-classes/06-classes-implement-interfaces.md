## Classes Implement Interfaces

Classes can implement interfaces using the [`implements` clause](https://www.typescriptlang.org/docs/handbook/2/classes.html#implements-clauses). This lets you say that a class must conform to the structure described by one or more interfaces.

Here are two simple interfaces:

```ts
interface Vehicle {
	make: string;
	model: string;
}

interface Drivable {
	drive(distance: number): void;
}
```

Now suppose we start with a class that has some of the required members:

```ts
class ElectricCar {
	make: string;
	model: string;
}
```

If we say that `ElectricCar` implements both `Vehicle` and `Drivable`, TypeScript will check that the class actually has all the properties and methods from those interfaces:

```ts
// Error: Class 'ElectricCar' incorrectly implements interface 'Drivable'.
class ElectricCar implements Vehicle, Drivable {
	make: string;
	model: string;
}
```

The error happens because `ElectricCar` does not yet have a `drive` method. Once we add it, the class correctly implements both interfaces:

```ts
class ElectricCar implements Vehicle, Drivable {
	make: string;
	model: string;

	// not required by the interfaces, but it's
	// fine to add extra properties
	private isRunning: boolean = false;

	constructor(make: string, model: string) {
		this.make = make;
		this.model = model;
		this.isRunning = false;
	}

	drive(distance: number): void {
		this.isRunning = true;
		console.log(`Driving ${distance} miles`);
	}
}
```

Implementing an interface does **not** prevent you from adding additional fields or methods; it only enforces that the required members exist and have compatible types.

Because `ElectricCar` implements both `Vehicle` and `Drivable`, you can use an instance anywhere either of those types is expected:

```ts
const myCar = new ElectricCar("Tesla", "Model S");

function testDrive(vehicle: Vehicle) {
	console.log(`Testing ${vehicle.make} ${vehicle.model}`);
}

testDrive(myCar); // "Testing Tesla Model S"

function takeForARide(drivable: Drivable) {
	drivable.drive(10);
}

takeForARide(myCar); // "Driving 10 miles"
```

This is a common pattern when you want classes to be interchangeable based on the behavior (interfaces) they support, instead of their specific implementation.

