El Motion 101 Algorithm es una forma sencilla de mover un objeto usando vectores. Primero, la aceleración modifica la velocidad, luego la velocidad cambia la posición del objeto en cada actualización. Si es necesario, la velocidad se puede limitar para que el movimiento no sea demasiado rápido.

En código, esto se traduce en tres pasos clave:

```js 
speed.add(acceleration); // Aumenta la velocidad con la aceleración
position.add(speed);    // Mueve el objeto sumando la velocidad a la posición
speed.limit(maxSpeed);  // (Opcional) Restringe la velocidad máxima

```
Este algoritmo es la base del movimiento en animaciones y simulaciones, permitiendo transiciones suaves y realistas.
