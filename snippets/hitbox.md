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

        // teken een groene box
        let area = this.getBounds()
        let greenBox = new PIXI.Graphics()
        greenBox.lineStyle(2, 0x33FF33, 1)
        greenBox.drawRect(0 - area.width/2, 0 - area.height/2, area.width, area.height)
        this.addChild(greenBox)
    }
}
```

<br>
<br>
<br>

## Custom hitbox

![boxb](./hitboxb.png)

Soms wil je dat je hitbox kleiner of groter is dan de texture van je sprite. In dit voorbeeld gebruiken we een *custom rectangle* als hitbox:

```typescript
class Shark extends PIXI.Sprite {

    constructor(texture){
        super(texture)

        // custom hitbox - de sprite texture is 270 x 135
        this.hitArea = new PIXI.Rectangle(0,0,200,100)
        
        let area = this.getBounds()
        let greenBox = new PIXI.Graphics()
        greenBox.lineStyle(2, 0x33FF33, 1)
        greenBox.drawRect(0 - area.width / 2, 0 - area.height / 2, area.width, area.height)
        this.addChild(greenBox)

    }

    // zorg dat getbounds de hitarea terug geeft
    getBounds() : PIXI.Rectangle {
        return this.hitArea as PIXI.Rectangle
    }
}
```

<br>
<br>
<br>