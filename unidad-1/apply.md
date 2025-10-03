# Unidad 1

## 🛠 Fase: Apply

### ACTIVIDAD 05

#### Explica cómo funciona el sistema físico interactivo que acabamos de crear.

Estamos creando un sistema físico interactivo distribuido. Eso significa que usamos dos dispositivos diferentes (dos “computadoras”, por así decirlo) que se comunican entre sí para lograr algo. En nuestro caso:

Un micro:bit (una mini computadora con botones).

Una computadora normal (donde usamos p5.js para hacer una animación visual).

¿Qué hace cada computadora?
1. micro:bit (la mini computadora)
Input:
Botón A
Es el botón físico que tú puedes presionar con el dedo.

Output:
Mensaje por puerto serial
Si el botón está presionado, el micro:bit envía un mensaje por el cable USB a la otra computadora.

Envía "A" si el botón está presionado.

Envía "N" si no lo está.
Esto lo hace varias veces por segundo.

2. Computadora con p5.js
Input:
Mensajes del micro:bit (por el cable USB)
La compu recibe las letras "A" o "N" que manda el micro:bit.

Output:
Un cuadrado de color en pantalla
La compu dibuja un cuadrado:

Si recibe "A" → lo pone rojo (el botón está presionado).

Si recibe "N" → lo pone verde (el botón no está presionado).


### ACTIVIDAD 06

[LINK PROGRMA P5.JS](https://editor.p5js.org/MariPrada/sketches/yHXtZ8JsE)

CÓDIGO DE PROGRAMA EN P5.JS

```
let port;
  let connectBtn;
  let connectionInitialized = false;
  let variableX;

  function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    connectBtn = createButton("Connect to micro:bit");
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);
    variableX = width / 2;
  }

  function draw() {
    background(220);

    if (port.opened() && !connectionInitialized) {
      port.clear();
      connectionInitialized = true;
    }

    if (port.availableBytes() > 0) {
      let dataRx = port.read(1);
      if (dataRx == "A") {
        variableX = variableX - 10;
      } else if (dataRx == "B") {
       variableX = variableX + 10;
      }
    }

  
    circle(variableX, height / 2, 50);

    if (!port.opened()) {
      connectBtn.html("Connect to micro:bit");
    } else {
      connectBtn.html("Disconnect");
    }
  }

  function connectBtnClick() {
    if (!port.opened()) {
      port.open("MicroPython", 115200);
      connectionInitialized = false;
    } else {
      port.close();
    }
  }
```

CÓDIGO DE PROGRAMA EN micro:bit 

```
from microbit import *

uart.init(baudrate=115200)
display.show(Image.HAPPY)


while True:

    if button_a.was_pressed():
        uart.write('A')
       
    if button_b.was_pressed():
        uart.write('B')
   

    sleep(100)
```
