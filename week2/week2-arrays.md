# Arrays

Als je een groot aantal `instances` nodig hebt, is het niet handig om voor elke `instance` een property aan te maken:

```typescript
import { Bunny } from "./Bunny"

export class Game {

    private bunnyOne: Bunny
    private bunnyTwo: Bunny
    private bunnyThree: Bunny

    constructor() {
        this.bunnyOne = new Bunny(this)
        this.bunnyTwo = new Bunny(this)
        this.bunnyThree = new Bunny(this)
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

We kunnen ook een enkele property aanmaken waarin alle Bunnies komen te staan. Dit is dan een array van het type `Bunny`. Let op dat je ook meteen een lege array aanmaakt.

Met een `for` loop kunnen we hier meerdere bunnies in zettten.

```typescript
import { Bunny } from "./Bunny"

export class Game {

    private bunnies: Bunny[] = []

    constructor() {
        for(let i = 0; i<10; i++){
            this.bunnies.push(new Bunny(this))
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
    private update(delta) {
        for(let bunny of this.bunnies){
            bunny.update(delta)
        }
    }
}
```

<Br>
<br>
<br>

## Opdracht

![fishes](../week1/opdracht.jpg)

- Zet je fish aquarium code van week 1 om naar Object Oriented code. Maak een `class` aan voor een `Fish`, `Bubble` en een class voor de `Background`. 
- Maak één keer een `new Background()` aan in de `Game`
- Gebruik `arrays` en `for` loops om meerdere vissen en bubbles aan te maken in de `Game` class.
- Geef de `Fish` en `Bubble` classes een `update` functie om te animeren (zie het voorbeeld van de Bunny class).
- Gebruik een `for of` loop om de `update` functie van de vissen en bubbles aan te roepen. 