## Preguntas


### ¿Por qué antes necesitábamos delimitadores y saltos de línea, y ahora no?
Porque se usa un paquete binario con tamaño fijo, por lo que no es necesario separar ni marcar los datos


### Compara el código de la unidad anterior con este. ¿Qué cambios ves?
- Lectura binaria – Se reemplaza el uso de texto por datos binarios usando DataView.
- Buffer de recepción – Se agrega un serialBuffer[] para manejar posibles fragmentaciones en la recepción.
- Framing + checksum – Se implementa framing (0xAA) y verificación de integridad con checksum.


### ¿Qué ves en la consola? ¿Por qué crees que se produce este error?
Podría ocurrir porque se están leyendo 6 bytes en el momento incorrecto.



### ¿Qué cambios tienen los programas y ¿Qué puedes observar en la consola del editor de p5.js?
El nuevo código reemplaza la lectura textual de líneas con comas por un manejo binario robusto con readSerialData(), 
usando serialBuffer, validación de encabezado 0xAA, y verificación de checksum.
Elimina Split y Trim así como el mensaje de que no hay datos recibidos del micro:bit.


- Adjunta imagen U5A3
