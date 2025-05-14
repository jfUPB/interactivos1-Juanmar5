### Describe cómo se están comunicando el micro\:bit y el sketch de p5.js. ¿Qué datos envía el micro:bit?
El micro:bit se comunica con el sketch de p5 por el puerto serial 
Envía cuatro datos: el valor del acelerómetro en X, el valor en Y, y los estados de los botones A y B todo en ASCII


### ¿Cómo es la estructura del protocolo ASCII usado?
El micro:bit forma un string con los datos separados por comas y lo termina con un carácter de nueva línea (`\n`). 


### Muestra y explica la parte del código de p5.js donde lee los datos del micro\:bit y los transforma en coordenadas de la pantalla.

```javascript
if (port.availableBytes() > 0) {
  let data = port.readUntil("\n");
  if (data) {
    data = data.trim();
    let values = data.split(",");
    if (values.length == 4) {
      microBitX = int(values[0]) + windowWidth / 2;
      microBitY = int(values[1]) + windowHeight / 2;
      microBitAState = values[2].toLowerCase() === "true";
      microBitBState = values[3].toLowerCase() === "true";
      updateButtonStates(microBitAState, microBitBState);
    }
  }
}
```

Aquí se espera que haya datos disponibles, se leen hasta el salto de línea, se eliminan espacios, 
se separan por comas y se convierten los valores a números o booleanos. Las coordenadas X e Y se ajustan sumando la mitad del ancho/alto 
de la ventana para centrar el dibujo.


### ¿Cómo se generan los eventos A pressed y B released que se generan en p5.js a partir de los datos que envía el micro:bit?
En la función `updateButtonStates()`, se compara el estado actual de los botones con su estado anterior. 
Si A pasa de `false` a `true`, se interpreta como un "A pressed". Si B pasa de `true` a `false`, se detecta como "B released". 


### Capturas de pantalla de algunos dibujos que hayas hecho con el sketch.
Imagen adjunta en assets como U5A1.
