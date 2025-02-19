### Mi proceso
Lo primero que hice para este ejercicio fue declarar el puerto 'e' en el editor de Python utilizando como plantilla el ejercicio de la unidad 1, esta vez pidiendo que muestre un fantasma
``` python
from microbit import *

uart.init(baudrate=115200)
display.show(Image.BUTTERFLY)

while True:
    if uart.any():
        data = uart.read(1)
        if data:
            if data[0] == ord('e'):
                display.show(Image.GHOST)
                sleep(1000)
```

Posteriormente, fui al editor de javascript, donde utilizando la plantilla anterior del ejercicio, cambié la variable de 'sendBtn' para que mostrara el texto "Send Ghost" y que invocara la función del puerto 'e'

``` javascript
let port;
let connectBtn;

function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);
    let sendBtn = createButton('Send Ghost');
    sendBtn.position(220, 300);
    sendBtn.mousePressed(sendBtnClick);
}

function draw() {


    if (!port.opened()) {
        connectBtn.html('Connect to micro:bit');
    }
    else {
        connectBtn.html('Disconnect');
    }
}

function connectBtnClick() {
    if (!port.opened()) {
        port.open('MicroPython', 115200);
    } else {
        port.close();
    }
}

function sendBtnClick() {
    port.write('e');
}
```

Tras probarlo, parece que sí funcionó
