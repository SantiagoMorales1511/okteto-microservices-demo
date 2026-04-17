# Patrones de nube


## 1. Mensajería asíncrona (Kafka)

**Qué hace en nuestro proyecto:** vote no escribe directo en la base cuando el usuario vota; manda un mensaje a Kafka. worker lo procesa después.

Desacoplamos el momento en que el usuario manda el voto del momento en que se persiste. Si worker tarda o se reinicia, el mensaje puede seguir en la cola (según configuración de retención de Kafka).

## 2. Microservicios en contenedores

**Qué hace en nuestro proyecto:** vote, worker y result son tres procesos distintos, cada uno con su `Dockerfile`. kafka y postgresql también van en contenedores. Los levantamos juntos con Docker Compose.

Cada servicio se puede versionar y desplegar por separado en teoría; en la práctica del taller los corremos todos en una máquina con compose.
