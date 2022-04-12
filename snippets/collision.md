# Collision

Om te testen of twee sprites (rechthoeken) elkaar overlappen kan je de `getBounds()` functie van een sprite gebruiken:

```typescript
import { Block } from "./block.ts"

export class Game {

    blockOne: Block
    blockTwo: Block

    constructor() {
        this.blockOne = new Block(blockTexture)
        this.blockTwo = new Block(blockTexture)
    }

    update(delta:number) {
        this.blockOne.update()
        this.blockTwo.update()

        if(this.collision(this.blockOne, this.blockTwo)){
            console.log("the blocks touch each other ❤️")
        }
    }

    collision(blockOne:PIXI.Sprite, blockTwo:PIXI.Sprite) {
        const bounds1 = blockOne.getBounds()
        const bounds2 = blockTwo.getBounds()

        return bounds1.x < bounds2.x + bounds2.width
            && bounds1.x + bounds1.width > bounds2.x
            && bounds1.y < bounds2.y + bounds2.height
            && bounds1.y + bounds1.height > bounds2.y;
    }
}

```
> ⚠️ Dit voorbeeld toont alleen de collision code, maar niet het aanmaken van het pixi canvas of het aanroepen van de ticker. Zie daarvoor de [default game class](../week2/week2-pixi-game.md).