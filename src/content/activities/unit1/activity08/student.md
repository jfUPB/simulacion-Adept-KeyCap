- La idea en principio es general algo visualmente llamativo utilizando como componente principal el ruido de perlin, el cual manipularé sus valores en tiempo real para que cambie la amplitud de los valores por medio del micrófono, lo que me parece más interesante de esta clase de experimentos es lo entretenido que es ver a las personas haciendo ruidos diferentes para ver comoprtar el programa de formas diferentes.
- Pienso usar tres conceptos de la siguiente manera:
  - **Perlin Noise**: Va a ser el punto central de la pieza o el más llamativo con el cual voya general una graficación de los números que puede general el ruido de perlin, dentro de ese hay un concepto que se llama el salto, que es la cantidad máxima de variación que puede tener en un tiempo determinado, por lo que voy a hacer que este valor sea directamente proporcional a la cantidad de ruido.
  - **Gaussian Distribution**: Voy a implementar generación de figuras aleatoria favoreciaendo unas u otras en un patrón de distribución gausiana, la velocidad con la que se generan nuevas figuras, también va  aestar directamente asociada con al cantidad de ruido que detecte el micrófono.
  - **Levy Flight**: Estas figuras apareceran en lugares aleaotrios que serán dictados por el patról del vuelo de Levy, por lo que harán ciertos recorridos particulares y no serán totalmente aleatorios.

- Referentes:
  - https://p5js.org/examples/repetition-color-interpolation/
  - https://www.ecophon.com/es/the-lab/#EXPERIMENTO-3
  - https://natureofcode.com/random/#a-smoother-approach-with-perlin-noise
