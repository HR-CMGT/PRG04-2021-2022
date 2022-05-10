# Encapsulation

Encapsulation betekent het afschermen van je variabelen en functies binnen een class. Het keyword `private` betekent dat alleen de class zelf bij deze variabelen en functies kan gebruiken. `public` betekent dat andere classes hier ook bij kunnen.

```typescript
class Car {
    private speed = 10

    public drive() {
        console.log("vroooom")
    }
}

let c = new Car()
c.speed = 12 // NOT ALLOWED - SPEED IS PRIVATE
c.drive()    // ALLOWED - DRIVE IS PUBLIC
```

<br>
<br>
<br>

## Opdracht 

Pas encapsulation toe in de code die je tot nu toe geschreven hebt. Maak je variabelen en functies bij voorkeur `private`, tenzij je echt zeker weet dat het `public` moet zijn.

<br>
<br>
<br>


## Opdracht : keyboard controls

Maak een sprite bestuurbaar met het toetsenbord. [Lees daarvoor deze code snippet!](../snippets/keyboard.md)

<br>
<br>
<br>

## Opdracht : collision detection

Controleer of twee sprites elkaar raken. [Lees daarvoor deze code snippet!](../snippets/collision.md)

<br>
<br>
<br>