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

let targetPosition = new PIXI.Point(100,200)
```


<br>
<br>
<br>

## Snelheid als vector

Je kan de `x,y` snelheid van een sprite opslaan als vector:
```typescript
this.fishSpeed = new PIXI.Point(1,-1)
```
Nu kan je elke update de `speed` vector optellen bij de positie! Let op dat we hier de `position` property van een sprite gebruiken om de `x,y` positie te bepalen.

```typescript
export class EvilFish extends PIXI.Sprite {

    swimSpeed : PIXI.Point

    constructor(texture:PIXI.Texture) {
        super(texture)
        this.swimSpeed = new PIXI.Point(-1, -1)
        this.position.set(800,400)
    }

    update(delta: number) {
        // tel de snelheid op bij de positie
        this.position = this.position.add(this.swimSpeed) as ObservablePoint  
    }
}
```
> ⚠️ de toevoeging `as ObervablePoint` is een typescript eigenaardigheid 😿 

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

Als je weet naar welk punt je toe wil bewegen, dan kan je met `normalize()` dat `x,y` **doel** vertalen naar een `x,y` **richting**. Dit geeft  waarden tussen `0` en `1`. Met deze snelheid beweeg je elk frame een heel klein beetje naar het doel. 

In dit voorbeeld bewegen we langzaam richting de muispointer.

```typescript
export class EvilFish extends PIXI.Sprite {

    swimSpeed:PIXI.Point

    constructor(texture) {
        super(texture)
        this.anchor.set(0.5)   
        this.swimSpeed = new PIXI.Point(-1, -1)
        this.position.set(800,400)
    }


    update(delta: number) {
        const mouseposition : PIXI.Point = this.game.pixi.renderer.plugins.interaction.mouse.global
        const direction = mouseposition.subtract(this.position).normalize()

        this.position = this.position.add(direction) as ObservablePoint
    }
}
```
<br>
<br>
<br>

## Speed

Als je wat sneller wil gaan kan je de `normalized direction` (*waarden tussen 0 en 1*) weer vermenigvulden met een `speed`:

```typescript
const speed = 3
const progress = direction.multiplyScalar(speed)
this.position = this.position.add(progress) as ObservablePoint
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
- [Code voorbeeld voor Vector Movement](https://github.com/KokoDoko/VectorTanks)
- [Math plugin](https://api.pixijs.io/@pixi/math.html) en [extras](https://www.runpkg.com/?@pixi/math-extras@6.3.0/README.md)