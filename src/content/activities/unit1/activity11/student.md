### Mi Código

``` js


let port;
let connectBtn;
let x = 200;

function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);
    fill('white');
    ellipse(x, 200, 50, 50);
    x = constrain(x, 25, 375);
}

function draw() {

    if(port.availableBytes() > 0){
        let dataRx = port.read(1);
        if(dataRx == 'A'){
            fill('pink');
            x -= 10;
        }
        else if(dataRx == 'B'){
            fill('lime');
            x += 10;
        }
        background(220);
        ellipse(x, 200, 50, 50);
    }


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
```
