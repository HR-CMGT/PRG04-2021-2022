# Texture wisselen met Click Event

Hieronder zie je hoe je meerdere textures kan gebruiken in een sprite, en hoe je het [Click voorbeeld van PixiJS](https://pixijs.io/examples/#/interaction/click.js) kan gebruiken in een Class:

```typescript
import bunnyImage from "./images/bunny.png"
import deadBunnyImage from "./images/deadbunny.png"

export class Bunny {
    sprite: PIXI.Sprite
    bonesTexture : PIXI.Texture

    constructor(game: Game) {
        this.deadTexture = PIXI.Texture.from(deadBunnyImage)

        ...

        this.sprite.interactive = true
        this.sprite.buttonMode = true
        this.sprite.on('pointerdown', () => this.bunnyClicked())
    }

    bunnyClicked() {
        console.log("click!")
        this.sprite.texture = this.deadTexture
    }
}
```
Kan je de texture van de sprite vervangen door het skelet plaatje als je op de vis klikt?
