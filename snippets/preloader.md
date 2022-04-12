# Preloader

Om met sprites te werken is het eigenlijk noodzakelijk om alle afbeeldingen in te laden voordat je game begint. Hiervoor kan je `PIXI.Loader` gebruiken:

```typescript
import * as PIXI from "pixi.js"
// png images
import fishImage from "./images/fish.png"
import waterImage from "./images/water.jpg"
import bubbleImage from "./images/bubble.png"
// sprite classes
import { Fish } from "./Fish" 
import { Water } from "./Water" 
import { Bubble } from "./Bubble" 

export class Game {

    pixi: PIXI.Application

    constructor() {
        this.pixi = new PIXI.Application({ width: 900, height: 500 })
        document.body.appendChild(this.pixi.view)

        // image preloader
        this.pixi.loader
            .add("fish", fishImage)
            .add("bubble", bubbleImage)
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

        let bg = new Water(this.pixi.loader.resources["water"].texture!)
        this.pixi.stage.addChild(bg)

        let fish = new Fish(this.pixi.loader.resources["fish"].texture!)
        this.pixi.stage.addChild(fish)

        let bubble = new Bubble(this.pixi.loader.resources["bubble"].texture!)
        this.pixi.stage.addChild(bubble)
    }
}
```