# Preloader

Om met assets te werken is het eigenlijk noodzakelijk om alle afbeeldingen, geluid, etc. in te laden voordat je game begint. Hiervoor kan je `PIXI.Loader` gebruiken. Bij geluiden plaats je `url:` in het `import` statement.

```typescript
import * as PIXI from "pixi.js"

// assets
import fishImage from "./images/fish.png"
import waterImage from "./images/water.jpg"

import coinSoundFile from "url:../sound/coin.mp3"  
import jumpSoundFile from "url:../sound/jump.mp3"  

// sprite classes
import { Fish } from "./Fish" 
import { Water } from "./Water"

export class Game {

    pixi: PIXI.Application
    loader : PIXI.Loader

    constructor() {
        this.pixi = new PIXI.Application({ width: 900, height: 500 })
        document.body.appendChild(this.pixi.view)

        // image preloader
        this.loader = new PIXI.Loader()
        this.loader
            .add("fish", fishImage)
            .add("bubble", bubbleImage)
            .add("coin", coinSoundFile)
            .add("jump", jumpSoundFile)
        

        this.loader.onProgress.add((loader) => this.showProgress(loader))
        this.loader.onError.add((arg) => {console.error(arg)})
        this.loader.load(() => this.doneLoading())
    }

    showProgress(p:PIXI.Loader){
        console.log(p.progress)
    }

    doneLoading(){
        console.log("preloader finished")

        // use the images for creating sprites
        let fish = new Fish(this.loader.resources["fish"].texture!)
        this.pixi.stage.addChild(fish)

        let bubble = new Bubble(this.loader.resources["bubble"].texture!)
        this.pixi.stage.addChild(bubble)

        // use the sounds for creating audio elements
        let coinSound = this.loader.resources["coinsound"].data!
        coinSound.play()

        let jumpSound = this.loader.resources["coinsound"].data!
        jumpSound.play()
    }
}
```
> Als je in jouw code `this.loader = new PIXI.Loader()` gebruikt, dan roep je de loader aan met `this.loader`.

<br>
<br>
<br>

# Sound Error

⚠️ Als je geluid wil spelen in je game kan je deze error krijgen:

> `Uncaught (in promise) DOMException: play() failed because the user didn't interact with the document first.`

Dit kan je oplossen door een moment van interactie in je game te bouwen, bijvoorbeeld een START knop waar je op moet drukken voor de game begint.

<br>
<br>
<br>

## Links

- [🔥 Genereer je eigen game sounds!](https://sfxr.me)
- [Pixi Loader Documentatie](https://pixijs.download/release/docs/PIXI.Loader.html)
- [Browser Sound Policy](https://goo.gl/xX8pDD)

