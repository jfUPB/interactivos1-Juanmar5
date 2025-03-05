
``` python
from microbit import *
import utime
import neopixel
np = neopixel.NeoPixel(pin0, 8)
np[0] = (255, 0, 0)
np[1] = (255, 255, 0)
np[2] = (0, 255, 0)



class NeoPixel:
        estado = 'Rojo'
    while True:
        if estado == "Rojo":
            np[0] = (255, 0, 0)
            np.sow()
            display.show(Image.NO)
            sleep(1000)
            estado = 'Amarillo'

        if estado == "Amarillo":
            np[1] = (255, 255, 0)
            np.show()
            display.show(Image.ASLEEP)
            sleep(1000)
            estado = 'Verde'
            
        if estado == "Verde":
            np[1] = (255, 255, 0)
            np.show()
            display.show(Image.YES)
            sleep(3000)
            estado = 'Rojo'
```
