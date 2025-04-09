### Mi código:

``` python
from microbit import *
import music

uart.init(baudrate=115200)
display.show(Image.BUTTERFLY)

while True:
    if button_a.is_pressed():
        uart.write('A')
        music.play(music.PUNCHLINE)
        sleep(1000)
    if button_b.is_pressed():
        uart.write('B')
        music.play(music.NYAN)
        sleep(1000)
```

### Explicación:
- Se importa la librería 'music'
- Presionar el botón A hará sonar sonar ese sonidito de punchline de series animadas
- El B hará sonar la musiquita del Nyan Cat
