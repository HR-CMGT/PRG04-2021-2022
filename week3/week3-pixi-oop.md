# Week 3 - Fish Class

In week 2 hebben we de sprites uit het [voorbeeld](https://pixijs.io/examples/#/sprite/basic.js) rechtstreeks in de Game class aangemaakt.

Zodra je game elementen **gedrag en eigenschappen** krijgen, dan kan je er een aparte class voor maken. De vis heeft als gedrag dat hij naar links zwemt, en als hij uit beeld gaat verschijnt hij rechts weer in beeld. 

<br>
<br>
<br>

# 🐠 Sprite Class

Om een sprite (*een sprite is een afbeelding met x en y positie, en nog veel meer eigenschappen*) in een eigen class te plaatsen kan je de volgende code gebruiken. 

> ⚠️ Let op de `extends` en `super` keywords, dit kan je niet weglaten. Dit zorgt dat jouw class nog steeds gezien wordt als een `sprite`.

```typescript
import * as PIXI from "pixi.js"

export class Fish extends PIXI.Sprite {
    
    constructor(texture: PIXI.Texture) {
        super(texture)
    }

    update(delta:number) {
        console.log("This fish is updating!")
    }
}

```
## Animatie

Net zoals in de `Game` class gebruik je `this` om de eigenschappen en gedrag van de `Fish` aan te roepen. We weten dat een sprite een `x` eigenschap heeft. We kunnen die `x` positie dus aanpassen met `this.x`

```typescript
export class Fish extends PIXI.Sprite {
    
    constructor(texture: PIXI.Texture) {
        super(texture)
        this.x = 100
    }

    update(delta:number) {
        this.x -= 5
    }
}

```

<br>
<br>

## 😱 Fish toevoegen aan de Game Class

Om de `Fish` in de `Game` te plaatsen kan je nu `new Fish()` gebruiken in plaats van `new PIXI.Sprite()`! Je hebt het `import` statement nodig zodat je editor weet waar de code van `Fish` staat.

```typescript
import { Fish } from "./Fish"

class Game {
    doneLoading() {
        // 👴🏻 Old code
        this.sprite = new PIXI.Sprite(loader.resources["fishTexture"].texture!)
        // 🤩 New code
        this.sprite = new Fish(loader.resources["fishTexture"].texture!)
    }
}
```
### 🎬 Animatie

Om de Fish te animeren kan je de `update` functie van de `Fish` aanroepen.

```typescript
class Game {
    update(delta:number) {
        this.sprite.update(delta)
    }
}
```


<br>
<br>
<br>

# Opdracht

Maak Classes voor Game, Fish, Background, Bubble

- Gebruik `Math.random()` in de `Fish` en `Bubble` classes, om de `this.x` en `this.y` posities random te maken.
- Gebruik `this.tint = Math.random() * 0xFFFFFF` voor een random kleur in de `Fish` class.
- Gebruik `this.scale.set(0.5)` om de schaal random te maken.

<br>
<br>
<br>

# Opdracht

Laat de vissen naar links zwemmen. Als de vis links uit beeld gaat, verschijnt de vis rechts weer in beeld. Doe hetzelfde met de bubbles, maar dan verticaal.

<br>
<br>
<br>

# Opdracht

Om een groter aantal fishes en bubbles te kunnen aanmaken hebben we `Arrays` nodig.

[Ga naar de Arrays opdracht](./week3-arrays.md)

<br>
<br>
<br>

## Links

- [Sprite documentatie](https://pixijs.download/dev/docs/PIXI.Sprite.html)
- [PixiJS Classes Youtube Tutorial](https://www.youtube.com/watch?v=NG5qxx9Ij6Q)
- [:movie_camera: Composition in OOP](https://youtu.be/xTOhht5-eg0)
