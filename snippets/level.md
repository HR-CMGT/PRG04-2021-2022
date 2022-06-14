# Levels

Bij sommige games wil je levels hebben die steeds iets moeilijker worden, of er iets anders uit zien.

In dit code voorbeeld voegen we code toe om de game te resetten met een verschillend aantal vijanden en een andere achtergrond.

<br>
<br>
<br>

## Container

Om te beginnen is het handig om al je game elementen die bij een level horen in een `PIXI.Container` te zetten. Je plaatst dan je sprites in die container in plaats van in de `pixi.stage`. 

Maak een aparte functie die het level bouwt. Die functie kunnen we dan vaker aanroepen.

```typescript
class Game {

    container : PIXI.Container
    player : Player
    enemies : Enemy[] = []

    doneLoading() {
        this.container = new PIXI.Container()
        this.pixi.stage.addChild(this.container)
        this.buildLevel()
    }

    buildLevel() {
        this.background = new PIXI.Sprite(this.loader.resources["water"].texture!)
        this.container.addChild(this.background)

        this.player = new Player()
        this.container.addChild(this.player)

        // voeg 5 vijanden toe
        for(let i = 0; i < 5; i++) {
            let enemy = new Enemy()
            this.container.addChild(enemy)
            this.enemies.push(enemy)
        }
    }
}
```

<Br>
<Br>
<br>

## Moeilijkheidsgraad doorgeven

Nu je een `buildLevel` functie hebt, kan je daaraan een moeilijkheidsgraad doorgeven, bijvoorbeeld om het aantal vijanden te bepalen. Je zou ook de achtergrondafbeelding kunnen doorgeven.

```typescript
class Game {
    buildLevel(amountEnemies:number, bg:PIXI.Texture) {
        this.background = new PIXI.Sprite(bg)
        this.container.addChild(this.background)

        for(let i = 0; i < amountEnemies; i++) {
            let enemy = new Enemy()
            this.container.addChild(enemy)
            this.enemies.push(enemy)
        }
    }
}
```

<Br>
<Br>
<br>

## Nieuw level starten

We stoppen eerst de pixi ticker met `pixi.stop()`. Daarna maken we met `removeChildren()` de container in één keer leeg. 

⚠️ Let op dat je eventuele arrays waar je sprites in staan ook leeg maakt. Properties zoals `this.player` of `this.background` kan je hier ook leeg maken, maar die worden sowieso overschreven als je een nieuw level aanmaakt.

Daarna roepen we de `buildLevel` functie opnieuw aan met andere waarden. In dit geval maken we een level met meer vijanden en een andere achtergrond.



```typescript
class Game {

    resetLevel() {
        this.pixi.stop()
        this.container.removeChildren()
        this.enemies = []

        this.buildLevel(25, this.loader.resources["space"].texture!)
        this.pixi.start()
    }
}
```

Als je player `window.addEventListener` gebruikt, moet je die listener verwijderen als je de player verwijdert. 

Een simpeler oplossing is om de speler niet in de container te zetten. In een nieuw level hoef je dan de speler niet opnieuw aan te maken!

