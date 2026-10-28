## CMPM121-S04

Group members: Aimee, Charlotte, and Sharon

1: Duplicated Code



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
