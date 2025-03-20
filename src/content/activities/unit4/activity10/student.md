### [Resultado de la simulación](https://editor.p5js.org/Adept-KeyCap/full/FPU-bO2SS)
### [Video del resultado](https://youtu.be/YJ-qtIHPek8)

```js
let pendulum;
let pendulum2;

function setup() {
  createCanvas(640, 480);
  // Make a new Pendulum with an origin position and armlength
  pendulum = new Pendulum(width / 2, 0, 175);
  pendulum2 = new Pendulum(width / 2, 175, 175);
}

function draw() {
  background(255);
  pendulum.update();
  pendulum.show();

  pendulum.drag(); // for user interaction
  
  pendulum2.update();
  pendulum2.show();
  pendulum2.pivot = pendulum.bob

  pendulum2.drag(); // for user interaction
}

function mousePressed() {
  pendulum.clicked(mouseX, mouseY);
  pendulum2.clicked(mouseX, mouseY);

}

function mouseReleased() {
  pendulum.stopDragging();
  pendulum2.stopDragging();
}

```
