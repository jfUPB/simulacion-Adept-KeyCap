### [Enlace de la simulación](https://editor.p5js.org/Adept-KeyCap/full/IaghAz2XD)
### [Video del resultado](https://youtu.be/0H5wz5uvNLc)

Solamente ```sketch.js``` fue modificado para esta actividad 

**Sketch.js**
```js

// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

let value = 2;

// Mover object
let bob = [];

// Spring object
let spring = [];

function setup() {
  createCanvas(640, 400);
  for (let i = 0; i < value; i++) {
    if (i == 0) {
      spring[i] = new Spring(width / 2, 10, 100);
      bob[i] = new Bob(width / 2, 100);
    } else {
      spring[i] = new Spring(bob[i - 1].position.x, bob[i - 1].position.y, 100);
      bob[i] = new Bob(bob[i - 1].position.x, bob[i - 1].position.y + 100);
    }
  }
}


function draw() {
  background(255);
  let gravity = createVector(0, 2);

  for (let i = 0; i < value; i++) {
    if (i > 0) {  // El segundo resorte se ancla al primer bob
      spring[i].anchor = bob[i - 1].position.copy();
    }

    bob[i].applyForce(gravity);
    bob[i].update();
    bob[i].handleDrag(mouseX, mouseY);

    spring[i].connect(bob[i]);
    spring[i].constrainLength(bob[i], 30, 200);

    spring[i].showLine(bob[i]);
    bob[i].show();
    spring[i].show();
  }
}

function mousePressed() {
  bob[0].handleClick(mouseX, mouseY);
  bob[1].handleClick(mouseX, mouseY);
}

function mouseReleased() {
  bob[0].stopDragging();
  bob[1].stopDragging();
}


```
