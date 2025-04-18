### [Prueba la simulación aquí](https://editor.p5js.org/Adept-KeyCap/full/53NnqLQvV)

Este código está mayoritariamente basado en la teoría y la práctica de [The n-Body Problem - The Nature of Code](https://natureofcode.com/forces/#the-n-body-problem). Simula cómo varios objetos se atraen entre sí usando una versión simplificada de la ley de gravitación de Newton. Al iniciar, se crean 10 cuerpos pequeños en un rango cerca del centro, que se mueven según la fuerza gravitacional que ejercen unos sobre otros.  

Cada vez que se hace clic, se añade un nuevo cuerpo más grande en los bordes del lienzo, afectando la dinámica del sistema. Aunque no es una simulación exacta del problema de los N-cuerpos, permite ver cómo múltiples objetos interactúan gravitacionalmente, generando movimientos y trayectorias complejas.

![Resultados](../../../../../src/assets/Unidad03/A11_resultado0.gif)

```js
let bodies = [];
let G = 1;
let spawnOffset = 50;

function setup() {
  createCanvas(640, 480);

  let centerX = width / 2;
  let centerY = height / 2;

  for (let i = 0; i < 10; i++) {  // Instanciar los cuerpos en un rango cercano al centro según el valor que les demos.
    bodies[i] = new Body(
      random(centerX - spawnOffset, centerX + spawnOffset),
      random(centerY - spawnOffset, centerY + spawnOffset), 1);
  }
}

function draw() {
  background(255);

  for (let i = 0; i < bodies.length; i++) {
    for (let j = 0; j < bodies.length; j++) {
      if (i !== j) {
        let force = bodies[j].attract(bodies[i]);
        bodies[i].applyForce(force);
      }
    }

    bodies[i].update();
    bodies[i].show();
  }
}

function mousePressed() {
  let x, y;
  let edge = floor(random(4)); // Elegir un borde aleatorio (0: arriba, 1: derecha, 2: abajo, 3: izquierda)

  if (edge === 0) {
    // Arriba
    x = random(width);
    y = 0;
  } else if (edge === 1) {
    // Derecha
    x = width;
    y = random(height);
  } else if (edge === 2) {
    // Abajo
    x = random(width);
    y = height;
  } else {
    // Izquierda
    x = 0;
    y = random(height);
  }

  bodies.push(new Body(x, y, 3)); // Crea un nuevo Body más grande
}

```
