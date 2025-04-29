### Concepto
- En esta obra de arte generativo voy a implementar un sistema de partículas en el cual según los requerimientos, usará herencia, y polimorfismo. Al mismo tiempo el usuario podrá interactuar usando el micrófono para incrementar la potencia del sistema de partículas.


### Gestión de memoria
- Investigué la pregunta que me hice en la actividad anterior, de cómo hace p5.js para gestionar esto, ya que desde el códgio lo único que se veía es que se eliminaban de una lista a travez la cual se iteraba. Cuando busqué, efectivamente **P5.js** usa el _garbage collector_ de _JavaScript_ para gestionar su memoria. De esta manera, cuando el código deja de iterar a travez de un objeto _(En este caso una partícula que se elimina de la lista)_ este es elejible para la colección de basura y se libera el espacio de memoria de dicho objeto.


### Conceptos de unidades anteriores
- 
