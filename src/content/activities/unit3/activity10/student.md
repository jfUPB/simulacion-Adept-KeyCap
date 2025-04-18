- **Fricción:** En cada actualización del sistema, la fricción se calcula y se resta de la velocidad de la partícula, lo que hace que esta desacelere progresivamente hasta detenerse.
En el código, lo implementé creando un vector de fricción proporcional a la velocidad pero en dirección contraria, asegurándome de que la magnitud no sea mayor que la velocidad actual para evitar que la partícula cambie de dirección abruptamente.

#### [Link de la simulación](https://editor.p5js.org/Adept-KeyCap/full/O6J5fFYhV)

```js
// Simulación 1: Fricción
let particle;
let c = -0.015;

function setup() {
    createCanvas(600, 400);
    particle = new Particle(width / 2, height / 2);
}

function draw() {
    background(220);
    let friction = particle.vel.copy();
    friction.mult(c); // Coeficiente de fricción
    particle.applyForce(friction);
    
    particle.update();
    particle.show();
}

class Particle {
    constructor(x, y) {
        this.pos = createVector(x, y);
        this.vel = createVector(random(-2, 2), random(-2, 2));
        this.acc = createVector(0, 0);
    }

    applyForce(force) {
        this.acc.add(force);
    }

    update() {
        this.vel.add(this.acc);
        this.pos.add(this.vel);
        this.acc.mult(0);
    }

    show() {
        fill(0);
        ellipse(this.pos.x, this.pos.y, 20);
    }
}

```
##
- **Resistencia al agua:** En cada frame, se calcula la fuerza de resistencia en función de la velocidad de la partícula y el coeficiente de resistencia del medio en el que se encuentra. Esta fuerza se opone al movimiento y se resta de la velocidad de la partícula, reduciendo gradualmente su rapidez. En medios más densos, como el agua, este efecto es más notorio, ya que la resistencia es mayor.
#### [Link de la simulación](https://editor.p5js.org/Adept-KeyCap/full/hy8MrYGzI)


```js
let particle;
let waterLevel;

function setup() {
    createCanvas(600, 600);
    particle = new Particle(width / 2, 50);
    waterLevel = height / 2; // Mitad inferior del lienzo será "agua"
}

function draw() {
    background(220);
    
    // Dibujar "agua"
    fill(100, 100, 255, 150);
    rect(0, waterLevel, width, height - waterLevel);
    
    // Aplicar gravedad
    let gravity = createVector(0, 0.2);
    particle.applyForce(gravity);
    
    // Aplicar resistencia si está en el agua
    if (particle.pos.y > waterLevel) {
        let drag = particle.calculateDrag(0.2); // Coeficiente de arrastre
        particle.applyForce(drag);
    }
    
    particle.update();
    particle.show();
}

class Particle {
    constructor(x, y) {
        this.pos = createVector(x, y);
        this.vel = createVector(0, 0);
        this.acc = createVector(0, 0);
        this.mass = 2;
    }

    applyForce(force) {
        let f = p5.Vector.div(force, this.mass);
        this.acc.add(f);
    }
    
    calculateDrag(coefficient) {
        let speed = this.vel.mag();
        let dragMagnitude = coefficient * speed * speed;
        let dragForce = this.vel.copy().mult(-1);
        dragForce.setMag(dragMagnitude);
        return dragForce;
    }

    update() {
        this.vel.add(this.acc);
        this.pos.add(this.vel);
        this.acc.mult(0)
    }

    show() {
        fill(0, 0, 0);
        noStroke();
        ellipse(this.pos.x, this.pos.y, 20);
    }
}

```

##
- **Atracción gravitacional:** Aquí simulo la atracción gravitacional entre dos objetos, uno fijo en el centro ```attractor``` y otro en movimiento ```mover```. El mover es afectado por una fuerza gravitacional calculada con la Ley de Gravitación Universal, lo que hace que su trayectoria se curve y pueda orbitar alrededor del attractor.
#### [Link de la simulación](https://editor.p5js.org/Adept-KeyCap/full/H39TS0sH9)
```js
let mover;
let attractor;
let gravityStrenght = 1;

function setup() {
  createCanvas(640, 240);
  mover = new Mover(300, 190, 2);
  attractor = new Attractor();
}

function draw() {
  background(255);

  let force = attractor.attract(mover);
  mover.applyForce(force);
  mover.update();

  attractor.show();
  mover.show();
}

class Mover {
  constructor(x, y, mass) {
    this.mass = mass;
    this.radius = mass * 8;
    this.position = createVector(x, y);
    this.velocity = createVector(1, 0);
    this.acceleration = createVector(0, 0);
  }
  // Segunda ley de newton
  applyForce(force) {
    let forceVector = p5.Vector.div(force, this.mass);
    this.acceleration.add(forceVector);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }

  show() {
    stroke(0);
    strokeWeight(2);
    fill(127, 127);
    circle(this.position.x, this.position.y, this.radius * 2);
  }
}

class Attractor {
  constructor() {
    this.position = createVector(width / 2, height / 2);
    this.mass = 20;
  }

  attract(mover) {
    // dirección de la fuerza
    let force = p5.Vector.sub(this.position, mover.position);
    // distancia entre los objetos
    let distance = force.mag();
    // limitar la distancia para establecer área efectiva de la gravedad
    distance = constrain(distance, 5, 25);

    // magnitud de la fuerza gravitacional
    let strength = (gravityStrenght * this.mass * mover.mass) / (distance * distance);
    // obtener el vector de fuerza
    force.setMag(strength);
    return force;
  }

  show() {
    strokeWeight(0);
    stroke(0);
    fill(0, 255);
    circle(this.position.x, this.position.y, this.mass * 2);
  }
}

```
