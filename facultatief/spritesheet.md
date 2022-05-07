# Spritesheet

Een spritesheet is een enkele afbeelding waarin alle frames van een animatie zitten. 

![sheet](./sheet-example.png)

Om spritesheets in te lezen gebruik je een **JSON** file waarin staat welke *bronafbeelding* je gebruikt en waar de *frames* zich precies bevinden in die afbeelding.

```json
{
    "frames": {
        "Explosion_Sequence_A 1.png": {
            "frame": {
                "x": 244, "y": 1454, "w": 240, "h": 240
            }
        },
        "Explosion_Sequence_A 2.png": {
            "frame": {
                "x": 244, "y": 970, "w": 240, "h": 240
            }
        }
    },
    "meta": {
        "image": "explosion.png",
    }
}
```
Je kan de [Texture Packer](https://www.codeandweb.com/texturepacker) software gebruiken om van je losse afbeeldingen een spritesheet met JSON file te maken.

> *Spritesheets zijn niet alleen handig voor animaties. Je kan het ook gebruiken om alle afbeeldingen uit je game in één enkele PNG file op te slaan. Dit is meer efficiënt qua geheugen van je grafische kaart*.

<br>
<br>
<br>

## Inladen Spritesheet

De [PixiJS Loader](https://pixijs.io/examples/#/sprite/animatedsprite-explosion.js) heeft een speciale functie die herkent dat je een ***spritesheet JSON file*** inlaadt. Je hoeft niet zelf de `PNG` file in te laden. De loader gaat automatisch `textures` uitknippen uit de PNG file.

```typescript
class Game {

    explosionTextures:PIXI.Texture[] = []

    constructor(){
        this.pixi.loader.add("spritesheet", "explosion.json")
        this.pixi.loader.load(() => this.doneLoading())
    }

    doneLoading(){
        // frames opslaan in een array
        for (let i = 0; i < 26; i++) {
            const texture = PIXI.Texture.from(`Explosion_Sequence_A ${i + 1}.png`)
            this.explosionTextures.push(texture)
        }
    }

}      
```
<br>
<br>
<br>

## De animatie tonen

Omdat we de textures in een array hebben opgeslagen, kan je op elk gewenst moment een animatie aanmaken met die textures!

```typescript
class Game {
    createExplosion(){
        const kaboom = new PIXI.AnimatedSprite(this.explosionTextures)
        kaboom.x = 100
        kaboom.y = 100
        kaboom.anchor.set(0.5)
        kaboom.play()
        this.pixi.stage.addChild(kaboom)
    }
}
```

<br>
<br>
<br>

## 💀 Live server

De pixi loader werkt niet samen met het `import` statement voor JSON files. Ook is het niet handig dat je live server steeds een andere bestandsnaam aan je spritesheet geeft. Om dit op te lossen gebruiken we een `static` map in het project. Deze map staat ***buiten*** de `src` map.

![static](./sheet-static.png)

Je kan deze statische bestanden telkens handmatig in je `docs` map zetten als je je game wil publiceren. Hier is echter ook een plugin voor:

```bash
npm install parcel-reporter-static-files-copy -D
```
Om de plugin te activeren maak je een `.parcelrc` bestand, daarin staat:
```json
{
    "extends": [
        "@parcel/config-default"
    ],
    "reporters": [
        "...",
        "parcel-reporter-static-files-copy"
    ]
}
```

<br>
<br>
<br>

## Links

- [PixiJS Explosion Example](https://pixijs.io/examples/#/sprite/animatedsprite-explosion.js)
- [Voorbeeldproject met Object Oriented Explosion en .parcelrc bestand](https://github.com/KokoDoko/pixidust/)
- [Texture Packer](https://www.codeandweb.com/texturepacker)
- [Spritesheet files voor Link en Explosion](./spritesheets/)
- [Static folder copy plugin](https://www.npmjs.com/package/parcel-reporter-static-files-copy)