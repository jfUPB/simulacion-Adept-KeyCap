### Gestión de memoria
- Durante toda la unidad no quise complicarme gestionando manualmente la memoria, sino que aproveché el Garbage Collector de JavaScript, pero comprendo lo que hace que es liberar el espacio reservado para una instancia en el momento que se deja de iterar a travéz de ella, dando paso a que se use ese espacio para una nueva instancia, lo cual es muy importante a la hora de implementar sitemas de partículas con cientos o miles de instancias.

### Motion 101
- En las actividades anteriores apliqué varios conceptos de este marco pero nunca todos juntos, ya que el objetivo no era buscar un sistema totalmente realista, en el ejercicio 2, en el apartado 4.2 implementé lo que sería el concepto del **Drag**, la fuerza de resistencia de un medio. En el apartado 4.4 implementé un **campo gravitatorio** que atraía a todas las ptatículas al rededor, si importar el **emitter**. En el 4.6 implementé un área de fuerza, un impulso aplicado en determinada zona para simular el empuje de uan corriente de viento. Y por último en la actividad 3, implementé un coeficiente de rebote a un objeto tipo **Ball**, el cual cada vez que rebota, no se ve reflejado el 100% de su velocidad sino una fracción, entre más cercano sea a 1, más rebotará.

### Fuerzas externas
- Como tal las fuerzas que se aplicaron fueron, la corriente de viento, el campo de gravedad y el **Drag** del agua.
Drag:
```js
// Método dentro de la clase particle

calculateDrag(coefficient) {
        let speed = this.velocity.mag();
        let dragMagnitude = coefficient * speed * speed;
        let dragForce = this.velocity.copy().mult(-1);
        dragForce.setMag(dragMagnitude);
        return dragForce;
  }

// Calcular el Drag cuando cambia de medio

if (particle.position.y > waterLevel) {
      let drag = particle.calculateDrag(0.2); // Coeficiente de arrastre
        particle.applyForce(drag);
```

Campo gravitatorio:
```js
// Método dentro de la clase Atracctor

attract(particle) {
    // dirección de la fuerza
    let force = p5.Vector.sub(this.position, particle.position);
    // distancia entre los objetos
    let distance = force.mag();
    // limitar la distancia para establecer área efectiva de la gravedad
    distance = constrain(distance, 5, 20);

    // magnitud de la fuerza gravitacional
    let strength = (gravityStrenght * this.mass * particle.mass) / (distance * distance);
    // obtener el vector de fuerza
    force.setMag(strength);
    return force;
  }

// Iterar por cada partícula de cada emitter

for (let emitter of emitters) {
    emitter.run();
    emitter.addParticle();

    for (let particle of emitter.particles){
      let force = attractor.attract(particle);
      particle.applyForce(force);
    }
  }
```

Corriente de viento:
```js
// Aplicar un vector de fuerza  a las partículas mientras estén dentro de un área determinada

for(var i = emitter.particles.length - 1; i > 0; i--){
    let currentPart = emitter.particles[i];
    var partPos = currentPart.position;
    if(partPos.y < windArea.y && partPos.y > windArea.x){
      console.log("inside wind");
      currentPart.applyForce(windForce);
    }
  }
```

### Herencia y polimorfismo
- La herencia se ve reflejada en el momento que gestiono clases como ```Proyectile```, ```Dust```, ```Ball```, todas estas heredando las funcionalidades de ```Particle```.
- Por el lado del polimorfismo, este está implementado sobreescribiendo la función ```show()``` o ```run()``` de cada una de las clases que hereda de ```Particle```, para lograr un comporatamiento y visualización similar o diferente de la clase padre. 
