#### ¿Qué información se está enviando? ¿Cómo se está enviando?

- xValue: inclinación en el eje X
- yValue: inclinación en el eje Y
- aState: estado del botón A (presionado = True, no presionado = False)
- bState: estado del botón B (igual que el anterior)
- Se envía como texto en formato CSV, por el puerto serial (UART).

#### ¿Qué significa esta parte?
``` 
"{},{},{},{}\n".format(xValue, yValue, aState,bState)
```
Crea una cadena con los cuatro valores, separados por comas y terminada en salto de línea (\n). 

#### ¿Qué ves en SerialTerminal?
Se ven líneas como:
```
-47,127,False,False
-48,128,True,False
```
Cada línea representa una "muestra" de datos enviada cada 100 ms.

#### ¿Por qué comas y salto de línea?
- Comas: separan los datos para que sea fácil dividirlos al recibirlos.
- Salto de línea: indica el fin de cada conjunto de datos.

#### ¿Qué pasaría sin comas ni salto de línea?
- Los datos se mezclarían y serían difíciles de interpretar.
- No se podría leer bien cuándo termina una línea.

#### ¿Para qué sirve sleep(100)?
- Envía datos 10 veces por segundo, sin eso se enviarían demasiados datos a la vez.

#### ¿Qué valores toman aState y bState?
- true si el botón está presionado, false si no.

#### Cambiar is_pressed() con was_pressed()
- Con is_pressed() se mantiene en true mientras se presiona mientras que con was_pressed(): solo da true una vez, cuando se detectó la pulsación.

#### Bytes enviados con xValue: 969, yValue: 652:
- xValue: 969
- yValue: 652
- aState: True
- bState: False
