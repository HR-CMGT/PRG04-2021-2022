# Collision

Om te testen of twee sprites (rechthoeken) elkaar overlappen kan je de `getBounds()` functie van een sprite gebruiken. 

![rectangles](./rectangles.png)

In dit geval zijn er twee sprites, `blockOne` en `blockTwo`.

```typescript
export class Game {

    player:PIXI.Sprite
    enemy:PIXI.Sprite

    doneLoading(){
        this.player = new PIXI.Sprite(texture)
        this.enemy = new PIXI.Sprite(texture)
    }

    update(delta:number) {
        this.player.update()
        this.enemy.update()

        if(this.collision(this.player, this.enemy)){
            console.log("player touches enemy 💀")
        }
    }

    collision(sprite1:PIXI.Sprite, sprite2:PIXI.Sprite) {
        const bounds1 = sprite1.getBounds()
        const bounds2 = sprite2.getBounds()

        return bounds1.x < bounds2.x + bounds2.width
            && bounds1.x + bounds1.width > bounds2.x
            && bounds1.y < bounds2.y + bounds2.height
            && bounds1.y + bounds1.height > bounds2.y;
    }
}

```
> ⚠️ Dit voorbeeld toont niet het aanmaken van het pixi canvas of het laden van de textures. Zie daarvoor de [default game class](../week2/week2-pixi-game.md).

<br>
<br>
<Br>

## Punt

Als je alleen wil weten of een bepaald punt binnen een sprite valt kan je dat doen met:

```typescript
let shark = new PIXI.Sprite(texture)
let point = new PIXI.Point(200,300)
let hit = shark.containsPoint(point)
```

<br>
<Br>
<br>

## Hitbox

[Lees meer over collisions in de **hitbox** tutorial!](./hitbox.md)



<br>
<br>
<br>

## Links

- [MDN Tutorial 2D Collision Detection](https://developer.mozilla.org/en-US/docs/Games/Techniques/2D_collision_detection)
- [getBounds API](https://pixijs.download/dev/docs/PIXI.Sprite.html#getBounds) en [containsPoint API](https://pixijs.download/dev/docs/PIXI.Sprite.html#containsPoint)
- [Using Physics for Collision Detection](https://brm.io/matter-js/) en [Voorbeeld Project](https://github.com/KokoDoko/piximatters)