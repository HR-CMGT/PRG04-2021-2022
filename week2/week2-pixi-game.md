# Week 2 - Game Class

Op de [PixiJS site](https://pixijs.io/examples/) vind je veel voorbeelden voor het werken met Pixi. De minimum code voor een PIXI app is:

```javascript
const app = new PIXI.Application({ width: 900, height : 450 })
document.body.appendChild(app.view)

app.ticker.add((delta) => {
    console.log("animating....")
})
```
<br>
<br>
<br>
<br>

# 🕹 Game Class

In een OOP game hebben we altijd één `Game` class waarin we de Pixi basics aanmaken: 

```typescript
import * as PIXI from "pixi.js"

export class Game {

    pixi: PIXI.Application

    constructor() {
        const container = document.getElementById("container")!
        this.pixi = new PIXI.Application({ width: 900, height: 500 })
        container.appendChild(this.pixi.view)
        this.pixi.ticker.add((delta) => this.update(delta))
    }

    update(delta) {
        console.log(`Dit is de Game Loop!`)
    }
}

new Game()
```
## Game loop

De `update(delta)` functie is de ***main game loop*** van onze game. Deze wordt 60 keer per seconde aangeroepen. 

<br>
<br>
<br>

# 🐠 Sprite voorbeeld  

We gaan het [sprite voorbeeld](https://pixijs.io/examples/#/sprite/basic.js) in de `Game` class plaatsen!

```typescript
import * as PIXI from "pixi.js"
import { fishImage } from "./images/fish.png"

export class Game {

    pixi: PIXI.Application
    // property aanmaken voor een sprite
    sprite:PIXI.Sprite

    constructor() {
        const container = document.getElementById("container")!
        this.pixi = new PIXI.Application({ width: 900, height: 500 })
        container.appendChild(this.pixi.view)
        this.pixi.ticker.add((delta) => this.update(delta))

        // sprite aanmaken
        this.sprite = PIXI.Sprite.from(fishImage)
        this.sprite.anchor.set(0.5)
        this.sprite.x = game.pixi.screen.width / 2
        this.sprite.y = game.pixi.screen.height / 2
        this.pixi.stage.addChild(this.sprite)
    }

    update(delta) {
        // sprite animatie 60fps
        this.sprite.rotation += 0.1 * delta
    }
}
```
<Br>
<br>
<br>

# Opdracht

Plaats een aantal vissen, bubbles en de achtergrond afbeelding in de game class.

![fishes](../week1/opdracht.jpg)

- Je hoeft nog geen animatie toe te voegen, je kan de `update` functie in `Game` dus even leeg laten.
- Je kan een `for` loop gebruiken om meerdere vissen aan te maken in de `Game` class.
- Je kan `Math.random()` gebruiken om de x en y posities random te maken.
- Je kan `sprite.tint = Math.random() * 0xFFFFFF;` gebruiken voor een random kleur.

<br>
<br>
<br>

# Opdracht

Als het je lukt om met de `Game` class te werken, dan kan je verder met deel 2. Hierin gaan we de `Fish` in een eigen class zetten.

[Verder met deel 2](./week2-pixi-oop.md)