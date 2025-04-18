### Desafíos encontrados y Aprendizajes
- Al implementar la interacción de las partículas con los puntos de atracción y repulsión, noté que si la fuerza aplicada era demasiado grande o si las partículas estaban demasiado cerca, se generaban movimientos bruscos e incluso comportamientos erráticos. Fue necesario ajustar la **magnitud de las fuerzas** para que el movimiento se viera más fluido y natural.

- Inicialmente, las influencias (atractores y repulsores) no desaparecían, lo que hacía que el espacio de simulación se saturara con demasiados elementos. Para solucionar esto, implementé un tiempo de vida para cada influencia, lo que permitió una experiencia más dinámica.

- Implementar estelas para las partículas sin que afectara el rendimiento o se viera desordenado requirió ajustar la cantidad de posiciones almacenadas en el rastro. Además, usar un fondo con transparencia en lugar de redibujar todo ayudó a que las estelas fueran más naturales. _(Como cuando lo descubrí por accidente en la unidad pasada)_

