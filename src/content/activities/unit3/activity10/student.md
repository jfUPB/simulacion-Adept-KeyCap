- **Fricción:** En cada actualización del sistema, la fricción se calcula y se resta de la velocidad de la partícula, lo que hace que esta desacelere progresivamente hasta detenerse.
En el código, lo implementé creando un vector de fricción proporcional a la velocidad pero en dirección contraria, asegurándome de que la magnitud no sea mayor que la velocidad actual para evitar que la partícula cambie de dirección abruptamente.

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

- **Resistencia al aire:**

- **Atracción gravitacional:**
