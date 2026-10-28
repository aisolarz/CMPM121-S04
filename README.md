## CMPM121-S04

Group members: Aimee, Charlotte, and Sharon

# 1: Duplicated Code

**What it is/Prevention:**

Duplicated code is when the same or very similar code is repeated in multiple places, often by copying and pasting code. This can make the program harder to understand and increase the chance of errors when changes are needed. To prevent this, you should reuse existing methods instead of rewriting the same logic. Fowler’s Extract Method technique can help by moving repeated code into a separate, reusable method, making the program eimpler/easier to update.

**Refactoring:**

### Code example from CMPM 120 final project

**Before**
```typescript
if (gameSettings.player1Character === 'purple') {
    this.player1 = this.add.sprite(412, -100, 'player1_jetpack1').setScale(0.5)
    this.player1.play('player1Anims');
}

if (gameSettings.player1Character === 'brown') {
    this.player1 = this.add.sprite(412, -100, 'player2_jetpack1').setScale(0.5)
    this.player1.play('player2Anims');
}
                
if (gameSettings.player2Character === 'purple') {
    this.player2 = this.add.sprite(612, -100, 'player1_jetpack1').setScale(0.5)
    this.player2.play('player1Anims');
}
                
if (gameSettings.player2Character === 'brown') {
    this.player2 = this.add.sprite(612, -100, 'player2_jetpack1').setScale(0.5)
    this.player2.play('player2Anims');
}
```

**Whats Wrong**
- Repeated logic: all four conditions create a sprite, set its scale, and play an animation

- Difficult maintenance: if you change the sprite creation logic, you may need to update multiple branches

- More room for errors: You could accidentally update one branch but forget the others 

- Solution: create a method that handles character creation and animation.

**After**
```typescript
createPlayer(x, character){
    const isPurple = character === ‘purple’;
	
    const texture = isPurple ? ‘player1_jetpack1’ : ‘player2_jetpack1’;

	const animation = isPurple ? ‘player1Anims’ : ‘player2_Anims’;

	const player = this.add.sprite(x, -100, texture).setScale(0.5);

	player.play(animation);

	return player;
}

//create player 1
this.player1 = this.createPlayer(412, gameSettings.player1Character);

//create player2
this.player2 = this.createPayer(612, gameSettings.player2Character);

```

**What changed**
- Added one reusable createPlayer() method handles sprite creation and animation

- Player positions stay the same

- Character selection stays the same






# 2: Mysterious Name

**What it is:**
A mysterious name is a variable, function, class, or field whose name doesnt tell you what it holds or does. You usually end up having to read the surrounding code to figure out the meaning

**How it happens:**
- Copy-pasting coe and keeping the old name
- the purpose of the code changes later but the name ends up staying
- short names that made sense when the code was shorter but not once the file grows
- writing quickly to meet a deadline

**Prevention:**
- Name things after what they mean not how they're used or how long they are
- use full words unless the short name is universal
- agree on some naming riles as a team

**Refactoring**

### Code Example 1 Typescript (Demo 1)

**Before**
```typescript
const numCoffeeDisplay = document.createElement("h1");
numCoffeeDisplay.id = "numCoffeeDisplay";
const productionDisplay = document.createElement("p");
const numPerClick = document.createElement("p");
```

```typescript
numPerClick.textContent = `Coffees per click ${Math.floor(cupsPerClick)}`;

**Whats wrong:** 
'numPerClick' sounds like it holds a number, but it is actually an 'HTMLParagraphElement' . The real number is cupsPerClick so a reader could really easily mix them up. It also doesnt match with the other display names in the file like `numCoffeeDisplay`, `productionDisplay`

**After:**

```typescript
const numCoffeeDisplay = document.createElement("h1");
numCoffeeDisplay.id = "numCoffeeDisplay";
const productionDisplay = document.createElement("p");
const perClickDisplay = document.createElement("p");
```

```typescript
perClickDisplay.textContent = `Coffees per click ${Math.floor(cupsPerClick)}`;
```

Refactoring used: [Rename Variable](https://refactoring.com/catalog/renameVariable.html). Now the name ends in `Display`, like the others, so it's clear it's something shown on the page.