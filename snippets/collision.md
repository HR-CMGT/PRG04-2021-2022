# Collision

Om te testen of twee sprites (rechthoeken) elkaar overlappen kan je de `getBounds()` functie van een sprite gebruiken:

```typescript
import blockImage from "../images/block3.png"

export class Game {

    blockOne: PIXI.Sprite
    blockTwo: PIXI.Sprite

    constructor() {
        this.blockOne = PIXI.Sprite.from(blockImage)
        this.blockTwo = PIXI.Sprite.from(blockImage)
    }

    update(delta:number) {
        this.blockOne.x += 1 * delta
        this.blockTwo.x += 3 * delta

        if(this.collision(this.blockOne, this.blockTwo)){
            console.log("the blocks touch each other ❤️")
        }
    }

    collision(spriteOne:PIXI.Sprite, spriteTwo:PIXI.Sprite) {
        const bounds1 = spriteOne.getBounds()
        const bounds2 = spriteTwo.getBounds()

        return bounds1.x < bounds2.x + bounds2.width
            && bounds1.x + bounds1.width > bounds2.x
            && bounds1.y < bounds2.y + bounds2.height
            && bounds1.y + bounds1.height > bounds2.y;
    }
}

```
> ⚠️ Dit voorbeeld toont alleen de collision code, maar niet het aanmaken van het pixi canvas of het aanroepen van de ticker. Zie daarvoor de [default game class](../week2/week2-pixi-game.md).