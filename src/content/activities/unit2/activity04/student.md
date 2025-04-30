### ¿Qué querías comprobar?
Cómo puedo verificar qué botón (o el logo) está siendo presionado en el micro:bit?
### ¿Cuál fue tu hipótesis?
En el editor de Python se podría hacer que presionar los botones A y B generen una imagen que se muestre con las luces del micro:bit y otra imagen con el toque del logo, así poder conocer qué se está presionado y cómo afecta al micro:bit.
Si yo pidiera que se evoque una imagen o figura a través de la lectura de cada entrada, podría comprobar que sus estados son funcionales.
### Los códigos involucrados en el experimento
``` python
from microbit import *

uart.init(baudrate=115200)
display.show(Image.BUTTERFLY)

while True:
    if button_a.is_pressed():
        uart.write('A')
        display.show(Image.ANGRY)
        sleep(1000)
    if button_b.is_pressed():
        uart.write('B')
        display.show(Image.HOUSE)
        sleep(1000)
    if pin_logo.is_touched():
        display.show(Image.HEART)
        sleep(1000)
```
### Descripción de lo resultados
Al presionar el botón A, se muestra en las luces LED una cara presuntamente enojada, al presionar el botón B, se muestra una casita y al tocar el logo superior se muestra un corazón
### Análisis de esos resultados
Efectivamente, cada entrada invoca la función que se le indicó en el código, lo que marcaría sus estados como funcionales.
### Conclusiones
Es por mínimo curioso cómo funciona el logo, se puede decir que es bastante sensible a cualquier toque pero muy interesante que sea capaz de proveer una entrada adicional a las análogas de los botones, se siente
como un toque más digital lo cual es muy interesante. Se puede concluir igual que todas las entradas funcionan correctamente como deberían.
