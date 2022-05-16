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

Kan je de vissen clickable maken? Zodra je klikt zet je de vis heel ver naar rechts zodat het even duurt voordat de vis weer in beeld verschijnt. 

<br>
<br>
<br>

# Opdracht

Zodra je op een fish klikt, verander je het het texture van de fish in `bones.jpg`. Je kan het texture van een sprite veranderen met `this.texture = ...`. Je zou dat tweede texture ook kunnen meegeven zodra je een `new Fish()` aanmaakt. Maak dan een property waar het bones texture in komt te staan.

```typescript
export class Fish extends PIXI.Sprite {

    deadTexture : PIXI.Texture
    
    constructor(texture: PIXI.Texture, deadTexture: PIXI.Texture) {
        super(texture)
        this.deadTexture = deadTexture
    }
}
```

<br>
<br>
<br>

# Opdracht

De vis krijgt een property `alive`. Zet deze op `false` als de vis dood is. Als de vis dood is, dan zwemt de vis niet meer naar links. In plaats daarvan zakt de vis naar de bodem, totdat de bodem bereikt is. 

<br>
<br>
<br>

## Links

- [Click voorbeeld PixiJS](https://pixijs.io/examples/#/interaction/click.js)
- [PixiJS Classes Youtube Tutorial](https://www.youtube.com/watch?v=NG5qxx9Ij6Q)
- [:movie_camera: Composition in OOP](https://youtu.be/xTOhht5-eg0)
