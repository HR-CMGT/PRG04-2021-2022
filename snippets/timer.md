# Timer

In de game class hebben we een game loop gemaakt met `ticker.add(()=>this.update())`. Die wordt **60x per seconde** aangeroepen. Deze game loop kan je pauzeren met `pixi.stop()` en `pixi.start()`. De game loop stopt ook als je browser tab geen focus heeft.

<Br>
<Br>
<br>

## Waarom geen setInterval

Je kan met `setInterval` en `setTimeout` code uitvoeren na een x aantal seconden. Die timers wachten echter niet automatisch als de browsertab geen focus heeft, en ook niet als je `pixi.stop()` hebt aangeroepen. Daarom is het beter om al je time-based functies met een *counter* op te lossen:

<br>
<Br>

## Spawn enemies

In dit voorbeeld spawnen we elke 2 seconden een nieuwe vijand.

```typescript
import { Enemy } from "./enemy"

class Game {

    spawnCounter:number = 0
    enemies:Enemy[] = []

    update(delta:number){
        this.spawnCounter+=delta
        if(this.spawnCounter > 120) {
            this.spawnCounter = 0
            this.enemies.push(new Enemy())
        }
    }
}
```
<br>
<br>
<br>

## Countdown clock

In dit voorbeeld telt een teller langzaam af

```typescript
class Game {

    doomClock:number = 3600 

    update(delta:number){
        this.doomClock-=delta
        let secondsLeft = Math.floor(doomClock / 60)
        if(this.doomClock <= 0) {
            console.log("Doomsday has come!")
        } else {
            console.log(`Only ${secondsLeft} seconds left!`)
        }
    }
}
```
