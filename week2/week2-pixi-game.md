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
        this.pixi = new PIXI.Application({ width: 900, height: 500 })
        document.body.appendChild(this.pixi.view)
        this.pixi.ticker.add((delta) => this.update(delta))
    }

    update(delta : number) {
        console.log(`Dit is de Game Loop!`)
    }
}

new Game()
```
## Game loop

De `update(delta)` functie is de ***main game loop*** van onze game. Deze wordt 60 keer per seconde aangeroepen. Omdat we met ***Typescript*** werken moet je aangeven dat `delta` een `number` is.

<br>
<br>
<br>

# 🐠 Sprites  

We gaan het [Sprite voorbeeld](https://pixijs.io/examples/#/sprite/basic.js) in `Game.ts` zetten.


// TODO PRELOADER EN NEW SPRITE() TOEVOEGEN HIER EN IN STARTPROJECT / WEEK 1 / PRESENTATIES



```typescript
import * as PIXI from "pixi.js"
import fishImage from "./images/fish.png"

export class Game {

    pixi: PIXI.Application
    sprite:PIXI.Sprite

    constructor() {
        this.pixi = new PIXI.Application({ width: 900, height: 500 })
        document.body.appendChild(this.pixi.view)

        this.sprite = PIXI.Sprite.from(fishImage)
        this.sprite.anchor.set(0.5)
        this.sprite.x = this.pixi.screen.width / 2
        this.sprite.y = this.pixi.screen.height / 2
        this.pixi.stage.addChild(this.sprite)

        // start de game loop
        this.pixi.ticker.add((delta) => this.update(delta))
    }

    update(delta : number) {
        // sprite animatie 60fps
        this.sprite.rotation -= 0.1 * delta
    }
}
```
<Br>
<br>
<br>

# Opdracht

![two](../week1/twofishes.png)

Plaats ***twee vissen, twee bubbles en één achtergrond afbeelding*** in de game class. 

- Je kan `Math.random()` gebruiken om de start `x,y` posities van de vissen en bubbles random te maken.
- Je kan `sprite.tint = Math.random() * 0xFFFFFF;` gebruiken voor een random kleur van de vis.
- Laat de vissen naar links bewegen en de bubbles naar boven.

<Br>
<br>
<br>

# Opdracht

Als de vissen links uit beeld zwemmen, moeten ze rechts weer in beeld verschijnen. Als de bubbles boven uit beeld verdwijnen, moeten ze onderin beeld weer verschijnen.

<br>
<br>
<br>

# Opdracht

[Ga verder met deel 2: een array van sprites](./week2-pixi-sprites.md)
