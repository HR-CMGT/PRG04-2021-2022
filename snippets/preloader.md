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

<br>
<br>
<br>

# Loading bar

Je kan de `progress` waarde gebruiken om een laadbalkje te tekenen! Voeg de volgende code toe aan je Game class:

```typescript
class Game {
    
    graphics:PIXI.Graphics

    constructor(){
        this.graphics = new PIXI.Graphics()
        this.pixi.stage.addChild(this.graphics)
    }

    showProgress(p:PIXI.Loader){
        console.log(`Loading ${p.progress}%`)
        let offset = 50
        let barWidth = (this.pixi.screen.width - (offset * 2)) * (p.progress/100)
        this.graphics.clear()
        this.graphics.beginFill(0x32DE49)
        this.graphics.drawRect(offset, this.pixi.screen.height/2 - 20, barWidth, 40)
        this.graphics.endFill()
    }

    doneLoading(){
        console.log("preloader finished")
        this.graphics.destroy()
    }

}
```

<br>
<br>
<br>

# Loader in eigen class 

Je `Game.ts` wordt overzichtelijker als je de [Loader en laadbalkje code in een eigen class zet](https://github.com/KokoDoko/pixidust/blob/main/src/ts/AssetLoader.ts).

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

