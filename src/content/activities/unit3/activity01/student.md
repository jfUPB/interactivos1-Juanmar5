Código

``` micropython
from microbit import *
import utime
import music


STATE_ROJO = 0
STATE_AMARILLO = 1
STATE_AMARILLO2 = 2
STATE_VERDE = 3
STATE_INIT = 4

ROJO_INTERVAL = 1500
AMARILLO_INTERVAL = 1000
AMARILLO2_INTERVAL = 1000
VERDE_INTERVAL = 2000

current_state = STATE_INIT
start_time = 0
interval = 0

while True:
    # pseudoestado STATE_INIT
    if current_state == STATE_INIT:
        display.show(Image.HAPPY)
        start_time = utime.ticks_ms()
        interval = ROJO_INTERVAL
        current_state = STATE_ROJO
    if current_state == STATE_ROJO:
        if utime.ticks_diff(utime.ticks_ms(), start_time) > interval:
            # Acciones para el evento
            display.show(Image.NO)
            # Acciones de entrada para el siguiente estado
            start_time = utime.ticks_ms()
            interval = AMARILLO_INTERVAL
            current_state = STATE_AMARILLO
    elif current_state == STATE_AMARILLO:
        if utime.ticks_diff(utime.ticks_ms(), start_time) > interval:
            display.show(Image.MEH)
            start_time = utime.ticks_ms()
            interval = VERDE_INTERVAL
            current_state = STATE_VERDE
    elif current_state == STATE_VERDE:
        if utime.ticks_diff(utime.ticks_ms(), start_time) > interval:
            display.show(Image.YES)
            start_time = utime.ticks_ms()
            interval = AMARILLO2_INTERVAL
            current_state = STATE_AMARILLO2
    elif current_state == STATE_AMARILLO2:
        if utime.ticks_diff(utime.ticks_ms(), start_time) > interval:
            display.show(Image.MEH)
            start_time = utime.ticks_ms()
            interval = ROJO_INTERVAL
            current_state = STATE_ROJO
```
