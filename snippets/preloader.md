# Preloader

Als je heel veel images wil preloaden voordat de game uberhaupt begint, dan kan je `PIXI.Loader` gebruiken:

```typescript
import * as PIXI from "pixi.js"
import fishImage from "./images/fish.png"
import waterImage from "./images/water.jpg"
import bubbleImage from "./images/bubble.png"

export class Game {

    pixi: PIXI.Application

    constructor() {
        this.pixi = new PIXI.Application({ width: 900, height: 500 })
        document.body.appendChild(this.pixi.view)

        // image preloader
        this.pixi.loader
            .add("fish", fishImage)
            .add("bubble", bubImage)
            .add("bones", bonesImage)
            .add("water", waterImage)
        
        this.pixi.loader.onProgress.add((p:PIXI.Loader) => this.showProgress(p))
        this.pixi.loader.onComplete.add(() => this.doneLoading())
        this.pixi.loader.load()
    }

    showProgress(p:PIXI.Loader){
        console.log(p.progress)
    }

    doneLoading(){
        console.log("preloader finished")

        let bg = PIXI.Sprite.from(this.pixi.loader.resources["water"].texture!)
        this.pixi.stage.addChild(this.sprite)

        let fish = PIXI.Sprite.from(this.pixi.loader.resources["fish"].texture!)
        this.pixi.stage.addChild(fish)

        let bubble = PIXI.Sprite.from(this.pixi.loader.resources["bubble"].texture!)
        this.pixi.stage.addChild(bubble)
    }
}

new Game()
```