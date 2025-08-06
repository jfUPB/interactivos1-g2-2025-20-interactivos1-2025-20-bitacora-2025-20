# Unidad 2

## 🔎 Fase: Set + Seek

### ACTIVIDAD 01

¿Cómo funciona el ejemplo?
Se define una clase Pixel, que representa un píxel individual de la micro:bit con cierta lógica de encendido y apagado.

Cada instancia de Pixel tiene un estado inicial, una posición (X, Y) en la matriz de LEDs, un estado del LED (pixelState, encendido o apagado), y un intervalo de tiempo entre cambios de estado.

En el loop infinito del programa (while True), se llama constantemente al método update() de cada píxel, lo cual evalúa el estado actual y actualiza el comportamiento del LED si es necesario.

Análisis del código con máquina de estados

¿Cuáles son los estados en el programa?

Los estados están definidos en el atributo self.state. Hay dos estados posibles:

"Init"

Estado inicial de cada Pixel. Solo se entra una vez al principio.

"WaitTimeout"

Estado de espera. Aquí el programa espera que pase el intervalo de tiempo definido para alternar el estado del LED.

⚙️ ¿Cuáles son los eventos o inputs?
Aunque este programa no tiene entradas externas como botones, sí tiene eventos internos (condiciones que provocan un cambio de estado):

Inicio del programa: cuando se crea el objeto Pixel, empieza en el estado "Init".

Tiempo transcurrido: el evento principal es el paso del tiempo, que se evalúa así:

python
Copiar
Editar
utime.ticks_diff(utime.ticks_ms(), self.startTime) > self.interval
Este evento activa el cambio de encendido/apagado del píxel.

### ACTIVIDAD 02

#### Código
```python
(from microbit import *
import utime

class Semaforo:
def init(self):
self.estado = "ROJO"
self.tiempo_inicio = utime.ticks_ms()

python
Copiar
Editar
def actualizar(self):
    tiempo_actual = utime.ticks_ms()
    tiempo_transcurrido = utime.ticks_diff(tiempo_actual, self.tiempo_inicio)

    if self.estado == "ROJO":
        self.encender_rojo()
        if tiempo_transcurrido > 3000:
            self.estado = "VERDE"
            self.tiempo_inicio = tiempo_actual

    elif self.estado == "VERDE":
        self.encender_verde()
        if tiempo_transcurrido > 3000:
            self.estado = "AMARILLO"
            self.tiempo_inicio = tiempo_actual

    elif self.estado == "AMARILLO":
        self.encender_amarillo()
        if tiempo_transcurrido > 1000:
            self.estado = "ROJO"
            self.tiempo_inicio = tiempo_actual

def encender_rojo(self):
    display.clear()
    display.set_pixel(2, 0, 9)

def encender_amarillo(self):
    display.clear()
    display.set_pixel(2, 1, 9)

def encender_verde(self):
    display.clear()
    display.set_pixel(2, 2, 9)
mi_semaforo = Semaforo()

while True:
mi_semaforo.actualizar()
sleep(100)
```

#### Estados
Son los distintos momentos en los que se encuentra el semáforo:

"ROJO" → El LED rojo está encendido.

"VERDE" → El LED verde está encendido.

"AMARILLO" → El LED amarillo está encendido.

Estos estados están representados en la variable self.estado dentro de la clase Semaforo.

#### Eventos
Los eventos son las condiciones que provocan un cambio de estado. En este caso, los eventos dependen del tiempo transcurrido.

tiempo_transcurrido > 3000 → si el estado actual es "ROJO" o "VERDE", cambia al siguiente.

tiempo_transcurrido > 1000 → si el estado es "AMARILLO", regresa a "ROJO".

Las acciones son las tareas que se ejecutan dentro de cada estado:

display.clear() → Limpia la pantalla.

display.set_pixel(x, y, 9) → Enciende el LED correspondiente al color actual.


#### Acciones según estado:

Estado	     Acción

"ROJO"	     Enciende el LED en (2, 0)
"VERDE"	     Enciende el LED en (2, 2)
"AMARILLO"	 Enciende el LED en (2, 1)

### ACTIVIDAD 03

¿Por qué este programa parece hacer varias cosas al mismo tiempo?
Aunque el micro:bit solo hace una cosa a la vez, este programa revisa muchas veces por segundo si:
el botón A fue presionado, y
si ya pasó cierto tiempo desde que se mostró una imagen.
Como hace estas dos revisiones en cada vuelta del ciclo while True, parece que el programa está pendiente de todo al mismo tiempo. Por eso decimos que simula que hace varias tareas a la vez.

Estados, eventos y acciones
Estados :

STATE_INIT: Al comenzar, muestra una carita feliz y pasa al siguiente estado.

STATE_HAPPY: Muestra una carita feliz.

STATE_SMILE: Muestra una carita sonriente.

STATE_SAD: Muestra una carita triste.

Eventos

Si se presiona el botón A

Si pasa cierto tiempo (1 o 2 segundos dependiendo del estado)

