# Unidad 1

## 🛠 Fase: Apply

### Actividad 5

***etapas del método deconstrucción/reconstrucción.***


*Select*

Voy a generative design y escojo uno de los ejemplos, he escogido este:
Link del ejercicio tomado: [link del ejercicio tomado](https://editor.p5js.org/generative-design/sketches/P_2_1_2_01)

Debido a que me ha interesado el diseño y la forma del código que me parece un tanto distinta de la que yo estoy acostumbrada.

*Describe*

- Se utilizan círculos sin relleno es decir solamente el borde, colores en escala de grises que cuando se mueve el puntero estos aumentan de tamaño o disminuyen. Cuando aumentan de tamaño se va oscureciendo más el color. Cuando le hago click cambia el patrón que tenía antes como si se reposicionaran. Por lo tanto pienso que tal vez si se desplazan pero ligeramente y lo que verdaderamente cambia es el tamaño del grosor del borde cuando me desplazo con el puntero.
<img width="599" height="559" alt="image" src="https://github.com/user-attachments/assets/8cb956a1-b82d-46a8-bb1e-c586d38d40f6" />

*Analyze*
- Para generar esa cuadricula peculiar noto que se crea por medio de:
  ``` js
  var tileCount = 20;
  ```
  Eso quiere decir que se divide en una cuadricula de 20 columnas y 20 filas, esto es lo que pasa cuando lo cambio a 40 por ejemplo:
  <img width="2283" height="1033" alt="image" src="https://github.com/user-attachments/assets/35fbc22a-6b89-49bd-b755-8ca8344dd189" />
  
- Algo que me llamó la atención es esto nuevo llamado actRandomSeed, experimenté y parece que es algo para almacenar semillas que controla valores aleatorios. Aparece en el draw y siento que es como si le estuviera diciendo que todos los random comiencen desde la semilla almacenada.
  
- Translate por lo que veo funciona para posicionar todo el dibujo en el lugar indicado.
  
- Esto para mi es un bucle que recorre cada fila y columna de la cuadrícula:
``` js
 for (var gridY = 0; gridY < tileCount; gridY++) {
  for (var gridX = 0; gridX < tileCount; gridX++) {
```
- Posición base:
``` js
var posX = width / tileCount * gridX;
var posY = height / tileCount * gridY;
```
- Pienso que es la parte del desplazamiento que se mueve de forma aleatoria por el random, se divide entre 20 para que no se note el desplazamiento.
``` js
var shiftX = random(-mouseX, mouseX) / 20;
var shiftY = random(-mouseX, mouseX) / 20;
```
- Aquí se dibuja el círculo que yo sepa, además de que el tamaño es controlado por el mousey/15:
``` js
ellipse(posX + shiftX, posY + shiftY, mouseY / 15, mouseY / 15);
```
- Ya por último con la tecla S se guarda la imagen.

*Convert*

Foto de como quedó mi experimento: <img width="1989" height="1090" alt="image" src="https://github.com/user-attachments/assets/550069f5-af6f-4a82-9b2b-a5639c18703b" />
Link de mi versión: https://editor.p5js.org/Jakeline-Avila/sketches/5iGOUrvKP

- Lo único que hice fue tomar el código anterior y cambiar los valores, ejemplo volví los círculos azules, menos columnas y filas, mayor tamaño y menos desplazamiento.

*Explore*
Link de la exploración: https://editor.p5js.org/Jakeline-Avila/sketches/Qf1SHzPNo
<img width="1200" height="1200" alt="250724_152138_941" src="https://github.com/user-attachments/assets/22e34d62-03e3-42e3-adf5-94f6b4ca097c" />

<img width="1200" height="1200" alt="250724_152155_913" src="https://github.com/user-attachments/assets/1fc48759-208b-48e9-9d16-dc474a9121aa" />

<img width="1821" height="1162" alt="image" src="https://github.com/user-attachments/assets/cdff0bf3-5bb5-422e-a4c9-0342861dfbfc" />

- Cambié los shiftY y shiftX por unos nuevos llamado ONDAY y ONDAX donde incluí sin y cos para hacer que se muevan como si estuvieran "ondeando".
- Cambié ellipse por rect.
- Cambié el color para que sea random cada vez que oprima la pantalla.
- Mini animación con let t = frameCount * 0.05;

*Tinker*

Se me ha roto el dibujo: <img width="1782" height="1084" alt="image" src="https://github.com/user-attachments/assets/b8e5c808-efc7-4404-a134-13a97f2fc7c8" />

Link del experimento: https://editor.p5js.org/Jakeline-Avila/sketches/y2nKJtGTF



