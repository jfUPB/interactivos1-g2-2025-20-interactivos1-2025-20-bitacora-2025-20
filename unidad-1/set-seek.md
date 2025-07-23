# Unidad 1

## 🔎 Fase: Set + Seek

# Actividad 01

## ¿Qué es un sistema físico interactivo?

Para mí, los sistemas físicos interactivos son como una mezcla entre lo real y lo digital. Son cosas que puedo tocar, mover o sentir físicamente, pero que al mismo tiempo están conectadas a un sistema que reacciona o cambia en una pantalla o en una experiencia virtual. Por ejemplo, en ‘The Void’ puedo caminar por un espacio real y sentir calor o viento, pero estoy viendo un mundo completamente diferente con gafas de realidad virtual. Es como si lo que hago con mi cuerpo tuviera un efecto directo en lo que pasa en el mundo digital. Me parece súper interesante porque no solo uso mis ojos y oídos, sino todo mi cuerpo para interactuar con la tecnología.

## ¿Cómo podrías aplicar lo que has visto en tu perfil profesional?

Ver estos sistemas me hizo entender que como animadora no solo puedo pensar en la pantalla, sino también en cómo mi trabajo puede cobrar vida en el mundo físico. Me gustaría aplicar lo aprendido para diseñar experiencias donde la animación se conecte con el cuerpo del usuario, con espacios reales o con objetos tangibles. Esto abre muchas posibilidades para crear entretenimiento más inmersivo, artístico o educativo. Y así crear experiencias únicas.

# Actividad 02

## ¿Qué es el diseño y el arte generativos?

Para mí, el diseño generativo es una forma de crear a partir de reglas, datos o códigos. En vez de diseñar cada elemento manualmente, se diseña un sistema que genera resultados por sí solo. Es como darle instrucciones claras a una máquina o programa y dejar que este cree cosas nuevas a partir de esas reglas. Puede usar datos, algoritmos, sensores o interacciones humanas para producir formas, animaciones, sonidos, patrones… y cada resultado puede ser diferente y único. Me parece una forma muy viva y creativa de trabajar, porque combina lo técnico con lo artístico.

## ¿Cómo podrías aplicar lo que has visto en tu perfil profesional?

Después de ver estos ejemplos, me di cuenta de que el arte generativo tiene muchísimo potencial para lo que quiero hacer en el futuro. Como estoy enfocada en animación y entretenimiento digital, podría usar este tipo de diseño para crear animaciones que cambian solas con datos o con lo que haga el usuario. También me gustaría experimentar con mundos o personajes que se generen automáticamente, o hacer instalaciones donde lo visual reaccione a sensores, sonidos o movimientos. Me parece una forma súper creativa de hacer que mis proyectos no solo se vean bien, sino que estén vivos y sean únicos cada vez.

# Actividad #3

## INPUTS/PROCESOS/OUTPUTS

-----------------------------------------------------
### Inputs	
- El serial para amboscomputadoras 
- Botón A del micro:bit
- Botón B del micro:bit
- Sensor de movimiento (sacudida)
- Botón "Send Love" en la interfaz de p5.js
### Proceso
Seria el programa que se encarga de dictamnar los inputs y outputs correspondientes
### Outputs
- En pantalla (p5.js): el círculo cambia de color y muestra la letra recibida (A: rojo, B: amarillo, C: verde)
- En el micro:bit: muestra una mariposa al inicio y un corazón si recibe la letra ‘h’



# Actividad 4

[LINK ARCHIVO P5.JS](https://editor.p5js.org/MariPrada/sketches/CuHteAIrQ)

```javascript
function setup() {
  createCanvas(600, 600);
  noLoop(); // Solo dibuja una vez
  rectMode(CENTER);
  angleMode(DEGREES);
  background(30);
  noFill();

  let spacing = 60;
  let maxRotation = 360;

  for (let x = spacing / 2; x < width; x += spacing) {
    for (let y = spacing / 2; y < height; y += spacing) {
      push();
      translate(x, y);
      rotate(random(maxRotation));
      strokeWeight(random(1, 3));
      stroke(random(100, 255), random(100, 255), random(100, 255), 200);

      // Dibuja un patrón aleatorio en cada celda
      let shapeType = int(random(3));
      if (shapeType === 0) {
        ellipse(0, 0, random(20, 50), random(20, 50));
      } else if (shapeType === 1) {
        rect(0, 0, random(20, 50), random(20, 50));
      } else {
        beginShape();
        for (let i = 0; i < 5; i++) {
          let angle = map(i, 0, 5, 0, 360);
          let r = random(10, 30);
          let vx = cos(angle) * r;
          let vy = sin(angle) * r;
          vertex(vx, vy);
        }
        endShape(CLOSE);
      }
      pop();
    }
  }
}
```

<img width="634" height="644" alt="image" src="https://github.com/user-attachments/assets/6dfbea4a-c2a6-44e1-984b-dc9a3ba00db3" />




