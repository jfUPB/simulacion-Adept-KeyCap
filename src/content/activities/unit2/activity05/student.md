### Código
```js

let t = 0; // Interpolation value
let speed = 0.01; // Oscillation speed
let direction = 1; // Controls whether it goes up or down

function setup() {
    createCanvas(600, 600);
}

function draw() {
    background(200);

    let v0 = createVector(50, 50);
    let v1 = createVector(500, 0);
    let v2 = createVector(0, 500);
  
  // Since the "drawArrow" function uses the "translate" method to change the origin,
  // vectors must be created with respect to the Canvas and not their local position
    let v3 = createVector(550, 50);
    let v4 = createVector(-500, 500);

    let interpolatedValue = valueOscillator(t, speed);
    let v5 = p5.Vector.lerp(v1, v2, interpolatedValue);

    drawArrow(v0, v1, 'red');
    drawArrow(v0, v2, 'blue');
    drawArrow(v0, v5, lerpColor('red', 'blue', interpolatedValue));
    drawArrow(v3, v4, 'rgb(0,145,0)');
}

function drawArrow(base, vec, myColor) {
    push();
    stroke(myColor);
    strokeWeight(3);
    fill(myColor);
    translate(base.x, base.y);
    line(0, 0, vec.x, vec.y);
    rotate(vec.heading());
    let arrowSize = 7;
    translate(vec.mag() - arrowSize, 0);
    triangle(0, arrowSize / 2, 0, -arrowSize / 2, arrowSize, 0);
    pop();
}

// Function that oscillates continuously between 0 and 1
function valueOscillator() {
    t += speed * direction;

    if (t >= 1 || t <= 0) {
        direction *= -1; // Changes direction when reaching the limits
    }

    return t;
}


```

- ```lerp()``` y ```lerpColor()``` Ambas funciones lo que hacen es **interpolar o transmutar** un valor entre 2 específicos, ajustando que tanto se parece a un valor o a otro según un _valor normalizado entre 0 y 1_, por lo que si modificamos esta valor constantemente podemos realizar una animación entre estos 2 valores. Además, el ```lerpColor()``` hace lo mismo pero en 3 valores diferentes, es decir en un vector de componentes **RGB**
- Lo primero de la función ```drawArrow()``` es su parte básica donde se reciben 3 parametros; **Base**, el cual establece el origen del vector; **vec**, el vector al cual va a apuntar la flecha; y **myColor**, que se explica solo. Después se establecen los valores de un stroke con los atribuitos de color y grosor establecidos, pero después de esto es donde va lo interesante:
  1. Primero se usa el método ```translate(x, y)``` el cual hace que todo lo que se dibuje después de esa función utilize un nuevo punto de origen _(El establecido en la función)_.
  2. Se dibuja la línea que visualiza la magnitud y dirección del vector con ```line()```, al mismo tiempo se conoce internamente la dirección del vector, pero para poder visualizarla, se utiliza ```rotate(vec.heading())``` para poder que todo lo que se dibuje después de esta función esté alineado con la orientación del vector.
  3. Se establece el tamaño de la flecha y se vuelve a cambiar el origen usando ```translate(x, y)```, posicionandolo en la punta del vector, terminando todo dibujando con ```triangle(x, y, z)```.
  4. Por últio están las funciones ```push()``` y ```pop()```, las cuales guardan el estado acutal del **Canvas** y la otra elimina los cambios hechos a los atributos como el centro, así se puede usar la función de manera escalable.
