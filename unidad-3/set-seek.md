# Unidad 3

## 🔎 Fase: Set + Seek

### Actividad 01

+-----------------------------+                   
|  Cliente Móvil (mobile.js)  |                   
|   p5.js - Captura touch     |                   
+-----------------------------+                   
               |                                   
               v                                   
+-----------------------------+                   
|    Socket.IO (Móvil)        |                   
|  emit("message", JSON{x,y}) |                   
+-----------------------------+                   
               |                                   
               v                                   
+-----------------------------+                   
|  Servidor Node.js           |                   
| Express + Socket.IO         |                   
| recibe y hace broadcast     |                   
+-----------------------------+                   
               |                                   
               v                                   
+-----------------------------+                   
|    Socket.IO (Escritorio)   |                   
|   on("message", parse JSON) |                   
+-----------------------------+                   
               |                                   
               v                                   
+-----------------------------+                   
| Cliente Escritorio          |                   
| p5.js - desktop.js          |                   
| Actualiza circleX, circleY  |                   
+-----------------------------+                   
               |                                   
               v                                   
+-----------------------------+                   
|  Pantalla Escritorio        |                   
|  Dibuja círculo rojo        |                   
+-----------------------------+                   


1. Descripción paso por paso del flujo de datos

- Cliente Móvil – Captura del toque:

- El usuario toca la pantalla.

- La función touchMoved() obtiene las coordenadas mouseX y mouseY.

- Se arma un objeto JSON con el formato:
```
{
  type: 'touch',
  x: mouseX,
  y: mouseY
}
```

Este objeto se envía al servidor usando:

```
socket.emit('message', JSON.stringify(touchData));
```

- Servidor Node.js (server.js):

- El servidor escucha conexiones con io.on('connection').

- Cuando recibe un mensaje con socket.on('message', ...), lo imprime en consola y lo reenvía a todos los demás clientes conectados usando:

```
socket.broadcast.emit('message', message);
```

- Cliente Escritorio – Recepción:

- El escritorio tiene un socket.on('message') que recibe los datos enviados por el servidor.

- Intenta parsear el JSON recibido. Si es del tipo "touch", actualiza las variables:
```
circleX = parsedData.x;
```

### Actividad 02


