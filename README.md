# Geschenke ausliefern
## ~avatar avatar @unplugged
gedulde dich noch ein wenig bis es soweit ist :-)
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

