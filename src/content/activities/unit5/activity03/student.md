### Concepto
- En esta obra de arte generativo voy a implementar un sistema de partículas en el cual según los requerimientos, usará herencia, y polimorfismo. Al mismo tiempo el usuario podrá interactuar usando el micrófono para incrementar la potencia del sistema de partículas.


### Gestión de memoria
- Investigué la pregunta que me hice en la actividad anterior, de cómo hace p5.js para gestionar esto, ya que desde el códgio lo único que se veía es que se eliminaban de una lista a travez la cual se iteraba. Cuando busqué, efectivamente **P5.js** usa el _garbage collector_ de _JavaScript_ para gestionar su memoria. De esta manera, cuando el código deja de iterar a travez de un objeto _(En este caso una partícula que se elimina de la lista)_ este es elejible para la colección de basura y se libera el espacio de memoria de dicho objeto.


### Conceptos de unidades anteriores
- **Motion 101**: Como siempre, jugar con físcias es difertido, por lo que le adicionaré a las partículas un peso para poder hacer variacones en las interacciónes que implementaré. En particular haré una pelota con el que el usuario va a interactuar.
- A esta misma pelota también le añadiré un coeficiente de rebote para que no siempre rebote infinitamentey así su comportamiento cambie con el tiempo.
- También estaran lo que son cambios de entornos o zonas espefícias donde se aplican fuerzas diferentes.
- Por último, la escena empieza con un ```emitter``` y un ```ball```, cada uno va a aparecer en una posición aleatoria según una distribución Gaussiana, para que tiendan a aparecer en la mitad, pero no siempre.
