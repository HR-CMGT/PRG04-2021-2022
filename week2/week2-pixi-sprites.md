# Week 2 - Array van sprites

![fishes](../week1/opdracht.jpg)

Als je voor elke sprite een property aanmaakt in de `Game` class, dan wordt het snel onhandig om heel veel sprites te hebben. Daarom maken we de `sprite` property een array. Let op dat deze property nu `sprites` heet.

```javascript
class Game {
    sprites : PIXI.Sprite[] = []
}
```

<Br>
<Br>
<br>

## For loop

Gebruik nu een `for` loop in de `constructor` om een heleboel sprites tegelijk aan te maken. Gebruik `this.sprites.push(...)` om de sprite in de array te zetten.

Geef elke sprite weer een random kleur en positie.

```javascript
class Game {
    sprites : PIXI.Sprite[] = []
    constructor(){
        for (...) {
            ...
        }
    }
}
```

<Br>
<br>
<br>

## Animatie

In de `update` functie kan je door je array heen loopen, om elke sprite te verplaatsen:

```javascript
class Game {
    ...
    update(delta) {
        for(let sprite of this.sprites){
            sprite.x += 1 * delta
        }
    }
}
```

Maak de afbeelding na met animerende bubbles en sprites. Kan je de bubbles omhoog laten bewegen en de fishes naar links?



<br>
<br>
<br>

# Opdracht

Als het je is gelukt om sprites te tonen in de Game class, dan kan je met behulp van de PixiJS voorbeelden ook Tekst en Graphics in je Game class plaatsen. 

- [PixiJS Text](https://pixijs.io/examples/#/text/text.js)
- [PixiJS Graphic](https://pixijs.io/examples/#/graphics/simple.js)