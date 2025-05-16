## Preguntas



### ¿Por qué se ve este resultado (texto incomprensible al mostrar datos binarios como texto)?
Se ve como caracteres extraños porque los datos binarios no están diseñados para ser interpretados como texto ASCII. 
Los valores valor de 0 a 255 se representan como símbolos aleatorios cuando se muestran como texto.


### ¿Cómo está relacionado lo que ves en Hex con esta línea de código?:

```python
data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState))
```

Cada bloque de datos en hex representa los valores empaquetados por `struct`: 2 enteros cortos (2 bytes cada uno) y 
2 enteros sin signo (1 byte cada uno).


### ¿Qué ventajas y desventajas ves en usar un formato binario en lugar de texto en ASCII?
* **Ventajas:** más compacto, rápido de transmitir, ideal para comunicación en tiempo real.
* **Desventajas:** difícil de leer y depurar directamente, menos accesible sin herramientas apropiadas.


### ¿Cuántos bytes se están enviando por mensaje? ¿Cómo se relaciona esto con el formato '>2h2B'? ¿Qué significa cada uno de los bytes que se envían?
Se envían 6 bytes por mensaje: 4 bytes para `xValue` y `yValue` (2 bytes cada uno porque son enteros cortos) y 
2 bytes para `aState` y `bState` (1 byte cada uno). Cada byte representa una parte del dato.


### ¿Cómo se verían los números positivos y negativos (xValue, yValue) en el formato '>2h2B'?
Se verían como valores codificados en complemento a dos, que es la forma estándar de representar enteros con signo.


### ¿Qué diferencias ves entre los datos en ASCII y en binario? ¿Qué ventajas y desventajas ves en cada uno?
**Diferencias:**

* El ASCII es legible, ocupa más espacio, y cada número se representa como caracteres.
* El binario es compacto, ilegible directamente, y representa los datos como bytes puros.

**Ventajas binario:** más eficiente, ideal para transmisión rápida.
**Desventajas binario:** difícil de interpretar sin decodificación.
**Ventajas ASCII:** fácil de leer y depurar.
**Desventajas ASCII:** ocupa más espacio y requiere más procesamiento para parsear.



- Se adjuntaron en assets las imágenes como "U5A2-#"
