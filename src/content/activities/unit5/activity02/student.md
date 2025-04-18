## 4.2:
particle.js
```js
class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.acceleration = createVector(0, 0);
    this.velocity = createVector(random(-1, 1), random(-1, 0));
    this.lifespan = 255.0;
  }

  run() {
    let gravity = createVector(0, 0.05);
    this.applyForce(gravity);
    this.update();
    this.show();
  }

  applyForce(force) {
    this.acceleration.add(force);
  }

  // Method to update position
  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.lifespan -= 2;
    this.acceleration.mult(0);
  }

  // Method to display
  show() {
    stroke(0, this.lifespan);
    strokeWeight(2);
    fill(127, this.lifespan);
    circle(this.position.x, this.position.y, 8);
  }

  
  calculateDrag(coefficient) {
        let speed = this.velocity.mag();
        let dragMagnitude = coefficient * speed * speed;
        let dragForce = this.velocity.copy().mult(-1);
        dragForce.setMag(dragMagnitude);
        return dragForce;
  }
  
  // Is the particle still useful?
  isDead() {
    return (this.lifespan < 0.0);
  }
}

```

sketch.js
```js
let particles = [];
let waterLevel;

function setup() {
  createCanvas(640, 240);
  waterLevel = height/1.35;
}

function draw() {
  background(255);
  
   // Dibujar "agua"
    fill(100, 100, 255, 150);
    rect(0, waterLevel, width, height - waterLevel);
  
  particles.push(new Particle(width / 2, 20));

  // Looping through backwards to delete
  for (let i = particles.length - 1; i >= 0; i--) {
    let particle = particles[i];
    particle.run();
    
    if (particle.position.y > waterLevel) {
      let drag = particle.calculateDrag(0.2); // Coeficiente de arrastre
        particle.applyForce(drag);
    }
    
    if (particle.isDead()) {
      //remove the particle
      particles.splice(i, 1);
    }
  }
}
```

- En este ejemplo lo que se hace para manejar la memoria, es que se usa la función ```splice()```, la cual lo saca del arreglo por lo que la función ```Draw()``` no vuelve a itreral por el, pero no me queda claro si P5.js se encarga de eliminar de la memoria el objeto o si el objeto sigue existiendo pero no se accede a él.
- En esta simulación apliqué el concepto de resistencia en diferentes medios, específicamente, el agua, donde las partículas desaceleran al momento de entrar a este nuevo medio.

  ![Resultados](../../../../../src/assets/Unidad05/A02_resultado0.png)

### [Link de la simulación](https://editor.p5js.org/Adept-KeyCap/full/7KWghXoAb)

## 4.4:
