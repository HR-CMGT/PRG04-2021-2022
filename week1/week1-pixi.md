# Week 1 - PixiJS voorbeelden gebruiken

Op de [PixiJS site](https://pixijs.io/examples/) vind je veel voorbeelden voor het werken met Pixi. Op deze pagina leer je hoe je deze voorbeelden kan toepassen in jouw OOP game. Je kan dit gebruiken voor alle PixiJS examples!

<br>
<br>
<br>
<br>

# PixiJS Sprite 🐰 

De [voorbeeldcode voor een PixiJS Sprite](https://pixijs.io/examples/#/sprite/basic.js) is als volgt:

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

# Omzetten naar Object Oriented Programming

## 🕹 Game Class

In een OOP game hebben we altijd één `Game` class waarin de basiselementen van PixiJS al staan, zoals het `canvas` element, de `pixi` application en het aanroepen van de `ticker` functie. Deze class is altijd hetzelfde: 

```typescript
import * as PIXI from "pixi.js"

export class Game {

    pixi: PIXI.Application

    constructor() {
        const container = document.getElementById("container")!
        this.pixi = new PIXI.Application({ width: 900, height: 500 })
        container.appendChild(this.pixi.view)
        this.pixi.ticker.add((delta) => this.update(delta))
    }

    update(delta) {
        
    }
}
```
<br>
<br>
<br>

## 🐰 Bunny Class  

We maken een class aan voor de `Bunny`, en plaatsen daarin functies en eigenschappen die echt bij de Bunny horen, en niet bij de overkoepelende game. 

In dit geval is dat alleen een *sprite* (de afbeelding), en de *positie* en *rotatie* van die sprite. Daarom maken we van `sprite` een property. De property kan je vervolgens vullen via `this.sprite`.

### Properties
```typescript
import { bunnyImage } from "./images/bunny.png"

class Bunny {
    // property
    sprite:PIXI.Sprite

    constructor(){
        // gebruik "this.sprite" om de property te vullen
        this.sprite = PIXI.Sprite.from(bunnyImage)
    }

}
```
<Br>

### App variabele

In het PixiJS example zie je dat er een `app` variabele gebruikt wordt. Deze `app` variabele kunnen we opvragen via de `constructor`. 

```typescript
import { bunnyImage } from "./images/bunny.png"
import { App } from "./App"

class Bunny {
    sprite: PIXI.Sprite
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

### Animatie

In de `update` functie plaats je code die elk frame uitgevoerd moet worden. ⚠️ Let op dat je hier geen nieuwe `ticker` hoeft aan te maken! De `ticker` staat al in de `Game` class.

```typescript
class Bunny {
    update(delta){
        this.sprite.rotation += 0.1 * delta
    }
}
```

<br>
<br>
<br>

## Bunny toevoegen aan de Game

In de Game class maken we een `property` voor een bunny. Daarin plaatsen we een `new Bunny()`. 

In de `update()` functie van de `Game` kan je de `update()` functies van je bunny aanroepen:

```typescript
import { Bunny } from "./Bunny"

export class Game {

    // property voor een bunny
    bunny: Bunny

    constructor() {
        // bunny aanmaken
        this.bunny = new Bunny(this)
    }

    update(delta) {
        // update van bunny aanroepen
        this.bunny.update(delta)
    }
}
```

<br>
<br>
<br>

# Opdracht

[Bekijk het voorbeeld voor het plaatsen van tekst](https://pixijs.io/examples/#/text/text.js) en voeg een tekst toe aan je Bunny Game.

Maak een `class` met de naam `UI`. 

```typescript
class UI {
    constructor(){
        console.log("I am the UI 🧅")
    }
}
```


In de constructor plaats je de text code uit het PixiJS voorbeeld. Let op dat `app` al aangemaakt is in `Game`. De app vraag je op via de constructor:

```typescript
import { App } from "./App"

class UI {
    constructor(app:App){
        // maak hier een text element
        ...
        // voeg het text element toe aan de pixi stage
        app.stage.addChild(...)
    }
}
```
<br>
<br>
<br>

## 🧅 UI Toevoegen aan Game

Als laatste moet je een `new UI()` aanmaken in je `Game` class, op dezelfde manier als de `Bunny`. De UI heeft geen `update` functie.

```typescript
import { Bunny } from "./Bunny"
import { UI } from "./UI"

export class Game {

    // property voor een UI  
    ...

    constructor() {
        // de ui aanmaken
        ...
    }
}
```