### Cómo nació la idea
La idea inicial era crear una simulación de ondas inspirada en el agua, pero con un toque visual llamativo, como un efecto de neón. Quería que la animación fuera fluida y que el usuario pudiera interactuar con ella en tiempo real.

### Cambios y mejoras
Al principio, solo había una onda en el centro, pero luego decidí agregar más, con pequeños desfases en Y para darle más profundidad. También añadí partículas flotando alrededor para darle un efecto más dinámico.

- La interacción también evolucionó bastante:

  - **El mouse controla la onda:** La amplitud cambia con la posición en Y y la frecuencia con la posición en X.

  - **Scroll del mouse:** Permite aumentar o disminuir la cantidad de ondas.

  - **Click del mouse:** Hace que las ondas se vuelvan locas por un momento, agregando un toque de caos divertido.

### Resultado final
El resultado es una obra interactiva que combina ondas, partículas y efectos de neón. Con solo mover el mouse, hacer scroll o hacer clic, se pueden crear patrones visuales únicos y dinámicos. Es un experimento entre arte y matemáticas que demuestra cómo algo tan simple como una onda puede transformarse en algo visualmente atractivo e interactivo.


## [Link de la simulación](https://editor.p5js.org/Adept-KeyCap/full/gvvw6mjOT)
```js

let waves = []; // Arreglo para almacenar diferentes objetos de ondas
let waveLength = 50;
let neonColor;
let particles = [];
let soundLevel = 0;
let mic;

function setup() {
  createCanvas(windowWidth, windowHeight);
  mic = new p5.AudioIn();
  mic.start();
  neonColor = color(0, 255, 255);
  
  // Crear una onda por defecto
  waves.push(new Wave(waveLength, 0)); // La primera onda no tiene desfase
}

function draw() {
  background(10, 10, 20, 150);
  
  soundLevel = mic.getLevel() * 500;
  
  // Actualizar y mostrar cada onda en el arreglo de ondas
  for (let i = 0; i < waves.length; i++) {
    waves[i].update();
    waves[i].display();
  }
  
  displayParticles();
}

function displayParticles() {
  for (let i = particles.length - 1; i >= 0; i--) {
    particles[i].update();
    particles[i].display();
    if (particles[i].isOffScreen()) {
      particles.splice(i, 1);
    }
  }
}

function mouseMoved() {
  neonColor = color(random(100, 255), random(100, 255), 255);
}

// Ajustar el número de ondas con la rueda del mouse
function mouseWheel(event) {
  if (event.delta > 0) {
    // Agregar una nueva onda con un desfase aleatorio en Y
    let lastWave = waves[waves.length - 1];
    let offsetY = random(-200, 200); // Desfase aleatorio en Y
    waves.push(new Wave(waveLength, offsetY));
  } else {
    // Eliminar la última onda cuando se hace scroll hacia arriba, pero asegurarse de que quede al menos una
    if (waves.length > 1) {
      waves.pop();
    }
  }
  
  return false; // Evitar que la página haga scroll
}

class Wave {
  constructor(length, offsetY) {
    this.waveLength = length;
    this.neonColor = color(random(100, 255), random(100, 255), 255); // Color aleatorio para cada onda
    this.offsetY = offsetY; // Desfase vertical para cada nueva onda
    this.wave = [];
    
    // Inicializar la onda con valores predeterminados
    for (let i = 0; i < width / this.waveLength; i++) {
      this.wave.push(createVector(i * this.waveLength, height / 2 + this.offsetY));
    }
  }
  
  update() {
    // Obtener la amplitud y la frecuencia basados en la posición del mouse
    let amplitude = map(mouseY, 0, height, 20, 200); // Amplitud de la onda (varía según mouseY)
    let frequency = map(mouseX, 0, width, 0.2, 0.1); // Frecuencia de la onda (varía según mouseX)

    // Actualizar la posición de cada punto en la onda
    for (let i = 0; i < this.wave.length; i++) {
      // Modificar la posición Y de la onda en función de la amplitud y frecuencia
      let noiseFactor = noise(i * frequency, frameCount * 0.01) * 10;
      let yOffset = sin(frameCount * 0.05 + i * 0.5) * amplitude;
      this.wave[i].y = height / 2 + yOffset + noiseFactor + this.offsetY;
      
      if (mouseIsPressed) {
        this.wave[i].y += random(-10, 10);
      }
    }
    
    if (frameCount % 5 === 0) {
      particles.push(new Particle(random(width), random(height / 2 - 50, height / 2 + 50)));
    }
  }
  
  display() {
    // Mostrar la onda
    noFill();
    stroke(this.neonColor);
    strokeWeight(4);
    for (let i = 0; i < this.wave.length - 1; i++) {
      line(this.wave[i].x, this.wave[i].y, this.wave[i + 1].x, this.wave[i + 1].y);
    }
  }
}



class Particle {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.vel = createVector(random(-2, 2), random(-2, 2));
    this.alpha = 255;
  }
  update() {
    this.pos.add(this.vel);
    this.alpha -= 5;
  }
  display() {
    noStroke();
    fill(0, 255, 255, this.alpha);
    ellipse(this.pos.x, this.pos.y, 8);
  }
  isOffScreen() {
    return this.alpha <= 0;
  }
}


```

![image](https://github.com/user-attachments/assets/e35685bf-a8bc-4baf-9ede-9be1de64cbb1)
