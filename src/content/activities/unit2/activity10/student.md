### Explicación
- A través de estados e intervalos, logramos que pasivamente se esté generando ese patrón de tiempo
- En la condicional del intervalo, también tenemos que se force un estado distinto al presionar el botón que corresponde al intervalo que le precede al actual
- Se logra hacer ambas cosas a la vez porque una es por medio de la no interacción mientras que la otra sí y lo que hace es devolver la secuencia, no cerrarla ni interrumpirla

### 3 Vectores de Prueba:
- Presionar A cuando STATE_HAPPY = STATE_SAD
- Presionar A cuando STATE_SMILE = STATE_HAPPY
- NO Presionar A cuando STATE_SAD = STATE_HAPPY
