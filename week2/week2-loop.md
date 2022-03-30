# Game loop

In de `Game` class roepen we de `ticker` functie van PixiJS aan. Deze roept vervolgens de `update()` functie van `Game` 60 keer per seconde aan:

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
        console.log("I get called 60 times per second! ☎️ ")
    }
}
```

In de `update()` functie van `Game` kan je al je animatie code plaatsen. Meestal roep je hier de `update()` functies van andere game objecten aan.


```typescript
import { Bunny } from "./Bunny"

export class Game {

    bunny: Bunny

    constructor() {
        this.bunny = new Bunny(this)
    }

    update(delta) {
        // roep de update code van bunny aan
        this.bunny.update(delta)
    }
}
```

<br>
<br>
<br>

# Animatie

De game objecten zoals `Bunny` hebben ook een `update` functie. Hierin zet je wat er elk frame moet gebeuren. In dit voorbeeld *draait* en *verplaatst* de sprite telkens.

```typescript
import { bunnyImage } from "./images/bunny.png"
import { App } from "./App"

class Bunny {
    sprite: PIXI.Sprite
    constructor(app:App){
        this.sprite = PIXI.Sprite.from(bunnyImage)
        this.sprite.anchor.set(0.5)
        this.sprite.x = app.screen.width / 2
        this.sprite.y = app.screen.height / 2
        app.stage.addChild(this.sprite)
    }

    update(delta){
        this.sprite.rotation += 0.1 * delta
        this.sprite.x += 1 * delta
    }
}
```

## Delta variabele

Deze variabele heeft doorgaans een waarde van 1.  Dus `1 * delta` blijft `1`. De `delta` waarde kan veranderen als de CPU van de computer even traag (of heel snel) is. Hierdoor krijg je `framedrop` in plaats van dat je hele game ineens heel langzaam of heel snel wordt.