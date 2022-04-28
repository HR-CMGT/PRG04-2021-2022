# Hitbox

![hitbox](./hitboxa.png)

In de [collision](./collision.md) tutorial heb je gezien dat je met `sprite.getBounds()` de collision rectangle kan ophalen van een sprite.

Je kan met [Pixi Graphics](https://pixijs.io/examples/#/graphics/simple.js) die hitbox ook tekenen in je sprite. [*Maak wel eerst een `class` van je sprite*](./pixi-oop.md).

In dit voorbeeld tekenen we de hitbox over de sprite heen. *Omdat het `anchor` van de sprite in het midden zit, moet je de hitbox graphic een `offset` geven*.


```typescript
import * as PIXI from "pixi.js"

export class Shark extends PIXI.Sprite {

    constructor(texture:PIXI.Texture) {
        super(texture)

        this.anchor.set(0.5)
        this.x = -100
        this.y = 180

        let box = this.getBounds()
        let hitbox = new PIXI.Graphics()
        hitbox.lineStyle(2, 0x33FF33, 1)
        hitbox.drawRect(0 - box.width/2, 0 - box.height/2, box.width, box.height)
        this.addChild(hitbox)
    }
}
```

<br>
<br>
<br>

## Custom hitbox

![boxb](./hitboxb.png)

Soms wil je dat je hitbox kleiner of groter is dan de texture van je sprite. Je kan dan je eigen `rectangle` gebruiken als hitbox. Je overschrijft hiermee de standaard `getBounds` van de sprite.

```typescript
class Shark extends PIXI.Sprite {

    customHitbox : PIXI.Rectangle

    constructor(texture){
        super(texture)
      
        // de hitbox is 200x100, de sprite is 270x135
        this.customHitbox = new PIXI.Rectangle(0,0,200,100)
        let hitbox = new PIXI.Graphics()
        hitbox.lineStyle(2, 0x33FF33, 1)
        hitbox.drawRect(0 - this.customHitbox.width / 2, 0 - this.customHitbox.height / 2, this.customHitbox.width, this.customHitbox.height)
        this.addChild(hitbox)
    }

    // vervang de standaard getbounds functie
    getBounds() : PIXI.Rectangle {
        return this.customHitbox
    }

```

<br>
<br>
<br>