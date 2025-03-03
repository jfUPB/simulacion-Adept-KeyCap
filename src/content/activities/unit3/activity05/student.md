- Según lo que he comprendido con respecto a las leyes de Newton, y como se explica en el enunciado de este punto, la acerelación equivale a la sumatoria de las fuerzas.
- En el código propuesto no veo que se estén sumando las fuerzas, por lo contrario se están reemplazando una a otra, la fuerza ```wind``` se está sobrescribiendo por la fuerza ```gravity```.

```js
// Función dentro del la clase Mover.js
ApplyForce(force){
  this.acceleration.Add(force)
}

//Update en el Sketch.js
Update{
  mover.ApplyForce(gravity)
  mover.ApplyForce(wind)
}
```

