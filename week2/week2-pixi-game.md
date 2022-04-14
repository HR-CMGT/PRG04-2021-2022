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

In een OOP game hebben we altijd één `Game` class waarin we de Pixi basics aanmaken. Hierin laden we alle textures voor de hele game, en daarna starten we de game loop.

```typescript
import * as PIXI from "pixi.js"
import fishImage from "../images/fish.png"
import bgImage from "../images/background.png"

export class Game {

    pixi: PIXI.Application

    constructor() {
        this.pixi = new PIXI.Application({ width: 900, height: 500 })
        document.body.appendChild(this.pixi.view)

        this.pixi.loader
            .add("fishTexture", fishImage)
            .add("backgroundTexture", bgImage)

        this.pixi.loader.load(() => this.doneLoading())
    }

    doneLoading() {
        console.log("all textures loaded!")
        this.pixi.ticker.add((delta) => this.update(delta))
    }

    update(delta : number) {
        console.log(`Dit is de Game Loop!`)
    }
}

new Game()
```
De `update(delta)` functie is de ***main game loop*** van onze game. Deze wordt 60 keer per seconde aangeroepen. Omdat we met ***Typescript*** werken moet je aangeven dat `delta` een `number` is.

<br>
<br>
<br>

# 🐠 Sprites  

In [week 1 hebben we sprites getekend in het canvas](../week1/week1-pixi.md). We gaan deze code nu in `Game.ts` plaatsen. Dit doen we in `doneLoading` omdat we dan zeker weten dat alle plaatjes geladen zijn.

```typescript
export class Game {

    pixi: PIXI.Application
    fish:PIXI.Sprite
    anotherFish:PIXI.Sprite

    constructor() {
        ...
    }

    doneLoading() {
        console.log("all textures loaded!")

        this.fish = new PIXI.Sprite(loader.resources["fishTexture"].texture!)
        this.pixi.stage.addChild(this.fish)

        this.anotherFish = new PIXI.Sprite(loader.resources["fishTexture"].texture!)
        this.pixi.stage.addChild(this.anotherFish)

        this.pixi.ticker.add((delta) => this.update(delta))
    }

    update(delta : number) {
        this.fish.x -= 2
        this.anotherFish.x -= 3
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
