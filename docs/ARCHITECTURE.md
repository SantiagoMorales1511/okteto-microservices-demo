# Arquitectura

## Qué estamos mostrando

Nosotros tomamos el **microservices-demo** como base: es una app de votación repartida en varios servicios. Para el taller nos interesaba entender el flujo completo y poder levantarlo en local, no reescribir la lógica desde cero.

## Componentes

| Pieza | Tecnología | Rol |
|-------|------------|-----|
| vote | Java (Spring Boot) | Web donde el usuario vota; manda el voto a Kafka |
| kafka | Apache Kafka | Cola: recibe mensajes de vote y los entrega al worker |
| worker | Go | Lee Kafka y guarda votos en PostgreSQL |
| postgresql | PostgreSQL | Base de datos con los votos |
| result | Node.js (Express + Socket.IO) | Web que lee la BD y muestra totales |

## Flujo que sustentamos

1. El usuario entra a **vote** (en local: `http://localhost:8080`).
2. vote publica un mensaje en **Kafka**.
3. **worker** consume ese mensaje y escribe en **postgresql**.
4. **result** consulta postgresql y actualiza la pantalla (en local: `http://localhost:4000`).

En una frase: **vote → kafka → worker → postgresql → result**.

## Cómo lo corremos nosotros

Para la entrega usamos **Docker Compose** (`docker-compose.yml` en la raíz). Ahí definimos los cinco servicios, puertos, volúmenes y healthchecks para que kafka y postgresql estén listos antes de que suban vote y worker.

El diagrama que adjuntamos en la entrega es `architecture.png` en la raíz del repo.

## Qué más trae el repo (y no es nuestro runtime principal)

El proyecto original incluye **Helm charts** (`vote/chart`, `worker/chart`, `result/chart`, `infrastructure/`) y **okteto.yml** para desplegar en Kubernetes/Okteto. Nosotros no hicimos la demo ahí; igual dejamos esos archivos y el CI los valida con `helm lint` / `helm template` para cumplir la parte de infraestructura del taller.