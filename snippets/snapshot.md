Wil je een screenshot maken van je canvas, dan kan dat met de PIXI.Extract class.

```typescript
 takeScreenshot() {
    let renderer: PIXI.Renderer = this.pixi.renderer as PIXI.Renderer
    let extract = new PIXI.Extract(renderer)
    
    let base64String = extract.base64(this.pixi.stage)
    
    console.log(base64String)
    // deze log laat een lange string zien van tekens. 
    // Deze tekens samen zijn om te zetten naar een plaatje
    
    // Van deze string is een Sprite te maken
    let sprite = PIXI.Sprite.from(base64String)
    sprite.x = 100
    sprite.y = 100
    this.pixi.stage.addChild(sprite)
}
```
