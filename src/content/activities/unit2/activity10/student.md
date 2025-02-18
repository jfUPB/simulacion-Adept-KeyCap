### Conceptualización de la pieza de arte generativo
- La idea es crear un sistema de partículas que se muevan libremente con velocidades aleatorias dentro del lienzo. Estas partículas van explorando el espacio sin rumbo fijo, pero pueden ser influenciadas por la interacción del usuario. Con el clic derecho, se coloca un círculo negro en la posición del cursor que actúa como un punto de atracción, jalando las partículas hacia él. En cambio, con el clic izquierdo, se genera un círculo que repele las partículas, alejándolas de su posición.

- Para que la composición se mantenga dinámica y no se llene de puntos de atracción y repulsión, estos círculos desaparecerán repentinamente después de un tiempo. Así, la escena está en constante cambio, dándole una sensación más orgánica e interactiva.

### Aplicación del marco Motion 101
- El sistema sigue el marco Motion 101, ya que cada partícula se mueve con un vector de velocidad y se ve afectada por fuerzas externas (atracción y repulsión). Se aplica la idea de que la aceleración es la clave para generar movimiento realista: las partículas no cambian de dirección instantáneamente, sino que poco a poco ajustan su trayectoria hacia los puntos de influencia, dándole un comportamiento más natural.

### Referentes e inspiración
- Esta idea se inspira en el comportamiento de partículas en simulaciones físicas y en obras de arte generativo que usan interacción para modificar patrones dinámicos. También recuerda un poco al movimiento de enjambres o partículas en sistemas naturales, donde diferentes fuerzas afectan la trayectoria de los elementos en el espacio.
