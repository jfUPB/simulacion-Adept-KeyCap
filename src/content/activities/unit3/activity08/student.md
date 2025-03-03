- La diferencia entre las 2 líneas es que en la primera se hace un **paso por valor** lo cual permite modificarlibremente el valor de ```friction``` sin alterar la instancia original, y en la otra se hace un **paso por referencia** lo que hace que se almacene la Instancia original del objeto ```p5.vector```

  ```js
  let friction = this.velocity.copy();  //Paso por valor
  let friction = this.velocity;         // Paso por Referencia
  ```
