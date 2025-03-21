### ¿Cuál es la relación entre r y theta con x e y?
Ambas representan coordenadas en un punto del espacio, pero unas usan la distancia del origen y un ángulo ``` r | Theta ```, mientras que el otro se basa en distancias desde el origen en 2 ejes diferentes. Ambos pueden represnetar el mismo punto con diferentes valores, pero pueden convertirse de manera secilla entre ellas para tener doferentes utilidades.

### ¿Qué pasa con la primera modificación (p5.Vector.fromAngle(theta)) y por qué?

El código original usa ```x = r * cos(theta)``` y ```y = r * sin(theta)``` pero ahora ```p5.Vector.fromAngle(theta)``` genera un vector unitario (longitud 1).
Como ```r``` no se usa, el punto siempre está en un círculo de radio 1.

### ¿Qué pasa con la segunda modificación (p5.Vector.fromAngle(theta, r)) y por qué?
Ahora ```r``` se pasa como argumento, lo que ajusta el tamaño del vector.
El punto vuelve a moverse en un círculo de radio ```r```, como en la versión original.
