# Unidad 3


## 🛠 Fase: Apply

### Actividad 03

Mobile sketch.js

``` js
let socket;
let currentState = 0;

function setup() {
  createCanvas(400, 400);
  socket = io();
  textAlign(CENTER, CENTER);
  textSize(18);
}

function draw() {
  background(200);
  fill(0);
  text("📱 Control remoto\nEstado actual: " + currentState, width/2, height/2);
  textSize(14);
  text("👉 Toca la pantalla para cambiar estado", width/2, height/2 + 40);
  text("👉 Arrastra para enviar datos", width/2, height/2 + 70);
}

// Función para enviar estado + parámetros simulados
function sendStateData() {
  let params = {
    estado: currentState,
    clientesConectados: floor(random(0, 10)),
    parametroExtra: nf(random(0, 1), 1, 2)
  };
  socket.emit('message', JSON.stringify(params));
  console.log("📤 Enviando datos:", params);
}

// Cambiar estado tocando la pantalla
function mousePressed() {
  currentState = (currentState + 1) % 3; // 0 → 1 → 2 → 0...
  sendStateData();
}

// Enviar datos mientras se arrastra
function mouseDragged() {
  let dragData = {
    estado: currentState,
    x: mouseX,
    y: mouseY
  };
  socket.emit('message', JSON.stringify(dragData));
  console.log("📤 Enviando drag:", dragData);
}
```

Desktop sketch.js

``` js
let socket;
let state = 0;
let clientesConectados = 0;
let parametroExtra = 0;

function setup() {
  createCanvas(400, 400);
  background(0);

  socket = io();

  socket.on('message', (msg) => {
    try {
      let data = JSON.parse(msg);

      // Si tiene campo 'estado', lo procesamos
      if(data.estado !== undefined){
        state = data.estado;
        if(data.clientesConectados !== undefined) clientesConectados = data.clientesConectados;
        if(data.parametroExtra !== undefined) parametroExtra = data.parametroExtra;
      }

    } catch {
      console.log("Mensaje no JSON recibido:", msg);
    }
  });
}

function draw() {
  background(30);
  fill(255);
  textAlign(CENTER, CENTER);
  textSize(18);

  switch(state){
    case 0:
      text("🌐 Estado 0\nEsperando datos...", width/2, height/2);
      break;

    case 1:
      text("🎨 Estado 1\nClientes: " + clientesConectados + "\nExtra: " + parametroExtra, width/2, height/2);
      fill(100, 200, 250);
      ellipse(width/2, height/2 + 80, 50 + clientesConectados*5, 50 + clientesConectados*5);
      break;

    case 2:
      text("🔥 Estado 2\nClientes: " + clientesConectados + "\nExtra: " + parametroExtra, width/2, height/2);
      fill(250, 100, 100);
      rectMode(CENTER);
      rect(width/2, height/2 + 80, 50 + parametroExtra*50, 50 + parametroExtra*50);
      break;
  }
}



```

Video: 



https://github.com/user-attachments/assets/0f55e620-bd70-4159-9432-c229044e9f3c




```
