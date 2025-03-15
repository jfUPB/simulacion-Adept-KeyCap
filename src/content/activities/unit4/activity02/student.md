### Primera simulación (manejo de ángulos)
**¿Qué está pasando en esta simulación? ¿Cuál es la interacción?** - 
Los elementos gráficos están girando alrededor del centro de la pantalla. La interacción ocurre al aplicar rotaciones en cada fotograma.

**¿Por qué se traslada el origen de coordenadas al centro?** - 
Hacer esto facilita la rotación, ya que los objetos giran alrededor del punto (0,0) en lugar de moverse de forma extraña.

**¿Cuál es la relación entre el sistema de coordenadas y la función rotate()?** - 
La función rotate() gira todo el sistema de coordenadas respecto al origen actual. Si no se traslada al centro antes, la rotación ocurre en otro punto de la pantalla.

**¿Por qué los elementos parecen dibujarse en (0,0)?** - 
Porque el sistema de coordenadas ya está trasladado al centro. Desde ahí, se dibujan los objetos en posiciones relativas.

**¿Por qué los elementos gráficos rotan aunque el código de dibujo no cambia?** - 
Porque en cada cuadro, se aplica rotate(), lo que cambia el ángulo del sistema de coordenadas antes de dibujar los objetos.
##
### Segunda simulación (dirección del movimiento)
**¿Qué es lo que se está haciendo en el marco Motion 101?** - 
Se está aplicando la idea de posición, velocidad y aceleración para que el objeto se mueva con una dirección clara.

**¿Qué hace la función heading()?** - 
Devuelve el ángulo de dirección de un vector. En este caso, indica hacia dónde apunta el vector de velocidad.

**¿Qué hacen push() y pop()?** - 
push() guarda el estado actual del sistema de coordenadas y pop() lo restaura. Esto evita que las transformaciones como rotate() afecten a otros elementos.

**¿Qué hace rectMode(CENTER)?** - 
Hace que los rectángulos se dibujen desde su centro en lugar de desde una esquina. Así, la rotación es más natural.

**¿Cuál es la relación entre el ángulo de rotación y el vector de velocidad?** - 
El ángulo de rotación se calcula a partir del vector de velocidad usando heading(). Esto hace que el objeto siempre apunte en la dirección en la que se mueve.
