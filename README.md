let level = 0
let yLevel = 0
let randomColor
class LevelIndicator {
  constructor(x, y, w, h, fillColor) {
    this.x = x;
    this.y = y;
    this.w = w;
    this.h = h;
    this.fillColor = fillColor
  }
}
const colorLevel = {}
const gameState = {}
const config = {
  width: 400,
  height: 400,
  backgroundColor: 0xdda0dd,
  scene: {
    preload,
    create,
    update
    }
}
function preload() {
  this.load.image('codey', 'https://content.codecademy.com/courses/learn-phaser/codey.png')
}
function create() {

  gameState.circle1 = this.add.circle(100, 100, 50, 0x00ff00)
  gameState.codey = this.add.sprite(200, 200, 'codey')
  gameState.cursors = this.input.keyboard.createCursorKeys()
}
function update() {
  
  if (gameState.cursors.up.isDown) {
    gameState.codey.y -= 5
  }
  if (gameState.cursors.down.isDown) {
    gameState.codey.y += 5
  }
  if (gameState.cursors.right.isDown) {
    gameState.codey.x += 5
  }
  if (gameState.cursors.left.isDown) {
    gameState.codey.x -= 5
  }
  if (Math.sqrt(Math.pow(((gameState.codey.x) - (gameState.circle1.x)), 2) + Math.pow(((gameState.codey.y) - (gameState.circle1.y)), 2)) <= (gameState.circle1.radius) + 25) {
    gameState.circle1.radius -= 1
  }
  if (gameState.circle1.radius <= 6) {
    gameState.circle1.x = Math.random() * 400
    gameState.circle1.y = Math.random() * 400
    gameState.circle1.radius = 50
    randomColor = Math.floor(Math.random()*16777217).toString(16)
    randomColor = randomColor.slice(0, 7)
    randomColor = '0x' + randomColor
    gameState.circle1.fillColor = randomColor
    if ((level * 5) >= 395) {
      yLevel ++
      level = 0
    }
    this.add.rectangle(((level * 5) + 5), ((yLevel * 5) + 5), 5, 5, (randomColor))
    level ++
  }
}
const game = new Phaser.Game(config)
