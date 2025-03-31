### Código de p5.js

``` js
let estado = "CONFIGURACION";
let tiempo = 20;
let sequence = ["A", "B", "A", "S"];
let input_sequence = [];
let port;

function setup() {
    createCanvas(400, 400);
    background(220);

    port = createSerial();
    port.open('MicroPython', 115200);

    textSize(20);
    textAlign(CENTER, CENTER);
}

function draw() {
    background(220);
    text("Estado: " + estado, width / 2, 50);
    text("Tiempo: " + tiempo, width / 2, 100);

    if (estado === "CUENTA_REGRESIVA") {
        if (tiempo > 0) {
            tiempo -= 1;
            setTimeout(() => {}, 1000);
        } else {
            estado = "EXPLOSION";
        }
    }

    if (estado === "EXPLOSION") {
        text("💥 EXPLOSIÓN 💥", width / 2, height / 2);
        setTimeout(() => resetear(), 2000);
    }
}

function serialEvent() {
    let data = port.read();
    if (data) {
        data = data.trim();
        procesarEvento(data);
    }
}

function procesarEvento(evento) {
    if (estado === "CONFIGURACION") {
        if (evento === "A" && tiempo < 60) tiempo++;
        if (evento === "B" && tiempo > 10) tiempo--;
        if (evento === "S") estado = "CUENTA_REGRESIVA";
    } else if (estado === "CUENTA_REGRESIVA") {
        input_sequence.push(evento);
        if (input_sequence.length > sequence.length) {
            input_sequence.shift();
        }
        if (JSON.stringify(input_sequence) === JSON.stringify(sequence)) {
            resetear();
        }
    }
}

function resetear() {
    estado = "CONFIGURACION";
    tiempo = 20;
    input_sequence = [];
}
```
````
