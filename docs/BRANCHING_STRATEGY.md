# Estrategia de ramas

## Cómo acordamos trabajar

Nosotros seguimos algo parecido a **GitHub Flow**: una rama principal estable y ramas cortas para cada cambio.

## Rama `main`

- Es la rama donde queremos que quede el código que ya pasó revisión.
- Preferimos que nadie haga push directo sin PR (si GitHub lo permite, configuramos protección de rama).
- Antes de mergear, nos fijamos que el **CI** esté en verde.

## Ramas de desarrollo

Usamos prefijos para que se entienda qué es cada cosa:

| Prefijo | Para qué |
|---------|----------|
| `feature/` | Nueva funcionalidad o mejora |
| `fix/` | Corrección de un error |

Ejemplo: `feature/ajuste-documentacion`, `fix/puerto-result`.

## Ramas o cambios de infraestructura

Cuando tocamos cosas de despliegue (Helm, `docker-compose.yml`, `okteto.yml`, workflows en `.github/workflows/`), lo tratamos con más cuidado: o usamos ramas tipo `infra/...` o marcamos el PR como cambio de infra para que el otro lo revise sabiendo que puede romper el entorno.

## Flujo que seguimos en la práctica

1. `git checkout main` y `git pull`.
2. Creamos rama: `git checkout -b feature/nombre`.
3. Commits con mensajes claros.
4. `git push` y abrimos **Pull Request** hacia `main`.
5. Revisamos entre nosotros y mergeamos cuando el CI pasa.
