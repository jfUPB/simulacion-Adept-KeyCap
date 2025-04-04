- Lo primero que tuve que hacer es entender como funcionaban los vectores que integra P5:
  - [Documentación Oficial - p5.Vector](https://p5js.org/search/?term=vector)
 
- Después hubo que tener en cuenta de que básicamente los vectores simplemente almacenan 2 valores dentro de una mismo objeto, por lo cual es provechoso para poder hacer calculos más eficientes de cosas como por ejemplo el ángulo, donde en mi implementación uso la función integrada ``` fromAngle(angle ``` para poder encontrar de una manera más secilla la direcciónd de la siguiente posición sin tener que hacer claçulso con **Sen y Cos**.

### Código

```js


let walker;

function setup() {
  createCanvas(640, 240);
  walker = new Walker();
  background(255);
}

function draw() {
  walker.step();
  walker.show();
}

// Function to generate a random number with a Lévy distribution
function levy(mu = 1.5) {
  let u = Math.random();
  let v = Math.random();
  return Math.pow(u, -1 / mu) * Math.sin(2 * Math.PI * v);
}

// Function to perform a Lévy flight
function levyFlight(mu = 1.5) {
  let stepLength = levy(mu);
  let angle = Math.random() * TWO_PI;
  let step = p5.Vector.fromAngle(angle).mult(stepLength);
  return step;
}

class Walker {
  constructor() {
    this.position = createVector(width / 2, height / 2);
    this.prevPosition = this.position.copy();
  }

  show() {
    stroke(0);
    line(this.prevPosition.x, this.prevPosition.y, this.position.x, this.position.y);
  }

  step() {
    let step = levyFlight();

    this.prevPosition.set(this.position);

    this.position.add(step);

    // If goes out of bounds, resets position
    if (this.position.x > width || this.position.x < 0 || 
        this.position.y > height || this.position.y < 0) {
      this.position.set(width / 2, height / 2);
    }
  }
}


  ```
