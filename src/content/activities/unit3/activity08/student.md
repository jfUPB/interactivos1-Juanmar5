### Código para Microbit Pyhton

``` python
from microbit import *
import uart

# Iniciar comunicación serial
uart.init(baudrate=115200)

while True:
    if button_a.was_pressed():
        uart.write("A\n")
    if button_b.was_pressed():
        uart.write("B\n")
    if accelerometer.was_gesture("shake"):
        uart.write("S\n")
    if pin_logo.is_touched():
        uart.write("T\n")

    sleep(100)
```
