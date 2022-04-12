# Keyboard controls

Gebruik `window.addEventListener("keydown")` om te reageren op keyboard events in het window.

We maken variabelen aan voor de X snelheid en de Y snelheid. De X,Y snelheid kan omhoog gaan als er toetsen worden ingedrukt.

De snelheid wordt weer 0 als de toets wordt losgelaten.

<br>

```typescript
import * as PIXI from "pixi.js"

export class Ship extends PIXI.Sprite {
    xspeed = 0
    yspeed = 0

    constructor(texture: PIXI.Texture) {
        super(texture)

        window.addEventListener("keydown", (e: KeyboardEvent) => this.onKeyDown(e))
        window.addEventListener("keyup", (e: KeyboardEvent) => this.onKeyUp(e))
    }
    
    update() {
        this.x += this.xspeed
        this.y += this.yspeed
    }

    shoot(){
        console.log("shooooot!")
    }

    onKeyDown(e: KeyboardEvent): void {
        switch (e.key.toUpperCase()) {
            case " ":
                this.shoot()
                break;
            case "A":
            case "ARROWLEFT":
                this.xspeed = -7
                break
            case "D":
            case "ARROWRIGHT":
                this.xspeed = 7
                break
            case "W":
            case "ARROWUP":
                this.yspeed = -7
                break
            case "S":
            case "ARROWDOWN":
                this.yspeed = 7
                break
        }
    }

    private onKeyUp(e: KeyboardEvent): void {
        switch (e.key.toUpperCase()) {
            case " ":
                break;
            case "A":
            case "D":
            case "ARROWLEFT":
            case "ARROWRIGHT":
                this.xspeed = 0
                break
            case "W":
            case "S":
            case "ARROWUP":
            case "ARROWDOWN":
                this.yspeed = 0
                break
        }
    }
}

```
<br>
<br>
<Br>

## Stoppen met keyboard events

Als het schip niet meer hoeft te reageren op key events dan kan je de listeners verwijderen.

```typescript
window.removeEventListener("keydown", (e: KeyboardEvent) => this.onKeyDown(e))
window.removeEventListener("keyup", (e: KeyboardEvent) => this.onKeyUp(e))
```