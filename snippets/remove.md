# Objecten spawnen

Als je sprites wil kunnen spawnen (en later verwijderen) uit de game begin je met het maken van een array die bijhoudt welke sprites er zijn. Nieuwe sprites plaats je in de array én op de pixi stage.

```typescript
class Game {
    fishes:Fish[] = []
    spawnFish(){
        let fish = new Fish(texture)
        this.fishes.push(fish)
        this.pixi.stage.addChild(fish)
    }
    update(){
        for(let fish of this.fishes) {
            fish.update()
        }
    }
}
```
Als je de `spawnFish` functie elke 2 seconden wil aanroepen, kan je dat doen met een [timer](./timer.md)

```typescript
class Game {
    fishes:Fish[] = []
    fishTimer:number = 0
    update(delta:number){
        for(let fish of this.fishes) {
            fish.update()
        }

        fishTimer += delta
        if(fishTimer > 60) {
            this.spawnFish()
            this.fishTimer = 0
        }
    }
}
```

<br>
<br>
<br>

# Objecten verwijderen

Als je de `Fish` wil verwijderen, moet je de sprite van de `pixi.stage` verwijderen én uit de array halen. Dat kan je bijvoorbeeld doen met `filter`. 

```typescript
class Game {
    removeFishFromGame(fish:Fish) {
        // verwijder uit array
        this.fishes = this.fishes.filter(f => f != fish)
        // verwijder uit pixi
        fish.destroy()
    }
}
```


<br>
<br>
<br>

# Object pool

Een veel gebruikte techniek om objecten te hergebruiken is de `object pool`. Denk hierbij aan fishes die zodra ze links uit beeld zwemmen, een nieuwe kleur en positie krijgen, en daarna weer vanuit rechts in beeld komen:

```typescript
class Fish extends PIXI.Sprite {
    update(){
        this.x--
        if(this.x < 0) {
            this.x = 1000
            this.y = Math.random() * 800
        }
    }
}
```

Als de Fish echt moet verdwijnen kan je het object ook tijdelijk inactief maken. Zet dan de sprite op `invisible`.

```typescript
class Fish extends PIXI.Sprite {
    update() {
        this.x++
    }
    killedByShark() {
        this.visible = false
    }
}
```
Let op dat je de `update` van de Fish nu niet meer moet aanroepen in `Game`. Ook moet je de Fish niet meer meenemen in de collision detection.

```typescript
class Game {
    fishes : Fish[] = []
    //
    // in de update check je alleen de fishes die visible zijn
    //
    update(delta:number){
        for(let fish of this.fishes) {
            if(fish.visible) {
                fish.update()
                this.checkCollision(fish, this.shark)
            }
        }
    }
}
```
<br>
<br>
<br>