# Week 3 - Fish Class

In week 2 hebben we alle sprites uit het [voorbeeld](https://pixijs.io/examples/#/sprite/basic.js) rechtstreeks in de Game class aangemaakt.

Zodra je game elementen meer gedrag en eigenschappen krijgen, dan is het handiger om er een aparte class voor te maken.

<br>
<br>
<br>

## 🐠 Fish Class

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

## 😱 Help! Het canvas staat in de Game class!

In de `Game` class zag je dat sprites aan de canvas worden toegevoegd met `this.pixi.stage.addChild()`

Omdat we nu in een aparte class zijn, moeten we dat doen via de `game` variabele die we via de `constructor` kunnen opvragen.

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
### 🎬 Animatie

In de `update` functie plaats je code die elk frame uitgevoerd moet worden. ⚠️ Let op dat je hier geen nieuwe `ticker` hoeft aan te maken! De `ticker` staat al in de `Game` class.

<br>
<br>
<br>

# Fish toevoegen aan de Game Class

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

Maak een Class voor Game, Fish, Background, Bubble

- Je hoeft nog geen animatie toe te voegen, je kan de `update` functie in `Fish` en `Bubble` dus even leeg laten.
- Maak **twee fishes, twee bubbles en een background** aan in Game.
- Je kan `Math.random()` gebruiken in de `Fish` en `Bubble` classes, om de x en y posities random te maken.
- Je kan `sprite.tint = Math.random() * 0xFFFFFF;` gebruiken voor een random kleur in de `Fish` class.

<br>
<br>
<br>

# Opdracht

Om een groter aantal fishes en bubbles te kunnen aanmaken hebben we `Arrays` nodig.

[Ga naar de Arrays opdracht](./week3-arrays.md)