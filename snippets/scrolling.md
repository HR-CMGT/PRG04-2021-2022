# Scrolling background

Je kan een afbeelding eindeloos laten herhalen door er een `TilingSprite` van te maken:

```typescript
import * as PIXI from "pixi.js"
import bgImage from "../images/background.png"

export class Game {

  tiles: PIXI.TilingSprite

  constructor() {
    const texture = PIXI.Texture.from(bgImage)

    this.tiles = new PIXI.TilingSprite(
      texture,
      this.pixi.screen.width,
      this.pixi.screen.height
    )
    this.pixi.stage.addChild(this.tiles)
  }

  update() {
    this.tiles.tilePosition.x -= 3
  }
}

```

<br>
<br>

## Links

- [Tiling Sprite](https://pixijs.io/examples/#/sprite/tiling-sprite.js)