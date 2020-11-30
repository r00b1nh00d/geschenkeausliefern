# Geschenke ausliefern
## ~avatar avatar @unplugged
Du bist am Nordpol angekommen der Weihnachtsmann braucht nun deine Hilfe. <br>
Auch der Weihnachtsmann hatte mit den wild gewordenen Elfen viel zu tun und hat jetzt angst die Gechenke nicht rechtzeitig ausliefern zu können.



## ~ @unplugged
Jetzt musst du ihm dabei helfen die Geschenke auszuliefern. <br>
![Geschenkeverteilen](https://github.com/r00b1nh00d/geschenkeausliefern/blob/master/GeschenkeAusliefern.gif?raw=true)

## Schritt 1
Ertelle ``||basic:beim Start||`` einen ``||variable:sprite||`` an der ``||game:Stelle (0,4)||``. <br>
Seine ``||game:Richtung||`` muss nun nach links gedreht werden. <br>

```blocks
let Sprite: game.LedSprite = game.createSprite(4, 0)
Sprite.turn(Direction.Left, 180)
``` 

## Schritt 2
In einer ``||basic:dauerhaft||`` - Schleife soll mittels ``||logic: wenn - dann||`` - Bedinugung zuerst geprüft werden, ob der Sprite gelöscht wurde. <br>
Wurde er gelöscht, soll nochmal mittels ``||logic: wenn - dann||`` - Bedinugung geprüft werden ob sich eine Zufallsvariable erfüllt. Ist diese auch erfüllt soll ein neuer Sprite an der Stelle, mit der selben Ausrichtung wie beim Start erstellt werden. Ist der Sprite ``||logic:nicht||`` ``||game: gelöscht||`` soll geprüft werden, ob der Sprite die Stelle x = 0 erreicht hat. <br>
Ist er an dieser Stelle soll er ``||game: gelöscht||`` werden. <br>
Trifft keine der Beiden Bedingungen zu soll der ``||game:Sprite bewegt||`` werden und der Calliope kurz ``||basic:pausieren||``. <br>
**Jetzt sollte ein Sprite von rechts nach links wandern**
```blocks
let Sprite: game.LedSprite = game.createSprite(4, 0)
Sprite.turn(Direction.Left, 180)

basic.forever(function () {
    if (Sprite.isDeleted()) {
        if (randint(0, 10) == 4) {
            Sprite = game.createSprite(4, 0)
            Sprite.turn(Direction.Left, 180)
        }
    } else if (Sprite.get(LedSpriteProperty.X) == 0) {
        Sprite.delete()
    } else {
        Sprite.move(1)
    }
    basic.pause(200)
})

``` 

## Schritt 3
Erstelle nun einen weitern Sprite namens  ``||variables:Weihnachtsmann||`` . Dieser soll beim Drücken der beiden ``||input:Tasten A und B||`` um 2 Pixel nach oben bewegt werden, nach einer kurzen Pause soll er wieder zurück an die ursprüngliche Position. 
```blocks

input.onButtonPressed(Button.AB, function () {
    Weihnachtsmann.move(2)
    basic.pause(100)
    Weihnachtsmann.move(-2)
})
let Weihnachtsmann: game.LedSprite = null
let Sprite = game.createSprite(4, 0)
Weihnachtsmann = game.createSprite(2, 2)
Sprite.turn(Direction.Left, 180)
basic.forever(function () {
    if (Sprite.isDeleted()) {
        if (randint(0, 10) == 4) {
            Sprite = game.createSprite(4, 0)
            Sprite.turn(Direction.Left, 180)
        }
    } else if (Sprite.get(LedSpriteProperty.X) == 0) {
        Sprite.delete()
    } else {
        Sprite.move(1)
    }
    basic.pause(200)
})

```

## Schritt 4 
Da sich jetzt alle Sprites so bewegen wie sie sollen kannst du nun die Spielregeln Programmieren. Diese kommen ebenfalls in den ``||input: wenn knopf A+B gedrückt||``. Genauer gesagt zwischen die Blöcke in denen sich der Weihnachtsmann nach oben und wieder nach unten bewegen soll. Hier kannst du eine Variable ``||varibales: Runden||`` um eins erhöhen und anschließend gleich testen ob diese den Wert 15 erreicht wodurch das Spiel beendet werden soll. <br>
Ebenso soll geprüft werden, ob der Weihnachtsmann ein Sprite berührt (solang der Sprite noch nicht gelöscht wurde). Ist dies erfüllt soll ein Punkt vergeben werden.


```blocks
input.onButtonPressed(Button.AB, function () {
    Weihnachtsmann.move(2)
    basic.pause(100)
    Runde += 1
    if (Runde == 15) {
        game.gameOver()
    }
    if (!(Sprite.isDeleted()) && Weihnachtsmann.isTouching(Sprite)) {
        game.addScore(1)
    }
    Weihnachtsmann.move(-2)
})
let Runde = 0
let Weihnachtsmann: game.LedSprite = null
let Sprite: game.LedSprite = null
Sprite = game.createSprite(4, 0)
Sprite.turn(Direction.Left, 180)
Weihnachtsmann = game.createSprite(2, 2)
Weihnachtsmann.turn(Direction.Left, 90)
basic.forever(function () {
    if (Sprite.isDeleted()) {
        if (randint(0, 10) == 4) {
            Sprite = game.createSprite(4, 0)
            Sprite.turn(Direction.Left, 180)
        }
    } else if (Sprite.get(LedSpriteProperty.X) == 0) {
        Sprite.delete()
    } else {
        Sprite.move(1)
    }
    basic.pause(200)
})


```


## Schritt 5
Zum Abschluss kannst du alles, was du mit den Sprite Programmiert hast duplizieren und noch für zwei weitere Sprites umschreiben.
```blocks

input.onButtonPressed(Button.AB, function () {
    Weihnachtsmann.move(2)
    Runde += 1
    if (Runde == 15) {
        game.gameOver()
    }
    if (!(Sprite.isDeleted()) && Weihnachtsmann.isTouching(Sprite)) {
        game.addScore(1)
    }
    if (!(Sprite.isDeleted()) && Weihnachtsmann.isTouching(Sprite2)) {
        game.addScore(1)
    }
    if (!(Sprite3.isDeleted()) && Weihnachtsmann.isTouching(Sprite3)) {
        game.addScore(1)
    }
    basic.pause(100)
    Weihnachtsmann.move(-2)
})
let Runde = 0
let Sprite3: game.LedSprite = null
let Sprite2: game.LedSprite = null
let Sprite: game.LedSprite = null
let Weihnachtsmann: game.LedSprite = null
Weihnachtsmann = game.createSprite(2, 2)
Sprite = game.createSprite(4, 0)
Sprite2 = game.createSprite(4, 0)
Sprite3 = game.createSprite(4, 0)
Sprite.turn(Direction.Left, 180)
Sprite2.turn(Direction.Left, 180)
Sprite3.turn(Direction.Left, 180)
Weihnachtsmann.turn(Direction.Left, 90)
basic.forever(function () {
    if (Sprite.isDeleted()) {
        if (randint(0, 10) == 4) {
            Sprite = game.createSprite(4, 0)
            Sprite.turn(Direction.Left, 180)
        }
    } else if (Sprite.get(LedSpriteProperty.X) == 0) {
        Sprite.delete()
    } else {
        Sprite.move(1)
    }
    if (Sprite2.isDeleted()) {
        if (randint(0, 10) == 4) {
            Sprite2 = game.createSprite(4, 0)
            Sprite2.turn(Direction.Left, 180)
        }
    } else if (Sprite2.get(LedSpriteProperty.X) == 0) {
        Sprite2.delete()
    } else {
        Sprite2.move(1)
    }
    if (Sprite3.isDeleted()) {
        if (randint(0, 10) == 4) {
            Sprite3 = game.createSprite(4, 0)
            Sprite3.turn(Direction.Left, 180)
        }
    } else if (Sprite3.get(LedSpriteProperty.X) == 0) {
        Sprite3.delete()
    } else {
        Sprite3.move(1)
    }
    basic.pause(200)
})
```


## ~ @unplugged
Jetzt hast du am oberen Bildschirmrand eine zufällige Abfolge von bis zu 3 Sprites. Dies simuliert eine Häuserreihe an der du vorbeifährst. Wenn du nun Beide Knöpfe drückst bewegt sich der Weihnachtsmann nach oben. Trifft er auf ein Haus gilt das Geschenk als ausgeliefert.
