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
- **Atracción gravitacional:** 
#### [Link de la simulación](https://editor.p5js.org/Adept-KeyCap/full/9OzdCZ5Um)
```js

```
