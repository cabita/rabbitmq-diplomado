# Taller de RabbitMQ - Diplomado U. Sabana

Este código implementa un servicio de inventario utilizando RabbitMQ como sistema de mensajería y a su vez un servicio de tienda que se conecta a un sistema de mensajería RabbitMQ para recibir actualizaciones de inventario y permite verificar la disponibilidad de productos.

## Instalación del proyecto:
- Clonar el repositorio
- Ejecutar el comando ```pipenv shell``` para crear un entorno específico para este proyecto.
- Instalar las dependencias con el comando ```pipenv install```

## Servicios:
### Inventory_service:
Este servicio implementa un sistema para actualizar el inventario de productos, enviando mensajes a una cola de RabbitMQ. Esto permite que otros servicios puedan consumir estas actualizaciones de inventario de manera asíncrona.

Para ello se establece una conexión con RabbitMQ, se declara una cola.  
El constructor inicializa el host (por defecto 'localhost') y el nombre de la cola.

En el método update_inventory():

Se conecta a RabbitMQ.
Crea un mensaje JSON con el ID del producto y la cantidad.
Publica el mensaje en la cola.
Imprime un mensaje de confirmación.
Cierra la conexión.


### Store_service:

Este código implementa un servicio de tienda que se conecta a un sistema de mensajería RabbitMQ para recibir actualizaciones de inventario y permite verificar la disponibilidad de productos.  Entonces realiza lo siguiente:

Recibir actualizaciones de inventario en tiempo real.
Consultar la disponibilidad de productos.

Define una clase StoreService:

Inicializa conexiones, inventario y variables de estado.
Implementa métodos para conectar con RabbitMQ, procesar actualizaciones de inventario y verificar disponibilidad.


El método connect():
Intenta establecer una conexión con RabbitMQ.
Si falla, reintenta cada 5 segundos.
Configura un consumidor para la cola de actualizaciones de inventario.


El método process_inventory_update():
Procesa los mensajes recibidos y actualiza el inventario local.


El método check_inventory():
Verifica la disponibilidad de un producto en la cantidad solicitada.


El método run():
Inicia la conexión en un hilo separado.
Ejecuta un bucle principal que permite al usuario consultar el inventario.
