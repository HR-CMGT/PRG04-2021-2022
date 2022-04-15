# Sprite clickable maken

We kunnen een sprite interactief maken met `this.interactive`. We kunnen vervolgens een click listener toevoegen met `this.on(event)`. Daarin geef je aan welke functie uitgevoerd moet worden als iemand op de sprite klikt. 

```typescript
import * as PIXI from "pixi.js"

export class Bunny extends PIXI.Sprite {
    
    constructor(texture: PIXI.Texture) {
        super(texture)

        this.interactive = true
        this.buttonMode = true
        this.on('pointerdown', () => this.bunnyClicked())
    }

    update(delta:number) {
        this.rotation += 0.01
    }

    bunnyClicked() {
        console.log("click!")
        this.rotation = 0
    }
}
```

<br>
<br>
<br>

# Opdracht

Kan je de vissen en bubbles clickable maken? Zodra je klikt zet je de vis heel ver naar rechts zodat het even duurt voordat de vis weer in beeld verschijnt. Doe dit ook voor de bubbles, maar dan verticaal.

<br>
<br>
<br>

## Links

- [Click voorbeeld PixiJS](https://pixijs.io/examples/#/interaction/click.js)
