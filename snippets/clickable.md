# Clickable sprite

Maak een sprite interactive

```typescript
import * as PIXI from "pixi.js"

export class Fish extends PIXI.Sprite {

    bonesTexture:PIXI.Texture
    
    constructor(texture: PIXI.Texture, bonesTexture:PIXI.Texture) {
        super(texture)
        this.bonesTexture = PIXI.Texture.from(bonesImage)

        this.anchor.set(0.5)
        this.x = 400
        this.y = 200

        this.interactive = true
        this.buttonMode = true
        this.on('pointerdown', () => this.onClick())
    }

    onClick() {
        console.log("je klikt op een vis")
        this.texture = this.bonesTexture
    }

    update(delta : number) {
        this.x -= 2 * delta
        if(this.x < -100) this.x = 900
    }

}
```