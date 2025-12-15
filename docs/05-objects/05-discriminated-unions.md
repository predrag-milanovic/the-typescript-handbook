## Discriminated Unions

A union of two primitive types, like `string | number`, is straightforward: it's a string or a number. The same is true of object types, but it can be tricky to know which shape you're dealing with at runtime. That's where discriminant properties (or "tags") help. A discriminant is a property whose value uniquely identifies the variant, making it easy to write conditional logic. Importantly, the discriminant can only be one specific value in each variant.

Unions of objects with a discriminant property are called [discriminated unions](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes-func.html#discriminated-unions) (or tagged unions).

```ts
type MultipleChoiceLesson = {
	kind: "multiple-choice"; // Discriminant property
	question: string;
	studentAnswer: string;
	correctAnswer: string;
};

type CodingLesson = {
	kind: "coding"; // Discriminant property
	studentCode: string;
	solutionCode: string;
};

type Lesson = MultipleChoiceLesson | CodingLesson;

function isCorrect(lesson: Lesson): boolean {
	switch (lesson.kind) {
		case "multiple-choice":
			return lesson.studentAnswer === lesson.correctAnswer;
		case "coding":
			return lesson.studentCode === lesson.solutionCode;
	}
}
```

Discriminated unions shine when you add new variants, because TypeScript helps ensure you handle all cases. For example, if we introduce another lesson type:

```ts
type TrueFalseLesson = {
	kind: "true-false"; // Discriminant property
	question: string;
	studentAnswer: boolean;
	correctAnswer: boolean;
};

type Lesson = MultipleChoiceLesson | CodingLesson | TrueFalseLesson;
```

TypeScript will now complain: "Function lacks ending return statement and return type does not include 'undefined'", nudging you to handle the new case.

```ts
function isCorrect(lesson: Lesson): boolean {
	switch (lesson.kind) {
		case "multiple-choice":
			return lesson.studentAnswer === lesson.correctAnswer;
		case "coding":
			return lesson.studentCode === lesson.solutionCode;
		case "true-false":
			return lesson.studentAnswer === lesson.correctAnswer;
	}
}
```

Do you have to use `kind` as the tag? Not technically. Should you use `kind`? Yes—it's the common convention and keeps code consistent.
