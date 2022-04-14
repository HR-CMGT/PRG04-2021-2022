# Week 1 - PixiJS Startproject

## Opdracht

[Je vindt hier een compleet startproject voor het vak PRG4](https://github.com/HR-CMGT/PRG04-2021-2022-startproject). Je kan dit startproject gebruiken voor alle oefeningen.

[Bekijk dit filmpje voor het snel opzetten van het startproject op je eigen computer](https://youtu.be/uuPprdiFKXI).

<br>
<br>
<br>

## Opdracht

Met `npm run start` start je de development omgeving. Je kan ook op `START ` klikken in VS Code. Dit hoef je maar één keer te doen. 

![run](./run_npm.png)

Test of de code in `game.ts` werkt. Wordt de vis getoond?

```javascript
import * as PIXI from 'pixi.js'
import fishImage from "./images/fish.png"
import bubbleImage from "./images/bubble.png"

// create a pixi canvas
const pixi = new PIXI.Application({ width: 800, height: 450 })
document.body.appendChild(pixi.view)

// preload all our textures
const loader = new PIXI.Loader()
loader.add('fishTexture', fishImage)
      .add('bubbleTexture', bubbleImage)
loader.load(()=>loadCompleted())

// after loading is complete, create a fish sprite
function loadCompleted() {
    let fish = new PIXI.Sprite(loader.resources["fishTexture"].texture!)
    pixi.stage.addChild(fish)
}
```
<br>
<br>
<br>


# Opdracht 

[Maak het pixel aquarium](./week1-pixi.md)

<br>
<br>
<br>

# Links

- [📺 Installatie instructies filmpje](https://youtu.be/uuPprdiFKXI)
- [PixiJS Examples](https://pixijs.io/examples/) en [Getting started](https://pixijs.io/guides/basics/getting-started.html)
- [NodeJS](https://nodejs.org/en/) en [Visual Studio Code](https://code.visualstudio.com)