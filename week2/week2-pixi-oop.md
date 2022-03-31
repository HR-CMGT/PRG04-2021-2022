# Week 1 - PixiJS toepassen in Classes

Op de [PixiJS site](https://pixijs.io/examples/) vind je veel voorbeelden voor het werken met Pixi. We gaan [de voorbeeldcode voor een PixiJS Sprite](https://pixijs.io/examples/#/sprite/basic.js) omzetten naar classes.

<br>
<br>
<br>
<br>

# 🕹 Game Class

In een OOP game hebben we altijd één `Game` class waarin het canvas van PixiJS wordt aangemaakt. 

<br>

## Game loop

De `Game` class bevat de ***main game loop***. De `ticker` functie van PixiJS roept `update(delta)` 60 keer per seconde aan. 

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
        console.log(`Dit is de Game Loop!`)
    }
}

new Game()
```
<br>
<br>
<br>



<br>
<br>
<br>

# 🐠 Fish Class  

Je game elementen krijgen elk een eigen class. We maken hier een nieuwe class aan voor een `Fish`, en plaatsen daarin functies en eigenschappen die bij een Fish horen. 

In dit geval is dat een *sprite* (de afbeelding), en de *positie* en *rotatie* van die sprite. Daarom maken we van `sprite` een property. Gebruik `this.sprite` om de sprite ook daadwerkelijk aan te maken.

### Properties
```typescript
import { fishImage } from "./images/fish.png"

class Fish {
    // property
    sprite:PIXI.Sprite

    constructor(){
        // gebruik "this.sprite" om de property te vullen
        this.sprite = PIXI.Sprite.from(fishImage)
    }

}
```
<Br>

## Stage addChild

In de PixiJS examples zie je dat sprites aan de canvas worden toegevoegd met `app.stage.addChild()`

Omdat onze Pixi canvas in de `Game` staat, hoeven we niet in de Bunny nog een keer een canvas aan te maken. In plaats daarvan gebruiken we een `game` variabele in de constructor.

```typescript
import { fishImage } from "./images/fish.png"
import { Game } from "./Game"

class Fish {
    sprite: PIXI.Sprite
    // plaats de game variabele in de constructor
    constructor(game:Game){
        this.sprite = PIXI.Sprite.from(fishImage)
        this.sprite.anchor.set(0.5)

        // nu kan je game.pixi gebruiken om het scherm te meten
        // en om addChild uit te voeren
        this.sprite.x = game.pixi.screen.width / 2
        this.sprite.y = game.pixi.screen.height / 2
        game.pixi.stage.addChild(this.sprite)
    }
}
```
<br>

### Animatie

In de `update` functie plaats je code die elk frame uitgevoerd moet worden. ⚠️ Let op dat je hier geen nieuwe `ticker` hoeft aan te maken! De `ticker` staat al in de `Game` class.

```typescript
class Fish {
    ...
    update(delta){
        this.sprite.rotation += 0.1 * delta
    }
}
```

<br>
<br>
<br>

# Fish toevoegen aan de Game

In de Game class maken we een `property` voor een Fish. Daarin plaatsen we een `new Fish()`. In de `update()` functie kan je de Fish updaten. Je `Game` class gaat er dan als volgt uit zien:
```typescript
import * as PIXI from "pixi.js"
import { Fish } from "./Fish"

export class Game {

    pixi: PIXI.Application
    Fish: Fish

    constructor() {
        const container = document.getElementById("container")!
        this.pixi = new PIXI.Application({ width: 900, height: 500 })
        container.appendChild(this.pixi.view)
        this.pixi.ticker.add((delta) => this.update(delta))

        this.fish = new Fish(this)
    }

    update(delta) {
        this.fish.update(delta)
    }
}

new Game()
```

<br>
<br>
<br>

# Opdracht

Zet het aquarium met vissen en bubbles van week 1 om naar Object Oriented Code. Maak een class voor:

- Game
- Fish
- Background
- Bubble

![fishes](../week1/opdracht.jpg)

- Je hoeft nog geen animatie toe te voegen, je kan de `update` functie in `Fish` en `Bubble` dus even leeg laten.
- Je kan een `for` loop gebruiken om meerdere vissen aan te maken in de `Game` class.
- Je kan `Math.random()` gebruiken in de `Fish` en `Bubble` classes, om de x en y posities random te maken.
- Je kan `sprite.tint = Math.random() * 0xFFFFFF;` gebruiken voor een random kleur in de `Fish` class.

<br>
<br>
<br>

# Opdracht

Maak de `Fishes` [clickable met de voorbeelcode van PixiJS](https://pixijs.io/examples/#/interaction/click.js). 

```javascript
this.sprite.interactive = true;
this.sprite.buttonMode = true;
this.sprite.on('pointerdown', () => this.onClick())
```
Als je op een Fish klikt, verander je het plaatje in een skelet! Maak de `onClick` functie waarin de sprite verandert.

```javascript
import { skeletonImage } from "./images/bones.png"
this.sprite = PIXI.Sprite.from(skeletonImage)
```

