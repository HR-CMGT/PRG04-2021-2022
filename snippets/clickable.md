# Clickable sprite

Maak een sprite interactief. Dit kan je simpelweg doen met:

```typescript
export class Fish extends PIXI.Sprite {
   
    constructor(texture: PIXI.Texture) {
        super(texture)
        this.x = 400
        this.y = 200
        this.interactive = true
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