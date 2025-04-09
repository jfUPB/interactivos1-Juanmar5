## Explicación del código
##### Importación Módulos
- from microbit import *: Importa todas las funciones necesarias para interactuar con el hardware del micro:bit, como la pantalla LED (display).
- import utime: Se usa para manejar el tiempo y medir intervalos en milisegundos.
  
##### Definición clase Pixel
- pixelX y pixelY: Coordenadas del píxel en la matriz 5x5.
- initState: Estado inicial del píxel (brillo entre 0 y 9).
- interval: Tiempo en milisegundos para alternar su estado.
- .
- self.state: Controla en qué fase del ciclo está (Init o WaitTimeout).
- self.startTime: Guarda el tiempo en que el píxel cambia de estado.
- self.interval: Define cuánto tarda en cambiar su estado.
- self.pixelState: Indica el brillo del píxel (0 = apagado, 9 = máximo brillo).
  
##### Método Update()
###### Fase de inicialización
- Si el píxel está en el estado "Init", se inicializa el temporizador (startTime).
- Cambia a "WaitTimeout", indicando que ahora está esperando el siguiente cambio.
- Dibuja el píxel en la pantalla con el brillo inicial.
###### Fase de espera y parpadeo
- Calcula cuánto tiempo ha pasado desde el último cambio.
- Si ha pasado el intervalo, cambia el brillo del píxel.
- Si el píxel está en brillo máximo (9), se apaga (0), y viceversa.
- Se actualiza en la matriz LED.

##### Creación de objetos Pixel
- Se crean dos píxeles
- Uno en la esquina superior izquierda (0,0), parpadea cada 1 segundo.
- Otro en la esquina inferior derecha (4,4), parpadea cada 0.5 segundos.

##### Bucle principal (while True)
- Llama al método update() de cada píxel en un bucle infinito.
- Cada píxel parpadea de forma independiente con su propio tiempo.


## Estados
##### Init:
- Estado inicial en el que el píxel se configura por primera vez.
- En este estado, el programa espera para registrar el tiempo actual y encender el píxel.
##### WaitTimeout:
- Estado en el que el programa espera a que pase el intervalo de tiempo antes de cambiar el estado del píxel.
- En este estado, el programa constantemente verifica si ha pasado el tiempo necesario antes de cambiar el brillo del píxel.


## Eventos
##### Paso del tiempo (utime.ticks_diff(utime.ticks_ms(), self.startTime) > self.interval):
- Ocurre en el estado "WaitTimeout".
- Se verifica si ha pasado el tiempo especificado en self.interval.
- Si el tiempo ha transcurrido, se activa un cambio de estado en el píxel.


## Acciones
##### Encender el píxel con display.set_pixel(self.pixelX, self.pixelY, self.pixelState)
- Ocurre en el estado "Init".
- Se activa cuando el programa inicializa un píxel por primera vez.
##### Alternar el estado del píxel entre apagado (0) y encendido (9)
- Ocurre en el estado "WaitTimeout" cuando ha pasado el intervalo de tiempo.
- Si el píxel está encendido, se apaga; si está apagado, se enciende.
- Luego, se actualiza la pantalla con display.set_pixel().
