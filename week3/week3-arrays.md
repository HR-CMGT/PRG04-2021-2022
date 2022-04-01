# Arrays

Als je een groot aantal `instances` nodig hebt, is het niet handig om voor elke `instance` een property aan te maken:

```typescript
import { Bunny } from "./Bunny"

export class Game {

    private bunnyOne: Bunny
    private bunnyTwo: Bunny
    private bunnyThree: Bunny

    constructor() {
        this.bunnyOne = new Bunny(this)
        this.bunnyTwo = new Bunny(this)
        this.bunnyThree = new Bunny(this)
    }

    private update(delta) {
        this.bunnyOne.update(delta)
        this.bunnyTwo.update(delta)
        this.bunnyThree.update(delta)
    }
}
```
<br>
<br>
<br>

## For loop en array

We kunnen ook een enkele property aanmaken waarin alle Bunnies komen te staan. Dit is dan een array van het type `Bunny`. Let op dat je ook meteen een lege array aanmaakt.

Met een `for` loop kunnen we hier meerdere bunnies in zettten.

```typescript
import { Bunny } from "./Bunny"

export class Game {

    private bunnies: Bunny[] = []

    constructor() {
        for(let i = 0; i<10; i++){
            this.bunnies.push(new Bunny(this))
        }
    }
}
```
<br>
<br>
<br>

## Animatie

We kunnen door de array heen loopen met een `for of` loop, en dan van elke `instance` de `update()` functie aanroepen.

```typescript
class Game {
    private update(delta) {
        for(let bunny of this.bunnies){
            bunny.update(delta)
        }
    }
}
```

<Br>
<br>
<br>

# Opdracht

![fishes](../week1/opdracht.jpg)

- Plaats de Fishes en Bubbles in een array in de Game class
- Geef de `Fish` en `Bubble` classes een `update` functie om te animeren (zie het voorbeeld van de Bunny class).
- Gebruik een `for of` loop om de `update` functie van de vissen en bubbles aan te roepen. 

<Br>
<br>
<br>

# Opdracht

Maak de `Fishes` [clickable met de voorbeelcode van PixiJS](https://pixijs.io/examples/#/interaction/click.js). 

Als je op een Fish klikt, verander je het plaatje in een skelet! Maak de `onClick` functie waarin de sprite verandert.

🤔 Plaats onderstaande code snippets op de juiste plek in de `Fish` class:

```javascript
// skelet plaatje
import { skeletonImage } from "./images/bones.png"

// sprite interactief maken
this.sprite.interactive = true
this.sprite.buttonMode = true
this.sprite.on('pointerdown', () => this.onClick())

// de class krijgt een onclick functie
onClick() {
    this.sprite = PIXI.Sprite.from(skeletonImage)
}
```

