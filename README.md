# Chat Cliente-Servidor

Aplicación de chat en tiempo real desarrollada en Java con **Sockets TCP**, **Threads** y **Java Swing (JFrame)**. Permite que un servidor central atienda a N clientes simultáneos, cada uno en su propia computadora, y que todos puedan chatear entre sí en tiempo real.

## Tecnologías usadas

- Java (proyecto de NetBeans con Ant)
- Java Swing / JFrame (NetBeans GUI Builder)
- Sockets TCP (`ServerSocket` / `Socket`)
- Threads (un hilo por cada cliente conectado)
- [Tailscale](https://tailscale.com/) para conectar clientes desde distintas redes físicas

## Estructura del proyecto

```
CHAT-CLIENTE-SERVIDOR/
├── src/
│   ├── ServidorJFrame.java        # Ventana y lógica del servidor
│   ├── ManejoHilosClientes.java   # Hilo que atiende a cada cliente
│   ├── ClienteJFrame.java         # Ventana y lógica del cliente
│   └── Chat_ClienteServidor_img/  # Íconos de la interfaz
├── nbproject/                     # Configuración de NetBeans
├── build.xml
└── manifest.mf
```

| Clase | Responsabilidad |
|-------|-----------------|
| `ServidorJFrame` | Ventana del servidor. Abre un `ServerSocket` en el puerto 5000, acepta conexiones, muestra los clientes conectados (nombre e IP), la cantidad de clientes y el log de mensajes. Reenvía cada mensaje a todos los clientes. |
| `ManejoHilosClientes` | Hilo que atiende a un cliente. Recibe su nombre, lee sus mensajes y notifica al servidor cuando se conecta o se desconecta. |
| `ClienteJFrame` | Ventana del cliente. Pide el nombre del usuario, se conecta al servidor, muestra el chat, la lista de usuarios conectados y permite enviar mensajes. |

## Cómo funciona

1. El servidor inicia y queda escuchando en el puerto `5000`.
2. Cada cliente se conecta y envía su nombre como primer mensaje.
3. El servidor crea un hilo (`ManejoHilosClientes`) por cada cliente conectado.
4. Cuando un cliente envía un mensaje, el servidor lo registra en su log y lo reenvía a todos los clientes con el formato `nombre: mensaje`.
5. El servidor mantiene actualizada la lista de usuarios y se la envía a todos los clientes cada vez que alguien entra o sale.

## Cómo ejecutar

### Requisitos

- JDK instalado
- NetBeans (recomendado)

### 1. Servidor

1. Abrir el proyecto en NetBeans.
2. Ejecutar `ServidorJFrame` en la computadora que hará de servidor.
3. Anotar la IP de esa computadora. Si los clientes están en redes distintas, usar la IP de Tailscale.

### 2. Clientes

1. En `ClienteJFrame.java`, cambiar la constante `HOST` por la IP del servidor:

   ```java
   final String HOST = "IP_DEL_SERVIDOR"; // por defecto es "localhost"
   final int PUERTO = 5000;
   ```

2. Cada compañero ejecuta `ClienteJFrame` en su propia computadora.
3. Al iniciar, se ingresa el nombre de usuario y se entra al chat.

Para probar todo en una sola computadora basta con dejar `HOST` en `localhost` y abrir varias instancias del cliente.

## Requisitos cumplidos

- [x] Vista de Cliente (nombre, chat, envío de mensajes)
- [x] Vista de Servidor (clientes conectados, log de mensajes)
- [x] Soporte para N cantidad de clientes simultáneos
- [x] Todos los clientes ven los mensajes de todos en tiempo real

## Autores

- Kendall Quesada (kenmendoza2712-ops)
- Cristofer (chrissoto03)
