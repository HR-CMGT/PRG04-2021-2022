# PixiJS Examples in een class

In dit voorbeeld zie je hoe je de [PixiJS Examples](https://pixijs.io/examples/) kan gebruiken in jouw OOP game.

<br>
<br>
<br>
<br>

## PixiJS Example: sprite 🐰 

De [voorbeeldcode voor een PixiJS sprite](https://pixijs.io/examples/#/sprite/basic.js) is als volgt:

```javascript
const app = new PIXI.Application({ backgroundColor: 0x1099bb });
document.body.appendChild(app.view);

// create a new Sprite from an image path
const bunny = PIXI.Sprite.from('examples/assets/bunny.png');

// center the sprite's anchor point
bunny.anchor.set(0.5);

// move the sprite to the center of the screen
bunny.x = app.screen.width / 2;
bunny.y = app.screen.height / 2;

app.stage.addChild(bunny);

// Listen for animate update
app.ticker.add((delta) => {
    // just for fun, let's rotate mr rabbit a little
    // delta is 1 if running at 100% performance
    // creates frame-independent transformation
    bunny.rotation += 0.1 * delta;
});
```

<br>
<br>
<br>
<br>

# Code verdelen over Game Class en Bunny class

## Stap 1 - Bunny class aanmaken 🐰 

We beginnen met het kijken welke code echt bij een `Bunny` hoort. Dat is zijn *sprite* (de afbeelding), *positie* en *rotatie*. Ook de actie die de `Bunny` elk frame moet uitvoeren (draaien) moet in de `Bunny` class komen.

Om de sprite toe te voegen aan pixi, en om te weten hoe groot het scherm is, hebben we de `app` variabele nodig. Die kunnen we opvragen via de `constructor`. 

```typescript
import { bunnyImage } from "./images/bunny.png"
import { App } from "./App"

class Bunny {
    private sprite: PIXI.Sprite
    constructor(app:App){
        this.sprite = PIXI.Sprite.from(bunnyImage)
        this.sprite.anchor.set(0.5)
        this.sprite.x = app.screen.width / 2
        this.sprite.y = app.screen.height / 2
        app.stage.addChild(this.sprite)
    }
}
```
<br>

## Stap 2 - Animatie

In de `Bunny` class hoef je alleen de code te plaatsen die elk frame uitgevoerd moet worden, dit doe je in de `update()` functie. ⚠️ Let op dat je hier geen nieuwe `ticker` hoeft aan te maken!

```typescript
class Bunny {
    ...
    public update(delta){
        this.sprite.rotation += 0.1 * delta
    }
}
```

<br>
<br>
<br>

## Bunny toevoegen aan de Game

In een OOP game hebben we altijd één `Game` class waarin de basiselementen van PixiJS al staan, zoals het `canvas` element, de `pixi` application en het aanroepen van de `ticker` functie: 

```typescript
import * as PIXI from "pixi.js"

export class Game {

    public pixi: PIXI.Application

    constructor() {
        const container = document.getElementById("container")!
        this.pixi = new PIXI.Application({ width: 900, height: 500 })
        container.appendChild(this.pixi.view)
        this.pixi.ticker.add((delta) => this.update(delta))
    }

    private update(delta) {
        
    }
}
```

Hierin maak je een `new Bunny()` aan en roep je de `update()` functie van de `Bunny` aan:

```typescript
import { Bunny } from "./Bunny"

export class Game {

    ...
    private bunny: Bunny

    constructor() {
        ...
        this.bunny = new Bunny(this)
    }

    private update(delta) {
        this.bunny.update(delta)
    }
}
```