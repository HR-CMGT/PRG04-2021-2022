# Week 1 - PixiJS Startproject

## Opdracht

[Je vindt hier een compleet startproject voor het vak PRG4](https://github.com/HR-CMGT/PRG04-2021-2022-startproject). Je kan dit startproject gebruiken voor alle oefeningen.

[Bekijk dit filmpje voor het snel opzetten van het startproject op je eigen computer](https://youtu.be/uuPprdiFKXI).

<br>
<br>
<br>

## Opdracht

Met `npm run start` start je de development omgeving. Dit hoef je maar één keer te doen. Als je wil stoppen druk je op `CTRL+C`.

Test of de code in `app.ts` werkt:

```javascript
import * as PIXI from 'pixi.js'
import fish from "./images/fish.png"

let app = new PIXI.Application({ width: 800, height: 450 })
document.body.appendChild(app.view)

let sprite = PIXI.Sprite.from(fish)
app.stage.addChild(sprite)
```
<br>
<br>
<br>

## Opdracht

Maak een aquarium met vissen en bubbles zoals in deze afbeelding. 

![fishes](./opdracht.jpg)

- Je kan een `for` loop en `Math.random()` gebruiken om meerdere vissen op random posities te plaatsen.
- Je kan `sprite.tint = Math.random() * 0xFFFFFF;` gebruiken voor een random kleur.

<br>
<br>
<br>

# Opdracht deel 2

In deel 2 gaan we kijken hoe we de PixiJS voorbeelden kunnen gebruiken in onze Object Oriented games.

[Ga naar deel 2](./week1-pixi.md)

<br>
<br>
<br>

# Links

- [📺 Installatie instructies filmpje](https://youtu.be/uuPprdiFKXI)
- [PixiJS Examples](https://pixijs.io/examples/) en [Getting started](https://pixijs.io/guides/basics/getting-started.html)
- [NodeJS](https://nodejs.org/en/) en [Visual Studio Code](https://code.visualstudio.com)
- [Zelf een PixiJS Typescript project opzetten from scratch](https://github.com/HR-CMGT/PRG04-2021-2022-startproject/blob/main/scratch.MD)