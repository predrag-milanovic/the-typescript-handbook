# Narrowing Types

[Type narrowing](https://www.typescriptlang.org/docs/handbook/2/narrowing.html) is the simple process of making a type more and more specific as you write your code. As a general rule (don't abuse it, for the love...) the more specific your types, the better. With narrower types:

- Your editor tooling will be more helpful
- Your code will self-document much better
- You'll catch more errors at compile time.

## Conditional Narrowing

One of the coolest features of TypeScript is how smart it is about recognizing how types are being narrowed in "regular" code. For example:

```typescript
type WitcherCharacter = {
  type: "witcher";
  name: string;
  magicPower: boolean;
};

type StarWarsCharacter = {
  type: "star-wars";
  name: string;
  forceSensitive: boolean;
};

type Character = WitcherCharacter | StarWarsCharacter;

function fight(player1: Character, player2: Character) {
  if (player1.type === "witcher" && player2.type === "witcher") {
    // I don't need to type cast (convert)
    // player1 and player2 to WitcherCharacter - TypeScript
    // does that automatically because this branch of the
    // conditional narrows the type
    fightWitcher(player1, player2);
  } else if (player1.type === "star-wars" && player2.type === "star-wars") {
    // same thing here
    fightStarWars(player1, player2);
  } else {
    throw new Error("Can't fight characters from different universes");
  }
}

function fightWitcher(player1: WitcherCharacter, player2: WitcherCharacter) {
  // witcher specific logic
}

function fightStarWars(player1: StarWarsCharacter, player2: StarWarsCharacter) {
  // star wars specific logic
}
```
