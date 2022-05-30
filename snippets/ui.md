# UI Class

Een User Interface laag bestaat uit tekstvelden, score weergave, health bars, etc. Het is handig om al deze elementen in een `PIXI.Container` te zetten. Deze container voeg je dan toe in je `Game.ts`.

```typescript
class Game {
    interface : UI

    doneLoading() {
        this.interface = new UI()
        this.pixi.stage.addChild(this.interface)
    }
}
```

<br>
<br>
<br>

## Interface

Omdat de `UI` class een `Container` is, kan je via `this.addChild()` elementen toevoegen. In dit voorbeeld worden twee tekstvelden gebouwd.

```typescript
export class UI extends PIXI.Container {

    scoreField:PIXI.Text
    nameField:PIXI.Text

    constructor(){
        const style = new PIXI.TextStyle({
            fontFamily: 'ArcadeFont',
            fontSize: 40,
            fontWeight: 'bold',
            fill: ['#ffffff']
        })
    
        this.scoreField = new PIXI.Text(`Score : 0`, style)
        this.addChild(this.scoreField)
        this.scoreField.x = 10
        this.scoreField.y = 10

        this.nameField = new PIXI.Text(`Bob`, style)
        this.addChild(this.nameField)
        this.nameField.x = 10
        this.nameField.y = 10
    }
}
```

<br>
<br>
<br>

## Voorbeeld: score tonen in UI

Hieronder een voorbeeld waarin de game een score doorgeeft aan de UI.

*GAME.ts*


```typescript
export class Game {
    interface : UI

    doneLoading() {
        this.interface = new UI()
        this.pixi.stage.addChild(this.interface)
    }

    //
    // na collision check : de player raakt een vijand
    //
    playerHitsEnemy() {
        this.interface.addScore(1)
    }
}
```
*UI.ts*

```typescript
export class UI {
    scoreField:PIXI.Text
    score:number = 0

    // voeg een getal toe aan de score
    addScore(n:number) {
        this.score += n
        this.scoreField.text = `Score : ${this.score}`
    }
}
```