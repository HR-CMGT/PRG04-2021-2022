# Week 2 - Fish Class

Je kan de sprite uit het [voorbeeld](https://pixijs.io/examples/#/sprite/basic.js) rechtstreeks in de Game class aanmaken, maar zodra je meer sprites krijgt, die elk ook gedrag en eigenschappen moeten krijgen, dan is het handiger om een aparte class te maken.

<br>
<br>
<br>

## 🐠 Fish

De Fish heeft een *sprite* (de afbeelding), en de *positie* en *rotatie* van die sprite. Daarom maken we van `sprite` een property. Gebruik `this.sprite` om de sprite ook daadwerkelijk aan te maken.

### Properties
```typescript
import { fishImage } from "./images/fish.png"

class Fish {
    sprite:PIXI.Sprite
    constructor(){
        this.sprite = PIXI.Sprite.from(fishImage)
    }

}
```
<Br>

## Sprite toevoegen aan canvas?

In de `Game` class zag je dat sprites aan de canvas worden toegevoegd met `this.pixi.stage.addChild()`

Omdat we nu in een aparte class zijn, moeten we dat doen via de `game` variabele die we via de `constructor` kunnen opvragen.

### Animatie

In de `update` functie plaats je code die elk frame uitgevoerd moet worden. ⚠️ Let op dat je hier geen nieuwe `ticker` hoeft aan te maken! De `ticker` staat al in de `Game` class.

```typescript
import { fishImage } from "./images/fish.png"
import { Game } from "./Game"

class Fish {
    sprite: PIXI.Sprite
    // plaats de game variabele in de constructor
    constructor(game:Game){
        this.sprite = PIXI.Sprite.from(fishImage)
        this.sprite.anchor.set(0.5)
        this.sprite.x = game.pixi.screen.width / 2
        this.sprite.y = game.pixi.screen.height / 2
        game.pixi.stage.addChild(this.sprite)
    }
    update(delta){
        this.sprite.rotation += 0.1 * delta
    }
}
```

<br>
<br>
<br>

# Fish toevoegen aan de Game

In de Game class maken we een `property` voor een Fish. Daarin plaatsen we een `new Fish()`. In de `update()` functie kan je de Fish updaten. Je `Game` class gaat er dan als volgt uit zien:
```typescript
import * as PIXI from "pixi.js"
import { Fish } from "./Fish"

export class Game {

    pixi: PIXI.Application
    Fish: Fish

    constructor() {
        const container = document.getElementById("container")!
        this.pixi = new PIXI.Application({ width: 900, height: 500 })
        container.appendChild(this.pixi.view)
        this.pixi.ticker.add((delta) => this.update(delta))

        this.fish = new Fish(this)
    }

    update(delta) {
        this.fish.update(delta)
    }
}

new Game()
```

<br>
<br>
<br>

# Opdracht

Zet het aquarium met vissen en bubbles van week 1 om naar Object Oriented Code. Maak een class voor:

- Game
- Fish
- Background
- Bubble

![fishes](../week1/opdracht.jpg)

- Je hoeft nog geen animatie toe te voegen, je kan de `update` functie in `Fish` en `Bubble` dus even leeg laten.
- Je kan een `for` loop gebruiken om meerdere vissen aan te maken in de `Game` class.
- Je kan `Math.random()` gebruiken in de `Fish` en `Bubble` classes, om de x en y posities random te maken.
- Je kan `sprite.tint = Math.random() * 0xFFFFFF;` gebruiken voor een random kleur in de `Fish` class.

<br>
<br>
<br>

# Opdracht

Maak de `Fishes` [clickable met de voorbeelcode van PixiJS](https://pixijs.io/examples/#/interaction/click.js). 

Als je op een Fish klikt, verander je het plaatje in een skelet! Maak de `onClick` functie waarin de sprite verandert.

Plaats onderstaande code snippets op de juiste plek in de `Fish` class:

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

