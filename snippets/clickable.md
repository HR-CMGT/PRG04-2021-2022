# Clickable sprite

Maak een sprite interactief. Dit kan je simpelweg doen met:

```typescript
export class Fish extends PIXI.Sprite {
   
    constructor(texture: PIXI.Texture) {
        super(texture)
        this.x = 400
        this.y = 200
        this.interactive = true  // make clickable
        this.buttonMode = true   // show hand cursor
        this.on('pointerdown', () => this.onClick())
    }

    onClick() {
        console.log("je klikt op een vis")
    }
}
```
<br>
<br>
<br>

## HitArea

De [hitArea](https://pixijs.download/dev/docs/PIXI.Sprite.html#hitArea) van een sprite kan je gebruiken om de hitbox voor ***mouse interaction*** aan te passen.

```typescript
this.hitArea = new PIXI.Rectangle(0,0,200,100)
```

Als een sprite geen `hitArea` heeft, dan wordt `getBounds()` gebruikt om te zien of de muis de sprite raakt. Je kan de `hitArea` een custom shape geven met [deze plugin](https://www.npmjs.com/package/hitarea-shapes). 

<br>
<br>
<br>

## Click handler verwijderen

Als je de click handler ook weer wil kunnen verwijderen moet je een aparte variabele aanmaken van het type `EventListener`:

```typescript
export class Fish extends PIXI.Sprite {

    clickHandler : EventListener
    
    constructor(texture: PIXI.Texture) {
        super(texture)
        this.x = 400
        this.y = 200
        this.interactive = true
        this.clickHandler = () => this.onClick()
        this.on('pointerdown', this.clickHandler)
    }

    onClick() {
        console.log("je klikt op een vis")
        this.off('pointerdown', this.clickHandler)
    }
}
```