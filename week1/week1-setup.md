# Week 1 - PixiJS Startproject

## Opdracht

[Je vindt hier een compleet startproject voor het vak PRG4](https://github.com/HR-CMGT/PRG04-2021-2022-startproject). Je kan dit startproject gebruiken voor alle oefeningen.

[Bekijk dit filmpje voor het snel opzetten van het startproject op je eigen computer](https://youtu.be/uuPprdiFKXI).

<br>
<br>
<br>

## Opdracht

Met `npm run start` start je de development omgeving. Dit hoef je maar één keer te doen. Als je wil stoppen druk je op `CTRL+C`.

Test of de code in `game.ts` werkt:

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


# Opdracht 

[Bekijk een aantal Pixi voorbeelden en maak het pixel aquarium](./week1-pixi.md)

<br>
<br>
<br>

# Links

- [📺 Installatie instructies filmpje](https://youtu.be/uuPprdiFKXI)
- [PixiJS Examples](https://pixijs.io/examples/) en [Getting started](https://pixijs.io/guides/basics/getting-started.html)
- [NodeJS](https://nodejs.org/en/) en [Visual Studio Code](https://code.visualstudio.com)
- [Zelf een PixiJS Typescript project opzetten from scratch](https://github.com/HR-CMGT/PRG04-2021-2022-startproject/blob/main/scratch.MD)