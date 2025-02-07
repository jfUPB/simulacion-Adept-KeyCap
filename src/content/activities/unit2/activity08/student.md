- Me propuse a hacer una modificación en la cual cada vez que una pelota o un ```Mover()``` llegara al borde de un canvas, apareciera uno nuevo.
 
- Me imagino que va a llegar a un punto donde van a haber tantas bolitas que la RAM asignada al navegador no va a soportar.

- Durante la realización de este ejercicio, me di cuenta que en realidad no estaba jugando con los vectores, lo cual creo que es todo el proposito de esta unidad por lo que decidí también añadir un cambio más, en vez de resetear la posición de la **pelota** cuando llegue a el borde del **Canvas**, la pelota debía cambiar de dirección.
  - La Lógica detrás de esto es muy simple, a la hora de detectar la colisión dentro de la clase ```Mover()```, voy a agarrar el componente ```Mover.velocity``` y lo **múltiplico** por -1, tanto en **X** como en **Y**, lo que termina por cambiar la dirección en la que se dirigía el ```Mover()``` simulando un rebote de uan pelota.

- Lo que pasó fue efectivamente lo que me esperaba, como cada que una pelota rebota en el borde hace aparecer una nueva, su instaciación va a crecer de manera exponencial. Al pasar unos 30 o 40 segundos la pestaña del **P5.js** se pone lenta, pero un poco más de un minuto después, la pestaña de congela pero el navegador sigue respondiedo.

- En cuanto al rebote ocurre porque invierto la dirección en la que va dirigida la velocidad de la pelota, simulando lo que sería la fuerza normal. Con respecto a el navegador, puede ser o cosa de P5 o de Firefox que no dejan que haya un leak en la memoria del navegador, manteniendo los recursos aislads y limitados a ciertas ventanas.

- **Modificaciones:**

  ```js

  // Cambio la función para multiplicar la velocidad por su misma inversa, lo que simula el rebote
  checkEdges() {
    if (this.position.x > width) {
      this.velocity.x *= -1;
    } else if (this.position.x < 0) {
      this.velocity.x *= -1;

    }

    if (this.position.y > height) {
      this.velocity.y *= -1;
    } else if (this.position.y < 0) {
      this.velocity.y *= -1;
    }
  }

  ```

  ```js

  // Cambio la lógica de como se instancian las pelotas para poder tener un arreglo con ellas almacenadas.
  let movers = [];

  function setup() {
    createCanvas(640, 640);
    movers.push(new Mover());
  }

  function draw() {
    background(255);

  for (let i = 0; i < movers.length; i++) {
    movers[i].update();
    movers[i].checkEdges();
    movers[i].show();

   
    if (movers[i].position.x >= width || movers[i].position.y >= height ||   movers[i].position.x <= 0 || movers[i].position.y <= 0) {
      movers.push(new Mover()); 
      }
    }
  }

  
  ```

### [Click Aquí para probar la simulación](https://editor.p5js.org/Adept-KeyCap/full/T2ZL_YHs8)
