## Preguntas


### ¿Qué es un protocolo de comunicación y por qué es importante en la comunicación serial?
   Reglas que definen cómo se envían y reciben datos para mejor comunicación.

### ¿Por qué se separan los datos con comas en el protocolo ASCII que exploramos?
   Para poder identificar y cada dato individual.

### ¿Por qué es necesario terminar los datos con un carácter que marque el fin del mensaje?
   Para que el receptor procese bien el mensae.

### ¿Por qué fue necesario usar una máquina de estados en la aplicación modificada de p5.js?
   Para controlar el comportamiento del sistema organizadamente en partes como espera y dibujo
```
function updateButtonStates(newAState, newBState) {
  // Generar eventos de keypressed
  if (newAState === true && prevmicroBitAState === false) {
    // create a new random color and line length
    lineModuleSize = random(50, 160);
    // remember click position
    clickPosX = microBitX;
    clickPosY = microBitY;
    print("A pressed");
  }
  // Generar eventos de key released
  if (newBState === false && prevmicroBitBState === true) {
    c = color(random(255), random(255), random(255), random(80, 100));
    print("B released");
  }

  prevmicroBitAState = newAState;
  prevmicroBitBState = newBState;
}
```

### ¿Cómo se formatean los datos en el micro:bit para ser enviados por el puerto serial?
   Se convierten en texto (string) separados por comas y terminados con (`\n`).

### ¿Por qué es necesario en la aplicación de p5.js preguntar si hay bytes disponibles en el puerto serial antes de leerlos?
   Para evitar leer datos incompletos o vacíos.

### ¿Qué pasa si esto no se hace?
   El programa podría fallar por hacer asunciones falsas o no ejecutar bien una función.

### ¿Cómo se elimina el retorno de carro o salto de línea de un string en p5.js?
   No recuerdo.

### Si una cadena tiene información separada por espacios y quieres dividir dicha información en varias cadenas individuales ¿Qué función de p5.js usarías?
   split.

### ¿Por qué es necesario en la aplicación del caso de estudio convertir las cadenas a números enteros antes de usarlas en el sketch de p5.js?
   Para que no sea texto.

### Si el micro\:bit tiene los siguientes datos xValue: 123, yValue: 756, aState: False, bState: True ¿Qué bytes se enviarían por el puerto serial?
   `"123,756,0,1\n"`.

### ¿Qué aprendiste nuevo del micro:bit que no sabías antes?   
   Que puede enviar datos por puerto serial en tiempo real y modificar cómo se leen mientras se sigue ejecutando el código.

### ¿Qué aprendiste nuevo de p5.js que no sabías antes?
   Cómo recibir y procesar datos seriales para controlar animaciones o comportamientos interactivos desde externos.
