## Código


``` javascript
let port;
let connectBtn;

function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(60, 300);
    connectBtn.mousePressed(connectBtnClick);
    let ABtn = createButton('A');
    ABtn.position(220, 300);
    ABtn.mousePressed(ABtnClick);
    let BBtn = createButton('B');
    BBtn.position(260, 300);
    BBtn.mousePressed(BBtnClick);
    let SBtn = createButton('S');
    SBtn.position(300, 300);
    SBtn.mousePressed(SBtnClick);
    let TBtn = createButton('T');
    TBtn.position(340, 300);
    TBtn.mousePressed(TBtnClick);
    fill('white');
    ellipse(width / 2, height / 2, 100, 100);
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

function ABtnClick() {
    port.write('A');
}

function BBtnClick() {
    port.write('B');
}

function SBtnClick() {
    port.write('S');
}

function TBtnClick() {
    port.write('T');
}
```
