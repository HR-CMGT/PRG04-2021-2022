# Screens en score opslaan

Er zijn meerdere manieren om je pixi game te resetten en een score in een ander scherm te tonen. 

- Game over button met `pixi.stop()`
- HTML pagina met score en link

<br>
<br>
<br>

## Game Over Button

Als je alleen een *game over button* wil tonen, dan kan je `pixi.stop()` gebruiken om het spel te pauzeren. Je toont dan een restart button over je game heen. 

Vervolgens heb je een restart functie nodig die je hele game kan resetten. Denk daarbij aan de positie van de speler, de score, het verwijderen van vijanden, etc. Deze functie roep je aan zodra iemand op de button klikt.

CODE VOORBEELD

```typescript
class Game {

    private gameOverButton : PIXI.Sprite

    private gameOver(){
        console.log("game over")
        this.pixi.stop()
        this.gameOverButton = new PIXI.Sprite(PIXI.Texture.WHITE) // jouw eigen sprite hier
        this.gameOverButton.width = 100
        this.gameOverButton.height = 50
        this.gameOverButton.x = 400
        this.gameOverButton.y = 200
        this.gameOverButton.interactive = true
        this.gameOverButton.buttonMode = true
        this.gameOverButton.on('pointerdown', () => this.resetGame())

        this.pixi.stage.addChild(this.gameOverButton)
    }

    private resetGame(){
        // verwijder de game over button
        this.gameOverButton.destroy() 
        // voorbeeld van het verwijderen van game elementen
        for (let bullet of this.bullets) {
            bullet.destroy()
        }
        this.bullets = []
        // herstart pixi
        this.pixi.start()
    }
}
```
<br>
<br>
<br>

## Score opslaan

Je kan via `localStorage` je score opslaan en in een andere pagina weer inlezen. Ook kan je de score weer inladen als je de game op een ander tijdstip opnieuw speelt.

```typescript
// score opslaan
localStorage.setItem('lastscore', JSON.stringify(this.score))

// score ophalen en tonen in een pixi textfield
let lastScore = localStorage.getItem('lastscore')
// het kan zijn dat er nog nooit een score is opgeslagen
if(lastScore) {
    this.lastScoreField.text = `Last score: ${JSON.parse(lastScore)}`
}
```
<Br>
<br>
<br>

## Score naar PHP sturen

Je kan een PHP pagina maken die via GET of POST een score waarde verwacht. Dan kan je de score opslaan in je database.

```typescript
class Game {
    public saveScore(){
        fetch(`https://mygame.nl/savescore.php?score=${this.score}`)
            .then(res => res.json())
            .then(data => {
                console.log("score is saved to php!")
            })
            .catch(err => {
                console.log("could not save score to php")
            })
    }
}
```


<br>
<br>
<br>

## HTML pagina's gebruiken

Als je meerdere schermen wil gebruiken, bijvoorbeeld voor een ***speluitleg, een highscore overzicht, of een introscherm***, dan is het handig om gewoon met HTML pagina's te werken. Je kan dan nog steeds de score inladen via `localStorage`. 

In dit voorbeeld zie je hoe je vanuit je PIXI game naar een score pagina kan navigeren.

```typescript

import link from "../score.html"

export class Game {
    
    score : number

    public gotoScoreScreen(){
        // score opslaan in local storage of php
        localStorage.setItem('lastscore', JSON.stringify(this.score))
        // navigeer naar het score scherm
        window.location.href = link
    }
}
```

### Score tonen in score.html

Vervolgens kan je in score.html de score via localStorage weer inladen. Je kan met een `<a>` link weer terug gaan naar de game.

```html
<div>HISCORES</div>
<div id="score">loading...</div>
<div>
    <a href="./index.html">REPLAY THE GAME</a>
</div>

<script>
    let score = localStorage.getItem('lastscore')
    document.querySelector("#score").innerText = score
</script>
```