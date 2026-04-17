# Docker Compose en este proyecto

## Estado actual

Este proyecto utiliza **Docker Compose** como mecanismo principal para definir y ejecutar el entorno local.  
La configuración se encuentra en el archivo `docker-compose.yml` ubicado en la raíz del repositorio.

Docker Compose permite levantar de forma conjunta los servicios de la aplicación y sus dependencias de infraestructura en un entorno reproducible y versionado.

## Servicios definidos

La composición local incluye los siguientes servicios:

| Servicio | Rol |
|----------|-----|
| `vote` | Recibe los votos desde la interfaz web y publica eventos en Kafka |
| `worker` | Consume eventos desde Kafka y persiste los votos en PostgreSQL |
| `result` | Consulta la base de datos y muestra los resultados |
| `kafka` | Broker de mensajería para desacoplar la recepción y procesamiento de votos |
| `postgresql` | Base de datos relacional para almacenar los votos |

## Ventajas de usar Docker Compose

- definición declarativa del entorno en un solo archivo
- facilidad para levantar todos los servicios con un solo comando
- portabilidad entre entornos de desarrollo
- consistencia en configuración de red, puertos, volúmenes y dependencias
- soporte para validación y ejecución local del sistema completo

## Ejecución

Para iniciar el entorno local se utiliza:

```bash
docker compose up --build