### Programa 1


> https://openprocessing.org/sketch/2588357
- Parecen gusanitos de colores, es muy bonito
- Funciones de p5.js utilizadas: createCanvas(), createVector(x, y) y p5.Vector, random(), dist(x1, y1, x2, y2), map(), colorMode(HSB, 255), fill(), noStroke(), stroke(), windowWidth, windowHeight, width, height, etc.
- Técnicas de programación aplicadas: (POO) La clase Boid encapsula datos y comportamientos (como flock(), update(), display()), facilitando la gestión de múltiples entidades en movimiento.
- Cambios: Aumenté el tamaño del cuadrado de atracción y el tiempo que duran los pequeños 'renacuajos' atraídos al mismo
- https://editor.p5js.org/Juanmar5/sketches/kWIsImGtJ
``` p5
const attractionStrength = 1.3;
const attractionCycleLength = 300; // Frames for complete attraction cycle
let attractionCycleCounter = 0;

function setup() {
  createCanvas(min(windowWidth, windowHeight),min(windowWidth, windowHeight));
	pixelDensity(1);
  colorMode(HSB, 255);
  background(0);
  
  // Set up the attraction rectangle in the center
  attractionRect = {
    x: width * 1.5,
    y: height * 0.5,
    width: width * 0.6,
    height: height * 0.4
  };
```




### Programa 2
> http://www.generative-gestaltung.de/2/sketches/?01_P/P_2_2_6_03
- Adoro ese efecto así como de hebra de ADN que parece 3D por toda la línea y se mantiene coherente sin importar la curva que dibuje, es una locura
- Funciones de p5.js utilizadas: setup(), draw(), mousePressed(), mouseReleased(), keyPressed(), vertex(), beginShape(), endShape(), stroke(), strokeWeight(), noFill(), fill(), ellipse(), line(), background(), createVector(), p5.Vector.lerp(), atan2(), constrain(), random(), sin(), cos()
- Técnicas de programación aplicadas: Funciones Constructivas y Recursividad
- Cambios: Cambio el número de articulaciones del péndulo de 12 a 6, y aumenté el damping de 0.998 a 0.95.
- https://editor.p5js.org/Juanmar5/sketches/fc81MhnCh
``` p5
var joints = 6;
var damping = 0.95;
```



### Programa 3
> https://p5js.org/examples/math-and-physics-smoke-particle-system/
- Me parece un muy interesante ejemplo de cómo hace ese shader de forma tan simple pero cambia de color y replica el efecto, está increíble. 
Parece que está utilizando ciclos for para crear un vector que determine la posición del viento basado en la del cursor y está constantemente creando y eliminando circulos que evocan de uno central 
en un ritmo que da ese efecto de humo
- Funciones de p5.js utilizadas: preload(), createVector(), map(), push()/pop(), stroke(), strokeWeight(), line(), image(), tint()
- Técnicas de programación aplicadas: Clases como ParticleSystem y Particle, Uso de vectores (p5.Vector), Animación Frame-by-Frame con draw(), Gestión de memoria manual
- Cambios: En la clase Particle, modifico el constructor para cambiar el color según mouseY en lugar de frameCount
- https://editor.p5js.org/Juanmar5/sketches/CWTTBmw8h
  ``` p5
  this.color = color(map(mouseY, 0, height, 0, 255), 255, 255);
  ```




