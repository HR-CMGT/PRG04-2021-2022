# Vector Math

Vector Math helpt je om makkelijker te werken met hoeken en richtingen waarin je sprites moeten bewegen. Een Vector is een object met een **x en y** waarde, in **PixiJS** is dat een `PIXI.Point`.

Om met vector math te werken moet je Pixi Math installeren:

```bash
npm install @pixi/math
npm install @pixi/math-extras
```

Nu kan je een Point aanmaken:

```typescript
import '@pixi/math-extras'

let fishPosition = new PIXI.Point(100,200)
```
> ⚠️ je kan het keyword `position` niet gebruiken omdat dit gereserveerd is voor PixiJS.

<br>
<br>
<br>

## Snelheid optellen bij positie

Door de positie en de snelheid als vector op te slaan, kan je makkelijk in alle richtingen bewegen.

```typescript
import { Game } from "./Game"
import * as PIXI from "pixi.js"
import '@pixi/math-extras'

export class EvilFish extends PIXI.Sprite {

    swimSpeed:PIXI.Point
    swimPosition:PIXI.Point

    constructor(texture:PIXI.Texture) {
        super(texture)
        this.swimSpeed = new PIXI.Point(-1, -1)
        this.swimPosition = new PIXI.Point(800,400)
    }

    update(delta: number) {
        // tel de snelheid op bij de positie
        this.swimPosition = this.swimPosition.add(this.swimSpeed)

        // draw
        this.x = this.swimPosition.x
        this.y = this.swimPosition.y
    }

}
```

<br>
<br>
<br>

## Afstand tussen twee punten

Het verschil tussen twee `x,y` punten kan je opvragen met `subtract()`. Dit is ook weer een punt met een `x,y` waarde.

```typescript
const difference = this.swimTarget.subtract(this.swimPosition)
```
Via *magnitude* kan je de daadwerkelijke afstand in pixels tussen twee punten opvragen:

```typescript
const distance = this.swimTarget.subtract(this.swimPosition).magnitude()
```

<br>
<br>
<br>

## Richting bepalen

Als je weet naar welk punt je toe wil bewegen, dan kan je met `normalize()` dat `x,y` doel vertalen naar een `x,y` richting. Dit geeft altijd `x,y` waarden tussen `0` en `1`. Met deze snelheid beweeg je elk frame een klein stukje naar het doel. 

In dit voorbeeld bewegen we langzaam richting de muispointer.

```typescript
export class EvilFish extends PIXI.Sprite {

    swimSpeed:PIXI.Point
    swimPosition:PIXI.Point

    constructor(texture) {
        super(texture)
        this.anchor.set(0.5)   
        this.swimSpeed = new PIXI.Point(-1, -1)
        this.swimPosition = new PIXI.Point(800,400)
    }


    update(delta: number) {
        const mouseposition : PIXI.Point = this.game.pixi.renderer.plugins.interaction.mouse.global
        const newDirection = mouseposition.subtract(this.swimPosition).normalize()

        this.swimPosition = this.swimPosition.add(newDirection)

        this.x = this.swimPosition.x
        this.y = this.swimPosition.y 
    }
}
```
Als je wat sneller wil gaan kan je de `normalized direction` weer vermenigvulden met een `speed`:

```typescript
const newSpeed = newDirection.multiplyScalar(3)
this.swimPosition = this.swimPosition.add(newSpeed)
```

<br>
<br>
<br>

## Naar het doel draaien

Om de sprite naar het doel te laten kijken hebben we een `rotation angle` nodig.

```typescript
this.angle = Math.atan2(newDirection.y, newDirection.x) * 180 / Math.PI
```

<br>
<br>
<br>

## Links

- [Point API](https://pixijs.download/release/docs/PIXI.Point.html)
- [Math plugin](https://api.pixijs.io/@pixi/math.html) en [extras](https://www.runpkg.com/?@pixi/math-extras@6.3.0/README.md)
- [Code voorbeeld voor Vector Movement](https://github.com/KokoDoko/VectorTanks)

<BR>
<BR>
<BR>
<BR>
<BR>

# OLDOLDOLD

## Punten vergelijken

Een vector heeft een aantal ingebouwde 'convenience methods'.

```typescript
let v1 = new Vector2(20,35)
let v2 = new Vector2(100,120)

// optellen
v1 = v1.add(v2)

// verschil tussen twee vectoren
let diff = v1.difference(v2)

// de lengte van deze vector
let v3 = new Vector2(100,100)
let distance = v3.magnitude()    // resultaat 141.42135
```

### Voorbeeld
```typescript
let position = new Vector2(200,300)
let speed = new Vector2(4,3)

// game loop
position = position.add(speed)
```





<br>
<br>
<br>




# OLD STUFF KAN WEG



## Vector class

```typescript
class Vector2 {
        
    public x : number
    public y : number
    
    constructor(x:number, y:number) {
        this.x = x
        this.y = y
    }

    // todo: methods static maken, nu worden ze telkens mee gekopieerd
    
    public add(v: Vector2): Vector2 {
        return new Vector2(this.x + v.x, this.y + v.y)
    }

    public difference(v: Vector2): Vector2 {
        return new Vector2(this.x - v.x, this.y - v.y)
    }

    public scale(n: number): Vector2 {
        return new Vector2(this.x * n, this.y * n)
    }

    public magnitude(): number {
        return Math.sqrt(this.x * this.x + this.y * this.y)
    }
    
    // x en y delen door de lengte (magnitude) geeft normalized
    public normalize():Vector2 {
        let mag = this.magnitude()
        return new Vector2(this.x/mag, this.y/mag)
    }

    public static reflectX(point: Vector2, x: number) {
        return new Vector2(2 * x - point.x, point.y)
    }

    public static reflectY(point: Vector2, y: number) {
        return new Vector2(point.x, 2 * y - point.y)
    }
}
```


