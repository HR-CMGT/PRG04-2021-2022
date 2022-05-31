# Scrolling background

Je kan een afbeelding eindeloos laten herhalen door een `TilingSprite` te maken:

*Background.ts*
```typescript
import * as PIXI from "pixi.js"

export class Background extends PIXI.TilingSprite {

    constructor(texture: PIXI.Texture, w:number, h:number) {
        super(texture, w, h)
    }

    public update() {
        this.tilePosition.x -= 3
    }
}
```
<br>
<Br>
<br>

Bij het maken van de TilingSprite moet je de breedte en hoogte doorgeven:

*GAME.TS*
```typescript
class Game {

    addBackground() {
        this.bg = new Background(this.pixi.loader.resources["background"].texture!, this.pixi.screen.width, this.pixi.screen.height)
        this.pixi.stage.addChild(this.bg)
    }

    update() {
        this.bg.update()
    }
}
```
<br>
<Br>
<br>

## Parallax scrolling

![parallax](./parallax.gif)

Door meerdere transparante achtergronden met een verschillende snelheid te laten scrollen krijg je een parallax effect.

<br>
<br>
<br>

## Links

- [Tiling Sprite](https://pixijs.io/examples/#/sprite/tiling-sprite.js)