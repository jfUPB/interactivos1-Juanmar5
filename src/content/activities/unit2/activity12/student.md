Código:

``` micropython

from microbit import *


# Estado inicial y variables
estado = "CONFIGURACION"
tiempo = 20 

def mostrar_tiempo():
    display.show(str(tiempo)[-1])


while True:
    if estado == "CONFIGURACION":
       mostrar_tiempo()

    if button_a.was_pressed() and tiempo < 60:
        tiempo += 1
    if button_b.was_pressed() and tiempo > 10:
        tiempo -= 1

    if accelerometer.was_gesture("shake"):
        estado = "CUENTA_REGRESIVA"
        display.show(Image.SKULL)
        sleep(1000)

    elif estado == "CUENTA_REGRESIVA":
        while tiempo > 0:
            display.show(str(tiempo)[-1])
            sleep(1000)
            tiempo -= 1

    if button_a.was_pressed():
        estado = "CONFIGURACION"
        break
        
    if tiempo == 0:
        estado = "EXPLOSION"

    elif estado == "EXPLOSION":
        display.show(Image.NO)
        sleep(2000)
        estado = "CONFIGURACION"
```


Link: https://youtube.com/shorts/-ykP24mxN5g?si=dxcBM6qvi2GGSoxL
