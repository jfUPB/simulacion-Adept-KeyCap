**Código**
```js
let t = 0.0;
let audioContext;
let analyser;
let dataArray;
let smoothedNoiseLevel = 2; // Variable to smooth the background transition
let normalizedNoise;
let walker;
let shapeTimer = 0;
let shapeInterval = 30; // Controls the speed of shape appearance

function setup() 
{
  createCanvas(360 * 2, 240 * 2);
  walker = new Walker();

  // Request access to the microphone
  navigator.mediaDevices.getUserMedia({ audio: true })
    .then(function(stream) {
      audioContext = new (window.AudioContext || window.webkitAudioContext)();
      const source = audioContext.createMediaStreamSource(stream);

      // Create an AnalyserNode object to obtain real-time audio signal data.
      analyser = audioContext.createAnalyser();
      analyser.fftSize = 256;
      source.connect(analyser); // Connect the microphone to the analyser

      dataArray = new Uint8Array(analyser.frequencyBinCount);
    })
    .catch(function(err) {
      console.error('Error accessing the microphone:', err);
    });
}

function draw()
{
  if (analyser) {
    analyser.getByteFrequencyData(dataArray);
    // Calculate the average noise level
    let average = dataArray.reduce((sum, value) => sum + value, 0) / dataArray.length;

    // Normalize the noise level
    normalizedNoise = map(average, 0, 255, 0, 1);

    // Interpolate the noise transition
    smoothedNoiseLevel = lerp(smoothedNoiseLevel, normalizedNoise, 0.1);

    // Map the smoothed level to a color between white and black
    let bgColor = map(smoothedNoiseLevel * 2, 0, 1, 255, 0);
    background(bgColor, average);
  } else {
    background(255);
  }

  let xoff = t;
  noFill();
  strokeWeight(10);

  beginShape(); // Green Line
  for (let i = 0; i < width; i++)
  {
    let y = noise(xoff) * height * smoothedNoiseLevel / 0.2; // Adjust noise level based on the microphone
    xoff += 0.01 * normalizedNoise;
    vertex(i, y);
    stroke(y, y / 2, y * 2);
  }
  endShape();

  beginShape(); // Purple Line
  for (let i = 0; i < width; i++)
  {
    let y = noise(xoff) * height * smoothedNoiseLevel / 0.5; // Adjust noise level based on the microphone
    xoff += 0.01 * normalizedNoise;
    vertex(i, y);
    stroke(y, y * 2, y / 2);
  }
  endShape();
  t += 0.05;

  // Move the walker using Lévy flight
  walker.step();
  walker.show();

  // Draw random shapes with Gaussian distribution following the Lévy flight pattern
  if (frameCount - shapeTimer > shapeInterval) {
    shapeTimer = frameCount;
    let x = walker.x;
    let y = walker.y;
    let size = random(10, 50);
    
    // Generate a Gaussian value centered at 1 with a standard deviation of 1
    let shapeType = int(abs(randomGaussian(1, 1)) % 3); // Limit values to 0, 1, or 2
    
    noStroke();
    fill(random(255), random(255), random(255), 150);
    
    if (shapeType === 0) {
      ellipse(x, y, size, size); // More likely
    } else if (shapeType === 1) {
      rect(x, y, size, size); // Less likely
    } else {
      triangle(x, y, x + size, y + size, x - size, y + size); // Least likely
    }
  }
}

// Function to generate a random number with a Lévy distribution
function levy(mu = 1.5) 
{
    let u = Math.random();
    let v = Math.random();
    return Math.pow(u, -1 / mu) * Math.sin(2 * Math.PI * v);
}

// Function to perform a Lévy flight
function levyFlight(mu = 1.5) 
{
    let stepLength = levy(mu);
    let angle = Math.random() * 2 * Math.PI;
    return {
        x: stepLength * Math.cos(angle),
        y: stepLength * Math.sin(angle)
    };
}

class Walker
{
  constructor()
  {
    this.x = width / 2;
    this.y = height / 2;
  }

  show()
  {
    stroke(0);
    point(this.x, this.y);
  }

  step() {
    let step = levyFlight();
    this.x += step.x;
    this.y += step.y;
    
    // Keep inside the screen boundaries
    this.x = constrain(this.x, 0, width);
    this.y = constrain(this.y, 0, height);
  }
}

```

**Resultado de la actividad**

![Resultado de la actividad09](../../../../../src/assets/Unidad01/A09_Resultado1.gif)

- [Click aquí para probarlo tu mismo](https://editor.p5js.org/Adept-KeyCap/full/4nhPijn-Y)

- Al final lo único que cambió sobre la marcha fue el fondo de la pantalla al cual cambia su color con interpolación para hacerlo negro cuando hay mucho ruido, lo que por alguna razón termino dando cierto efecto visual de ghosting con respecto a los objetos que si se pintan bien en pantalla, mi teoría es que puede que al estar cambiando el color de la pantalla, no esté cambiando entre blanco y negro sino entre negro y vacío, por lo que le da este efecto en el background, me gustó tanto como se veía visualmente que decidí no tocarlo más para que quedara con este efecto.

