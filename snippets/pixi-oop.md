# PixiJS voorbeelden gebruiken in OOP

Op de [PixiJS site](https://pixijs.io/examples/) vind je veel voorbeelden voor het werken met Pixi. Op deze pagina zie je hoe je deze voorbeelden kan toepassen in jouw OOP game. Bekijk ook deze [Youtube Tutorial](https://www.youtube.com/watch?v=NG5qxx9Ij6Q) voor het werken met Classes in Pixi.

<br>
<br>
<br>
<br>

# PixiJS Sprite 🐰 

De [voorbeeldcode voor een PixiJS Sprite](https://pixijs.io/examples/#/sprite/basic.js) is als volgt:

```javascript
const app = new PIXI.Application({ backgroundColor: 0x1099bb })
document.body.appendChild(app.view)
const bunny = PIXI.Sprite.from('examples/assets/bunny.png')
bunny.anchor.set(0.5)
bunny.x = app.screen.width / 2
bunny.y = app.screen.height / 2
app.stage.addChild(bunny)
app.ticker.add((delta) => {
    bunny.rotation += 0.1 * delta
})
```
We gaan deze code omzetten naar een `Bunny` class en een `Game` class:


<br>
<br>
<br>
<br>

# 🕹 Game Class

In een OOP game hebben we altijd één `Game` class waarin de basiselementen van PixiJS al staan, zoals het `canvas` element, de `pixi` application en het aanroepen van de `ticker` functie. 


```typescript
import * as PIXI from "pixi.js"

export class Game {

    pixi: PIXI.Application

    constructor() {
        this.pixi = new PIXI.Application({ width: 900, height: 500 })
        document.body.appendChild(this.pixi.view)
        this.pixi.ticker.add((delta) => this.update(delta))
    }

    update(delta:number) {
        console.log(`Dit is de Game Loop!`)
    }
}
```
<br>
<br>
<br>

# 🐰 Bunny Class  

We maken een class aan voor de `Bunny`, en plaatsen daarin functies en eigenschappen die bij de Bunny horen. Voor nu is dat alleen de positie en het middelpunt.

In de `update()` functie plaats je de code die elk animatie frame uitgevoerd moet worden.

### Properties
```typescript
import * as PIXI from "pixi.js"

class Bunny extends PIXI.Sprite {

    constructor(texture: PIXI.Texture) {
        super(texture)
        this.anchor.set(0.5)
        this.x = 100
        this.y = 100
    }

    update(delta){
        this.sprite.rotation += 0.1 * delta
    }

}
```


<br>
<br>
<br>

## Bunny toevoegen aan de Game

Met de pixi preloader laden we eerst de `textures` voor alle sprites.

In de Game class maken we een `property` voor een bunny. Daarin plaatsen we een `new Bunny()`. Je moet de texture meegeven. Vervolgens plaats je de sprite in het pixi canvas met de `addChild` functie.

In de `update()` functie van de `Game` kan je de `update()` functie van de bunny aanroepen:

```typescript
import bunnyImage from "./images/bunny.png"
import enemyImage from "./images/enemy.png"
import { Bunny } from "./Bunny"

export class Game {

    bunny: Bunny

    constructor() {
          // load all textures for the whole game
        this.pixi.loader
            .add("bunnytexture", bunnyImage)
            .add("enemytexture", enemyImage)

        this.pixi.loader.onProgress.add((p: PIXI.Loader) => this.showProgress(p))
        this.pixi.loader.onComplete.add(() => this.doneLoading())
        this.pixi.loader.load()
    }

    showProgress(p: PIXI.Loader) {
        console.log(`Loading ${p.progress}%`)
    }

    doneLoading() {
        console.log("preloader finished")

        // create the bunny
        this.bunny = new Bunny(this.pixi.loader.resources["bunny"].texture!)
        this.pixi.stage.addChild(this.bunny)
    }

    update(delta) {
        // update the bunny 
        this.bunny.update(delta)
    }
}
```

<br>
<br>
<br>

## Links

- [📺 PixiJS Classes Youtube Tutorial](https://www.youtube.com/watch?v=NG5qxx9Ij6Q)
