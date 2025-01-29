
``` js

function setup() {
  createCanvas(600, 600);
  noStroke();
}

function draw(){
  background(0);

  
  fill(random(100, 255), random(100, 255), random(100, 255));
  ellipse(width / random(1, 5), height / random(1, 5), random(100, 200), random(100, 200));
  
}

```
