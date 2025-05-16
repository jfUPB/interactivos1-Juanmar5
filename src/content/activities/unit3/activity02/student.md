## Código

``` micropython
from microbit import *
import music

estado = "CONFIGURACION"
tiempo = 20
sequence = ["A", "B", "A", "SHAKE"]
input_sequence = []

def mostrar_tiempo():
    display.show(str(tiempo)) 
def resetear():
    global estado, tiempo, input_sequence
    estado = "CONFIGURACION"
    tiempo = 20
    input_sequence = []  # Reinicia secuencia
    display.clear()

while True:
    if estado == "CONFIGURACION":
        mostrar_tiempo()

        if button_a.was_pressed() and tiempo < 60:
            tiempo += 1
            sleep(200)  # Pequeña pausa para evitar registros dobles

        if button_b.was_pressed() and tiempo > 10:
            tiempo -= 1
            sleep(200)

        if accelerometer.was_gesture("shake"):
            estado = "CUENTA_REGRESIVA"
            display.show(Image.SKULL)
            sleep(1000)
            display.clear()

    elif estado == "CUENTA_REGRESIVA":
        while tiempo > 0:  
            if button_a.was_pressed():
                input_sequence.append("A")
                sleep(200)
            if button_b.was_pressed():
                input_sequence.append("B")
                sleep(200)
            if accelerometer.was_gesture("shake"):
                input_sequence.append("SHAKE")
                sleep(200)

            if len(input_sequence) > len(sequence):
                input_sequence.pop(0)

            # Verificar secuencia
            if input_sequence == sequence:
                resetear()
                break  # Salir del bucle de cuenta regresiva

           
            mostrar_tiempo()
            sleep(1000)
            tiempo -= 1

        if tiempo == 0:
            estado = "EXPLOSION"

    elif estado == "EXPLOSION":
        display.show(Image.NO)
        music.play(music.WAWAWAWAA)
        sleep(2000)
        resetear()
```

## Explicación
- Se creó un input sequence con valores que corresponden a las entradas de cada botón y un índice que indique que la secuencia es A-B-A-Shake
- Se verifica que la secuencia ingresada corresponda a la esperada, si sí, se invoca la funcioón 'resetear'
