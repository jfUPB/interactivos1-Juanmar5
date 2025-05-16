- https://editor.p5js.org/Juanmar5/sketches/fc81MhnCh
-  Código:
```
'use strict';

var shapes = [];
var newShape;

var joints = 6;
var linelength = 64;
var resolution = 0.06;
var gravity = 0.094;
var damping = 0.95;

var showPath = true;
var showPendulum = true;
var showPendulumPath = true;
var clearScreen = false;

let port;
let connectBtn;
let microBitConnected = false;

let microBitX = 0;
let microBitY = 0;
let microBitAState = false;
let microBitBState = false;
let prevA = false;
let prevB = false;

let serialBuffer = [];

function setup() {
  createCanvas(windowWidth, windowHeight);
  colorMode(HSB, 360, 100, 100, 100);
  noFill();
  strokeWeight(1);

  port = createSerial();
  connectBtn = createButton("Conectar micro:bit");
  connectBtn.position(10, 10);
  connectBtn.mousePressed(() => {
    if (!port.opened()) {
      port.open("MicroPython", 115200);
    } else {
      port.close();
    }
  });
}

function draw() {
  if (clearScreen) background(0, 0, 100);

  if (port.opened() && port.availableBytes() > 0) {
    readSerialData();
  }

  shapes.forEach(s => {
    s.draw();
    s.update();
  });

  if (newShape) {
    newShape.addPos(microBitX, microBitY);
    newShape.draw();
    newShape.update();
  }
}

function readSerialData() {
  // Leer un byte por frame para evitar bloqueos
  let byte = port.read();
  if (typeof byte === "number") {
    serialBuffer.push(byte);
  }

  // Procesar paquetes binarios de 8 bytes (con encabezado 0xAA y checksum)
  while (serialBuffer.length >= 8) {
    if (serialBuffer[0] !== 0xAA) {
      serialBuffer.shift();
      continue;
    }

    let frame = serialBuffer.slice(0, 8);
    let x = (frame[1] << 8) | frame[2];
    let y = (frame[3] << 8) | frame[4];
    let a = frame[5];
    let b = frame[6];
    let checksum = frame[7];

    let sum = (frame[1] + frame[2] + frame[3] + frame[4] + a + b) & 0xFF;

    if (sum === checksum) {
      x = x > 32767 ? x - 65536 : x;
      y = y > 32767 ? y - 65536 : y;

      microBitX = map(x, -1024, 1024, 0, width);
      microBitY = map(y, -1024, 1024, 0, height);
      microBitAState = a === 1;
      microBitBState = b === 1;

      if (microBitAState && !prevA) {
        newShape = new Shape(color(random(360), 80, 60, 50));
        newShape.addPos(microBitX, microBitY);
      }

      if (!microBitAState && prevA && newShape) {
        shapes.push(newShape);
        newShape = undefined;
      }

      prevA = microBitAState;
      prevB = microBitBState;

      serialBuffer.splice(0, 8);
    } else {
      serialBuffer.shift(); // descartar encabezado inválido
    }
  }
}

// ---------- Clases Shape y Pendulum ----------

function Shape(pendulumPathColor) {
  this.shapePath = [];
  this.pendulumPath = [];
  this.pendulumPathColor = pendulumPathColor;
  this.iterator = 0;
  this.linelength = linelength;
  this.resolution = resolution;
  this.pendulum = new Pendulum(this.linelength, joints);

  this.addPos = function(x, y) {
    this.shapePath.push(createVector(x, y));
  };

  this.draw = function() {
    strokeWeight(0.8);
    stroke(0, 10);

    if (showPath) {
      beginShape();
      this.shapePath.forEach(pos => vertex(pos.x, pos.y));
      endShape();
    }

    if (this.iterator < this.shapePath.length) {
      let i = floor(this.iterator);
      let currentPos = this.shapePath[i];
      let prevPos = this.shapePath[i - 1];
      if (prevPos) {
        let offset = p5.Vector.lerp(prevPos, currentPos, this.iterator - i);
        let heading = atan2(currentPos.y - prevPos.y, currentPos.x - prevPos.x) - HALF_PI;

        push();
        translate(offset.x, offset.y);
        this.pendulum.update(heading);
        if (showPendulum) this.pendulum.draw();
        pop();

        this.pendulumPath.push(this.pendulum.getTrail(offset));
      }
    }

    if (showPendulumPath) {
      strokeWeight(1.6);
      stroke(this.pendulumPathColor);
      beginShape();
      this.pendulumPath.forEach(pos => vertex(pos.x, pos.y));
      endShape();
    }
  };

  this.update = function() {
    this.iterator += this.resolution;
    this.iterator = constrain(this.iterator, 0, this.shapePath.length);
  };
}

function Pendulum(size, hierarchy) {
  this.hierarchy = hierarchy - 1;
  this.size = size;
  this.angle = random(TAU);
  this.origin = createVector(0, 0);
  this.end = createVector(0, 0);
  this.gravity = gravity;
  this.damping = damping;
  this.angularAcceleration = 0;
  this.angularVelocity = 0;
  this.pendulumArm = this.hierarchy > 0 ? new Pendulum(this.size / 1.5, this.hierarchy) : null;

  this.update = function(heading) {
    this.end.set(this.origin.x + this.size * sin(this.angle), this.origin.y + this.size * cos(this.angle));
    this.angularAcceleration = (-this.gravity / this.size) * sin(this.angle + heading);
    this.angle += this.angularVelocity;
    this.angularVelocity += this.angularAcceleration;
    this.angularVelocity *= this.damping;

    if (this.pendulumArm) this.pendulumArm.update(heading);
  };

  this.getTrail = function(offset, end = null) {
    if (this.pendulumArm) {
      if (end) end.add(this.end);
      else end = this.end.copy();
      return this.pendulumArm.getTrail(offset, end);
    } else {
      return this.end.copy().add(end).add(offset);
    }
  };

  this.draw = function() {
    stroke(0, 40);
    line(this.origin.x, this.origin.y, this.end.x, this.end.y);
    fill(0, 20);
    ellipse(this.end.x, this.end.y, 2, 2);
    noFill();
    if (this.pendulumArm) {
      push();
      translate(this.end.x, this.end.y);
      this.pendulumArm.draw();
      pop();
    }
  };
}

function keyPressed() {
  if (key === 's' || key === 'S') saveCanvas('pendulum', 'png');
  if (keyCode === DELETE || keyCode === BACKSPACE) {
    shapes = [];
    newShape = undefined;
    background(0, 0, 100);
  }
  if (keyCode === UP_ARROW) linelength += 2;
  if (keyCode === DOWN_ARROW) linelength -= 2;
  if (keyCode === LEFT_ARROW) joints = max(1, joints - 1);
  if (keyCode === RIGHT_ARROW) joints++;
  if (key === '1') showPath = !showPath;
  if (key === '2') showPendulum = !showPendulum;
  if (key === '3') showPendulumPath = !showPendulumPath;
  if (key === '4') clearScreen = !clearScreen;
  if (key === '-') gravity -= 0.001;
  if (key === '+') gravity += 0.001;
}
```
- https://editor.p5js.org
