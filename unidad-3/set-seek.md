# Unidad 3

## 🔎 Fase: Set + Seek

### Actividad 01

Diagrama de bloques:

[Cliente Móvil (Mobile.js)]  
       │ (touchMoved -> genera JSON con coordenadas x,y)
       ▼
[Socket.IO en Cliente Móvil]  
       │ (socket.emit('message', datos))
       ▼
[Servidor Node.js con Express + Socket.IO]  
       │ (recibe mensaje y lo reenvía con socket.broadcast.emit)
       ▼
[Socket.IO en Cliente Escritorio (Desktop.js)]  
       │ (socket.on('message') recibe datos JSON)
       ▼
[Lógica en Desktop.js]  
       │ (parsea coordenadas x,y y actualiza circleX, circleY)
       ▼
[Pantalla Escritorio]  
       ● Dibuja el círculo rojo en la nueva posición


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
