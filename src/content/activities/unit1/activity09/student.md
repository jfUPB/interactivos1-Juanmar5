
``` js

function setup() {
  createCanvas(600, 600);
  noStroke();
}

function draw(){
  background(0);

  for (i = 0; i < 20; i++) {
  fill(random(100, 255), random(100, 255), random(100, 255));
  ellipse(random(0, width), random(0, height), random(30, 100), 100);
  }
  
}

```
