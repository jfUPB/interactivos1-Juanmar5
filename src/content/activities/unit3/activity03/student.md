## WIP, le falta trabajo a esto

``` micro python

from microbit import *
import music

# Variables globales
estado = "CONFIGURACION"
tiempo = 20
sequence = ["A", "B", "A", "S"]
input_sequence = []

# Variables de eventos
evento_recibido = False  # Indica si hay un evento pendiente
evento = ""  # Almacena el evento recibido


def mostrar_tiempo():
    display.show(str(tiempo))


def resetear():
    global estado, tiempo, input_sequence
    estado = "CONFIGURACION"
    tiempo = 20
    input_sequence = []
    display.clear()


def tareaEventos():
    """Detecta eventos de botones, shake o del puerto serial y los almacena."""
    global evento_recibido, evento

    if button_a.was_pressed():
        evento = "A"
        evento_recibido = True
    elif button_b.was_pressed():
        evento = "B"
        evento_recibido = True
    elif accelerometer.was_gesture("shake"):
        evento = "S"
        evento_recibido = True

    # Leer desde el puerto serial
    mensaje = uart.read()
    if mensaje:  # Verifica que no sea None
        mensaje = mensaje.decode().strip()
        if mensaje in ["A", "B", "S", "T"]:
            evento = mensaje
            evento_recibido = True


def tareaBomba():
    """Gestiona la lógica de la bomba basándose en eventos."""
    global estado, tiempo, evento_recibido, evento

    if estado == "CONFIGURACION":
        mostrar_tiempo()

        if evento_recibido:
            if evento == "A" and tiempo < 60:
                tiempo += 1
            elif evento == "B" and tiempo > 10:
                tiempo -= 1
            elif evento == "S":
                estado = "CUENTA_REGRESIVA"
                display.show(Image.SKULL)
                sleep(1000)
                display.clear()

        evento_recibido = False  # Consumir el evento

    elif estado == "CUENTA_REGRESIVA":
        if evento_recibido:
            input_sequence.append(evento)
            if len(input_sequence) > len(sequence):
                input_sequence.pop(0)
            if input_sequence == sequence:
                resetear()

        evento_recibido = False  # Consumir el evento

        if tiempo > 0:
            mostrar_tiempo()
            sleep(1000)
            tiempo -= 1
        else:
            estado = "EXPLOSION"

    elif estado == "EXPLOSION":
        display.show(Image.NO)
        music.play(music.WAWAWAWAA)
        sleep(2000)
        resetear()


# Habilitar la comunicación serial
uart.init(baudrate=115200)

while True:
    tareaEventos()
    tareaBomba()
```
