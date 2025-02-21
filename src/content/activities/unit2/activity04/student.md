- ```mag()``` devuelve la magnitud _(o norma)_ de un vector, es decir, su longitud en el espacio. Se calcula como la raíz cuadrada de la suma de los cuadrados de sus componentes.

- ```magSq()``` devuelve la magnitud al cuadrado del vector, sin calcular la raíz cuadrada. Es más eficiente que ```mag()``` porque evita una operación costosa _(sqrt)_. Se usa cuando solo se necesita comparar magnitudes sin la raíz cuadrada.

- Convierte un vector en un vector unitario _(de magnitud 1)_, manteniendo su dirección. Se usa para trabajar con direcciones sin cambiar proporciones de escala.

- El producto punto ```dot()``` calcula la similitud entre dos vectores. Su resultado es mayor cuanto más alineados estén y es cero si son perpendiculares.

- La versión de instancia ```v1.dot(v2)``` calcula el producto punto de v1 con v2, mientras que la versión estática ```p5.Vector.dot(v1, v2)``` hace lo mismo sin necesidad de instanciar un objeto.

- El producto cruz entre dos vectores en 3D genera un nuevo vector perpendicular a ambos, cuya magnitud representa el área del paralelogramo que forman.

- Calcula la distancia euclidiana entre dos puntos representados como vectores. Se usa para medir separación en un espacio 2D o 3D.

- ```normalize()``` ajusta un vector a magnitud 1, conservando su dirección, y por otro lado ```limit(max)``` restringe la magnitud de un vector a un valor máximo, útil en simulaciones para evitar velocidades excesivas.
