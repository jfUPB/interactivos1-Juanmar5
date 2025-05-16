
## Tabla comparativa

| Aspecto              | Protocolo ASCII                                           | Protocolo Binario                                                                                 |
| -------------------- | --------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |                                               
| **Velocidad**        | Más lento porque convierte texto a números.               | Más rápido. Los datos llegan como enteros listos para usar                                        |
| **Facilidad**        | Más fácil de entender para principiantes.                 | Más difícil por el manejo que pide.                                                               |


## Preguntas teóricas y prácticas

### ¿Por qué fue necesario introducir framing en el protocolo binario?

Porque en binario no están los separadores de ASCII como las comas entonces no sabríamos de dónde a dónde va cada línea. 


### ¿Cómo funciona el framing?

Pone un encabezado al inicio de cada paquete y un checksum al final. para procesarlo mejor y como uno solo.


### ¿Qué es un carácter de sincronización?

Es un byte que indica el inicio de un paquete de datos.


### ¿Qué es el checksum y para qué sirve?

Como un valor que suma los bytes para verificar si se envió bien un paquete.


### ¿Qué hace `concat` y por qué?

`concat()` une el contenido al final del buffer para acumularlos en orden.


### ¿Por qué se recorre el buffer solo si tiene 8 o más bytes?

Porque un paquete completo tiene 8 bytes, si hay menos puede que hayan menos datos.


### ¿Qué significa `0xAA`?

Es un valor hexadecimal


### ¿Qué hace `shift()` y la instrucción `continue`? ¿Por qué?

shift() elimina el primer byte del buffer.
continue salta al siguiente ciclo del bucle.


### ¿Qué hace `break` si hay menos de 8 bytes?

Detiene el bucle para esperar más datos


### ¿Diferencia entre `slice` y `splice`? ¿Por qué se usan ambas?

* slice copia los primeros 8 bytes
* splice elimina los bytes

Es para extraer el paquete y luego limpiar el buffer


### ¿Cómo opera `reduce` en esta línea?

recorre todos los valores de dataBytes y los suma


### ¿Por qué se compara el checksum enviado con el calculado?

Para detectar errores.


### ¿Qué hace la instrucción `continue` en ese contexto?

Salta al siguiente ciclo del bucle.


### ¿Qué es un `DataView`? ¿Para qué se usa?

DataView permite leer tipos de datos desde un binario


### ¿Por qué es necesario hacer estas conversiones?

Porque los datos recibidos se deben reconstruir para evitar corrupciones.


##### Mucho lo busqué, no recordaba la mayoría
