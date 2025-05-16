## Preguntas


#### ¿Qué notas de diferente respecto al caso de estudio original?
Este código utiliza los datos del microbit en un lienzo como antes pero parece que es con el microbit que se dibuja

#### ¿Para qué se usan las imágenes (SVGs)? ¿Qué representan?
Son módulos gráficos que en este caso son como brochas

#### ¿Qué pasaría si das click al botón?
Se conecta o desconecta del micro:bit a través del puerto serial.

#### ¿Por qué solo se leen datos si el puerto está abierto?
Porque port.readUntil("\n") solo puede ejecutarse si hay una conexión activa

#### ¿Podrías leer datos si el puerto está cerrado?
No, el puerto debe estar abierto para recibir información del micro:bit.

#### ¿Qué pasaría si el puerto está cerrado y el micro:bit envía datos?
Los datos se pierden; no hay ningún canal de comunicación abierto para recibirlos.

#### Según data = "{},{},{},{}\n".format(...): ¿Puedes verlo?
Sí, el micro:bit envía una línea con 4 valores separados por comas y terminada en \n, para facilitar su lectura.

#### ¿Qué pasaría si el micro:bit no envía el "\n"?
readUntil("\n") nunca finalizaría, el código no procesaría ni mostraría datos.

#### ¿Por qué se suma windowWidth/2 y windowHeight/2 a x e y?
Para centrar el sistema de coordenadas en el centro de la pantalla en lugar de la esquina superior izquierda.

#### ¿Cómo verificar que los eventos de keyPressed y keyReleased se generan?
Puede ver el cambio en color al soltar y se dibuja al presionar, además de los mensajes en la consola.

#### ¿Qué hace el algoritmo updateButtonStates?
Detecta los cambios en los botones A y B y genera acciones cuando cambian de estado (presión/liberación).

#### ¿Por qué es necesario almacenar el estado anterior de los botones?
Para detectar el cambio (transición) entre estados y no ejecutar acciones repetidamente mientras el botón está presionado.

#### ¿Qué pasaría si no se almacenara el estado anterior?
Los eventos se activarían continuamente cada frame, causando múltiples líneas o cambios de color excesivos, quizá mucho eso de la memoria también.

#### ¿Qué diferencias encuentras?
Este código no usa micro:bit ni puerto serial; todo se controla con el mouse y el teclado directamente desde la interfaz.

#### ¿Qué pasó con algunos eventos del mouse?
Se reemplazan por eventos del acelerómetro y botones del micro:bit.

#### ¿Qué pasó con la función relacionada con la barra de espacio del teclado?
Ahora está asignada a soltar el botón B.

#### Ejecuta la aplicación. Mira en la consola los mensajes que se generan. Nota en particular uno que dice: "No se están recibiendo 4 datos del micro:bit" ¿Qué significa esto?
Significa que el código espera recibir 4 valores separados por comas desde el micro:bit, pero está obteniendo menos.

#### ¿Este mensaje ocurre en varios frames o solo en uno? ¿Por qué?
Parece que solo en el primer frame.

#### ¿Qué puedes hacer para solucionar este problema?
Ignorar la primera línea o primer frame antes de que empiece a recibir datos
