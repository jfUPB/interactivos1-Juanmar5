### Mi código:

``` python
from microbit import *

uart.init(baudrate=115200)
display.show(Image.BUTTERFLY)

while True:
    if button_a.is_pressed():
        uart.write('A')
        display.scroll('waka')
        display.show(Image.PACMAN)
        sleep(1000)
    if button_b.is_pressed():
        uart.write('B')
        display.scroll('casa')
        display.show(Image.HOUSE)
        sleep(1000)
    if pin_logo.is_touched():
        display.scroll(1)
        display.show(Image.HEART)
        sleep(1000)
    if accelerometer.is_gesture('shake'):
        display.scroll('hola')
        sleep(1000)
```

### Explicación:
Básicamente 
- El presionar el botón A hará que el display muestre la palabra "waka" con la imagen de un Pac-Man.
- El B Presentará "casa" con la imagen de una casa
- El toque del logo mostrará el número 1 y un corazón
- Agitar el micro:bit mostrará la plabra "hola"
