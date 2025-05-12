### ¿Cómo entiendo este código?

- function preload(): Tiene imágenes de brochas pre cargadas
- function setup(): Crea el lienzo para dibujar
- function draw(): Dibuja con una brocha al presionar el click izquierdo y hace que se dibuje con un ángulo y translación del mouse
- function mousePressed(): Cambia el color con el espacio a uno aleatorio
- function keyPressed(): Hace que las teclas de flechas laterales aumenten o disminuyen  la velocidad rotación de dibujado en 0.5, el valor puede ser negativo; también hace que las flechas de altura aumenten el tamaño del módulo mientras esté dibujando, pero parece que cada dibujado nuevo (soltar y clickear de nuevo) altera esté tamaño también
- function keyReleased(): Hace que la s guarde una imagen y que d altere el ángulo de rotación en 180 y la velocidad en -1, así como cambiar a colores predeterminados con 1, 2, 3, 4; uno aleatorio con Espacio y finalmente el módulo de línea (brocha) se cambia con 5, 6, 7, 8 y 9
