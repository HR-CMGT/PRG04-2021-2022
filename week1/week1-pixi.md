# Week 1 - PixiJS voorbeelden

Op de [PixiJS site](https://pixijs.io/examples/) vind je veel voorbeelden voor het werken met Pixi. In week 1 kan je deze voorbeelden plakken in `game.ts` om te kijken of het werkt in onze development omgeving!

<br>
<br>
<br>

## Canvas

Je hoeft de pixi app (met het html canvas) maar één keer aan te maken. In deze canvas plaats je al je game elementen.

```javascript
import * as PIXI from 'pixi.js'

const pixi = new PIXI.Application({ backgroundColor: 0x1099bb, width: 900, height: 500 })
document.body.appendChild(pixi.view)
```

<br>
<br>
<br>

## 🐰 Sprite  

https://pixijs.io/examples/#/sprite/basic.js

```javascript
import fish from "./images/fish.png"

const fish = PIXI.Sprite.from(fish)

fish.anchor.set(0.5)
fish.x = pixi.screen.width / 2
fish.y = pixi.screen.height / 2

pixi.stage.addChild(fish)

pixi.ticker.add((delta) => {
    fish.rotation += 0.1 * delta
})
```
Je kan meerdere sprites maken van dezelfde afbeelding
```javascript
const anotherFish = PIXI.Sprite.from(fish)
```

<br>
<br>
<br>

## ⏱ Ticker

⚠️ Als je meerdere sprites gaat animeren, hoef je niet meerdere keren `app.ticker` aan te roepen. Plaats al je animaties in dezelfde `app.ticker` functie.

```javascript
pixi.ticker.add((delta) => {
    fish.rotation += 0.1 * delta
    anotherFish.y += 1 * delta
})
```

<br>
<br>
<br>

## 💬 Text

https://pixijs.io/examples/#/text/text.js

```javascript
const basicText = new PIXI.Text(`Score: 0 Lives: 3`)
basicText.x = 50
basicText.y = 100

pixi.stage.addChild(basicText)
```

<br>
<br>
<br>


# Opdracht

Maak een aquarium met vissen en bubbles zoals in deze afbeelding. Dit hoeft nog niet te animeren.

![fishes](./opdracht.jpg)

- Je kan een `for` loop en `Math.random()` gebruiken om meerdere vissen op random posities te plaatsen.
- Je kan `sprite.tint = Math.random() * 0xFFFFFF;` gebruiken voor een random kleur.
- Optioneel: plaats de fish en bubble sprites in een array, zodat je ze in de `ticker` kan laten bewegen 😱 .

<br>
<br>
<br>