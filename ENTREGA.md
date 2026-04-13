# Taller 1 - Pipelines en Cloud

 - Santiago Morales
 - David Alejandro Troya

## Implementación realizada

Aunque el proyecto original trae archivos de Okteto, para esta entrega decidimos hacer la implementación de forma local con Docker Compose. Eso nos permitió levantar toda la arquitectura en nuestra máquina y probar el sistema completo sin depender de una instancia externa.

Con `docker-compose.yml` levantamos estos servicios:

- `vote`
- `kafka`
- `worker`
- `postgresql`
- `result`

De esta forma mantuvimos la misma estructura general del proyecto y pudimos hacer una prueba funcional completa.

## Demostración realizada

Para la demostración primero revisamos que los workflows de GitHub Actions estuvieran pasando correctamente. Después levantamos el entorno local y probamos el flujo completo del sistema.

La prueba consistió en registrar votos desde `vote`, revisar que los resultados cambiaran en `result` y confirmar en los logs del `worker` que sí había conexión con Kafka y PostgreSQL, además del procesamiento de mensajes.

## Resultados entregados

Como parte de la entrega se incluye:

- el repositorio con los workflows implementados
- el diagrama de arquitectura
- la configuración de despliegue local con Docker Compose
- capturas de GitHub Actions en ejecución exitosa
- capturas de la prueba local del sistema funcionando

### Cómo correrlo

1. Validar configuración:
   - `docker compose config`
2. Levantar todo:
   - `docker compose up --build -d`
3. Revisar estado:
   - `docker compose ps`

`http://localhost:8080` registrar votos.
`http://localhost:4000` resultados.

- Apagar servicios:
  - `docker compose down`
- Apagar y borrar volúmenes:
  - `docker compose down -v`