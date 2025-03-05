### Solución

Tras "cacharrear" un poco, descubrí que la solución estaba en el editor de Python, así que primero edité eso para que mostrara más imágenes con los botones y el agitamiento

``` python
from microbit import *

uart.init(baudrate=115200)
display.show(Image.BUTTERFLY)

while True:
    if button_a.is_pressed():
        uart.write('A')
        display.show(Image.PACMAN)
        sleep(500)
    if button_b.is_pressed():
        uart.write('B')
        display.show(Image.SILLY)
        sleep(500)
    if accelerometer.was_gesture('shake'):
        uart.write('C')
        display.show(Image.DUCK)
        sleep(500)
        sleep(500)
    if uart.any():
        data = uart.read(1)
        if data:
            if data[0] == ord('h'):
                display.show(Image.HEART)
                sleep(500)
               
```

Después de eso ya iban 3 imágenes, para la última solo volví a utilizar el botón de "Send Love" de antes

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
    let sendBtn = createButton('Send Love');
    sendBtn.position(220, 300);
    sendBtn.mousePressed(sendBtnClick);
    fill('white');   
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
    port.write('h');
}
```
