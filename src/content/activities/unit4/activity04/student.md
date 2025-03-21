¿Qué modificación hay que hacer para agregar fuerzas acumulativas?
En cada frame, hay que calcular y acumular las fuerzas aplicadas al objeto antes de actualizar su movimiento. Esto permite que el objeto responda a múltiples fuerzas de manera realista.

¿Dónde está el Attractor y cómo cambiar su color?
El Attractor es el círculo en el centro. Para cambiar su color, modifica su display():

```js
fill(255, 0, 0); // Color rojo
```
¿Cómo hacer que el Attractor se mueva con el mouse y cambie de color al pasar sobre él?

 - Detectar si el mouse está encima:
  ```js
  this.rollover = dist(mouseX, mouseY, this.position.x, this.position.y) < this.mass;
  ```
  - Arrastrar el Attractor:
  ```js
  if (this.dragging) {
    this.position.set(mouseX + this.dragOffset.x, mouseY + this.dragOffset.y);
  }
  ```
  - Activar arrastre con el mouse:
  ```js
  function mousePressed() {
    attractor.dragging = attractor.rollover;
    attractor.dragOffset = p5.Vector.sub(attractor.position, createVector(mouseX, mouseY));
  }
  
  function mouseReleased() {
    attractor.dragging = false;
  }
  ```
Con esto, el Attractor cambia de color cuando el mouse lo toca y se puede mover arrastrándolo.
