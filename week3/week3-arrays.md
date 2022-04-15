# Arrays

Als je een groot aantal `instances` nodig hebt, is het niet handig om voor elke `instance` een property aan te maken:

```typescript
import { Bunny } from "./Bunny"

export class Game {

    bunnyOne: Bunny
    bunnyTwo: Bunny
    bunnyThree: Bunny

    constructor() {
        let texture = loader.resources["bunnyTexture"].texture!
        this.bunnyOne = new Bunny(texture)
        this.bunnyTwo = new Bunny(texture)
        this.bunnyThree = new Bunny(texture)

        this.pixi.stage.addChild(this.bunnyOne)
        this.pixi.stage.addChild(this.bunnyTwo)
        this.pixi.stage.addChild(this.bunnyThree)
    }

    private update(delta) {
        this.bunnyOne.update(delta)
        this.bunnyTwo.update(delta)
        this.bunnyThree.update(delta)
    }
}
```
<br>
<br>
<br>

## For loop en array

We kunnen ook een enkele property aanmaken waarin alle Bunnies komen te staan. Dit is dan een array van het type `Bunny`. Let op dat je ook meteen een lege array aanmaakt : `bunnies: Bunny[] = []`

Met een `for` loop kunnen we hier meerdere bunnies in zetten. Vergeet niet dat je de bunny ook nog aan de `canvas` moet toevoegen. Daarom maken we een tijdelijke variabele met `let`.

```typescript
import { Bunny } from "./Bunny"

export class Game {

    bunnies: Bunny[] = []

    constructor() {
        for(let i = 0; i<10; i++){
            let bunny = new Bunny(loader.resources["bunnyTexture"].texture!)
            this.bunnies.push(bunny)
            this.pixi.stage.addChild(bunny)
        }
    }
}
```
<br>
<br>
<br>

## Animatie

We kunnen door de array heen loopen met een `for of` loop, en dan van elke `instance` de `update()` functie aanroepen.

```typescript
class Game {
    update(delta) {
        for(let bunny of this.bunnies){
            bunny.update(delta)
        }
    }
}
```

<Br>
<br>
<br>

# Opdracht

![fishes](../week1/opdracht.jpg)

- Plaats de Fishes en Bubbles in een array in de Game class.
- Geef alle vissen en bubbles random startposities. 
- Geef alle vissen een random startkleur.
- Gebruik een `for of` loop om de `update` functie van de vissen en bubbles aan te roepen. 
- De vissen bewegen naar links, de bubbles bewegen naar boven. Als ze uit beeld gaan verschijnen ze aan de andere kant weer in beeld.

<Br>
<br>
<br>

# Opdracht

[Maak de `Fishes` clickable](./week3-click.md)