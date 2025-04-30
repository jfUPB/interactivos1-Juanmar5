### Vectores de prueba

descripción de errores encontrados y correcciones implementadas. 


### Código final corregido.

``` micropython
from microbit import *
import music


# Estado inicial y variables
estado = "CONFIGURACION"
tiempo = 20 

def mostrar_tiempo():
    display.show(str(tiempo)[-1])

def resetear():
    global estado, tiempo
    estado = "CONFIGURACION"
    tiempo = 20
    display.clear()


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
        if pin_logo.is_touched():
            resetear()
            
        if tiempo > 0:
            display.show(str(tiempo)[-1])
            sleep(1000)
            tiempo -= 1

        else:
            estado = "EXPLOSION"
        


    elif estado == "EXPLOSION":
        display.show(Image.NO)
        music.play(music.WAWAWAWAA)
        sleep(2000)
        resetear()

    if pin_logo.is_touched():
            resetear()
```
