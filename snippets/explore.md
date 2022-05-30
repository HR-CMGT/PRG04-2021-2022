# Exploring a map

Voor een top-down game wil je vaak rond kunnen lopen door een afbeelding. Dit doe je door de afbeelding te verplaatsen in plaats van de sprite. Dit kan je doen door aan de player de achtergrond door te geven.

GAME.TS
```typescript
class Game {
    background:PIXI.Sprite
    player:Player
    doneLoading(){
        this.background = new PIXI.Sprite(texture)
        this.player = new Player(texture, this.background)
    }
}
```
Gebruik de [keyboard controls](./keyboard.md) om de achtergrond te bewegen. Zorg wel dat je achtergrond veel groter is dan de stage. 

PLAYER.TS
```typescript
export class Player extends PIXI.Sprite {

    xspeed = 0
    yspeed = 0
    background: PIXI.Sprite

    constructor(texture: PIXI.Texture, background: PIXI.Sprite) {
        super(texture)

        this.anchor.set(0.5)
        this.x = 350
        this.y = 250

        // achtergrond
        this.background = background
        
        // zie de keyboard snippet voor de complete movement code
        window.addEventListener("keydown", (e: KeyboardEvent) => this.onKeyDown(e))
        window.addEventListener("keyup", (e: KeyboardEvent) => this.onKeyUp(e))
    }

    //
    // verplaats de achtergrond 
    //
    update(delta: number) {
        this.background.x -= this.xspeed
        this.background.y -= this.yspeed
    }
}
```
<br>
<br>
<br>

## Eindeloos lopen

Als je de achtergrond verandert in een [Tiling Sprite](./scrolling.md) dan kan je eindeloos in alle richtingen door blijven lopen. Let op dat je hierbij de `tile x,y` van de sprite aanpast in plaats van de sprite als geheel.

GAME.TS
```typescript
class Game {
    doneLoading() {
        this.background = new PIXI.TilingSprite(texture, 1440, 900)
        this.pixi.stage.addChild(this.background)
    }
}
```
PLAYER.TS
```typescript
class Player {
    update(delta: number) {
        this.background.tilePosition.x -= this.xspeed
        this.background.tilePosition.y -= this.yspeed
    }
}
```


<br>
<br>
<br>

## Camera effect 🤯

Als je *géén* eindeloos herhalende achtergrond hebt, dan moet de achtergrond stoppen met scrollen als de afbeelding ophoudt. Dat kan je bereiken met de `clamp` functie.

```typescript
export class Player extends PIXI.Sprite {

    xspeed = 0
    yspeed = 0
    background: PIXI.Sprite
    box:Rectangle

    constructor(background: PIXI.Sprite, texture: PIXI.Texture) {
        super(texture)
        this.anchor.set(0.5)
        this.x = 350
        this.y = 250
        this.background = background
    }    
    //
    // verplaats de achtergrond tot aan de rand
    //
    update(delta: number) {
        const stagewidth = 700
        const stageheight = 500
        const mapwidth = 1400
        const mapheight = 900

        this.background.x = this.clamp(this.background.x - this.xspeed, stagewidth-mapwidth, 0)    
        this.background.y = this.clamp(this.background.y - this.yspeed, stageheight-mapheight, 0)
    }

    clamp(num:number, min:number, max:number) {
        return Math.min(Math.max(num, min), max)
    }
}
```
Het kan mooi zijn als je figuurtje nog wel naar de rand toe kan lopen als de afbeelding stopt met scrollen! [Zie dit codesandbox voorbeeld](https://codesandbox.io/s/map-explorer-on4g4t). 


<br>
<br>
<br>

## Links

- [Keyboard controls](./keyboard.md)
- [Tiling Sprite](https://pixijs.io/examples/#/sprite/tiling-sprite.js)
- [Codesandbox voorbeeld camera effect](https://codesandbox.io/s/map-explorer-on4g4t)