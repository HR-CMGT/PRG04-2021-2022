# Top down view

![topdown](./topdown.gif)

Voor een top-down game wil je vaak rond kunnen lopen door een map. De meeste game engines doen dit door een camera te bevestigen aan de player. In Pixi kan je dit effect bereiken door het middelpunt van de `pixi.stage` gelijk te maken aan de speler. *Zorg dat je map veel groter is dan het scherm dat de speler ziet*. 

[Codesandbox Voorbeeld](https://codesandbox.io/s/map-explorer-on4g4t)

<br>
<br>
<br>

GAME.TS
```typescript
class Game {

    player:Player

    doneLoading(){
        let background = new PIXI.Sprite(texture)
        this.pixi.stage.addChild(background)
        
        this.player = new Player(this, texture)
        this.pixi.stage.addChild(this.player)

        // start positie van de stage
        this.pixi.stage.x = this.pixi.screen.width / 2
        this.pixi.stage.y = this.pixi.screen.height / 2
    }
}
```

Je gebruikt nog steeds de [keyboard controls](./keyboard.md) om de player te bewegen. In dit voorbeeld gebruiken we `clamp` om te zorgen dat de speler niet buiten de map kan lopen.

PLAYER.TS

```typescript
class Player {
    update(){
        this.x = this.clamp(this.x + this.xspeed, 0, 1800)  // map width
        this.y = this.clamp(this.y + this.yspeed, 0, 1300)  // map height
    }
    clamp(num: number, min: number, max: number) {
        return Math.min(Math.max(num, min), max)
    }
}
```

Echter, je plaatst nu ook het middelpunt van de `pixi stage` telkens onder de player. Daardoor lijkt de player stil te staan en de kaart te bewegen.

```typescript
class Player {
    update(){
        // plaats nu ook de map onder de speler !
        this.game.pixi.stage.pivot.set(this.x, this.y)
    }
}

```
Het is nog mooier als je de map ***niet*** onder de speler centreert als de speler bij de rand komt. *De kaart kan dan nooit buiten beeld scrollen, én de speler kan nog wel naar de hoeken lopen*. Zie daarvoor het complete code voorbeeld hieronder.

<br>
<br>
<br>

## Compleet code voorbeeld

PLAYER.TS
```typescript
export class Player extends PIXI.Sprite {

    xspeed = 0
    yspeed = 0
    game:Game

    constructor(game:Game, texture: PIXI.Texture) {
        super(texture)
        this.game = game
        this.anchor.set(0.5)
        this.x = game.pixi.screen.width/2
        this.y = game.pixi.screen.height/2

        window.addEventListener("keydown", (e: KeyboardEvent) => this.onKeyDown(e))
        window.addEventListener("keyup", (e: KeyboardEvent) => this.onKeyUp(e))
    }

    update(delta: number) {
        let mapwidth = 1800
        let mapheight = 1300
        let centerx = 350
        let centery = 250

        // beweeg het karakter over de map. clamp zorgt dat je niet buiten de map kan lopen
        this.x = this.clamp(this.x + this.xspeed, 0, mapwidth)
        this.y = this.clamp(this.y + this.yspeed, 0, mapheight)

        // centreer het hele level onder het karakter behalve aan de randen
        let mapx = this.clamp(this.x, centerx, mapwidth - centerx)
        let mapy = this.clamp(this.y, centery, mapheight - centery)
        this.game.pixi.stage.pivot.set(mapx, mapy)        
    }

    clamp(num: number, min: number, max: number) {
        return Math.min(Math.max(num, min), max)
    }
}
```

<br>
<br>
<br>

## Links

- [Codesandbox Voorbeeld](https://codesandbox.io/s/map-explorer-on4g4t)
- [Keyboard controls](./keyboard.md)