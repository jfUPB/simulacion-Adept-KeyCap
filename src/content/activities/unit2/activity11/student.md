### [Pruebalo tu mismo](https://editor.p5js.org/Adept-KeyCap/full/W5OwzfoEe)

![Resultado de la actividad11Z](../../../../../src/assets/Unidad02/A11_Resultado0.gif)

```js
let particles = [];
let influences = [];

function setup() {
    createCanvas(600, 600);
    for (let i = 0; i < 100; i++) {
        particles.push(new Particle(random(width), random(height)));
    }
}

function draw() {
    background(220, 50); // Dejar un leve rastro
    
    // Dibujar y actualizar partículas
    for (let p of particles) {
        p.applyForces(influences);
        p.update();
        p.show();
    }
    
    // Dibujar influencias y eliminarlas si han expirado
    for (let i = influences.length - 1; i >= 0; i--) {
        influences[i].show();
        if (influences[i].isExpired()) {
            influences.splice(i, 1);
        }
    }
}

function mousePressed() {
    let type = mouseButton === LEFT ? 'repel' : 'attract';
    influences.push(new Influence(mouseX, mouseY, type));
}

class Particle {
    constructor(x, y) {
        this.pos = createVector(x, y);
        this.vel = p5.Vector.random2D().mult(random(1, 3));
        this.trail = []; // Almacena las posiciones pasadas
    }

    applyForces(influences) {
        for (let inf of influences) {
            let force = p5.Vector.sub(inf.pos, this.pos);
            let distance = constrain(force.mag(), 10, 100);
            force.normalize();
            let strength = map(distance, 10, 100, 1, 0);
            force.mult(inf.type === 'attract' ? strength : -strength);
            this.vel.add(force);
        }
    }

    update() {
        this.trail.push(this.pos.copy()); // Guardar posición actual
        if (this.trail.length > 10) { // Limitar la cantidad de puntos en la estela
            this.trail.shift();
        }
      // Aplicamos conceptos del Motion 101
        this.pos.add(this.vel); 
        this.vel.mult(0.999); // Reducir la velocidad con el tiempo
        this.edges();
    }

    edges() {
        if (this.pos.x > width || this.pos.x < 0) this.vel.x *= -1;
        if (this.pos.y > height || this.pos.y < 0) this.vel.y *= -1;
    }

    show() {
        let speed = this.vel.mag();
        let col = lerpColor(color(0, 0, 255), color(255, 0, 0), map(speed, 0, 3, 0, 1));
        fill(col);
        noStroke();
        
        // Dibujar estela
        for (let i = 0; i < this.trail.length; i++) {
            let alpha = map(i, 0, this.trail.length, 50, 255);
            fill(red(col), green(col), blue(col), alpha);
            ellipse(this.trail[i].x, this.trail[i].y, 4);
        }
        
        // Dibujar partícula
        fill(col);
        ellipse(this.pos.x, this.pos.y, 5);
    }
}

class Influence {
    constructor(x, y, type) {
        this.pos = createVector(x, y);
        this.type = type;
        this.timestamp = millis();
        this.lifespan = 5000;
    }

    isExpired() {
        return millis() - this.timestamp > this.lifespan;
    }

    show() {
        fill(this.type === 'attract' ? 'black' : 'red');
        noStroke();
        ellipse(this.pos.x, this.pos.y, 20);
    }
}
```

- Inicialmente no era tan visualmente atractivo, al pnto que no sentía que se sintiera como una pieza de arte en general, solo una simple simulación. Entonces el único cambio que hice sobre el concepto original, fueron las visuales. Se añadieron efectos visuales como el trail y la animación de desaparición de los campos gravitacionales.
