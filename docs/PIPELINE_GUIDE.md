# Guía de pipelines (GitHub Actions)

## Para qué los usamos

Nosotros configuramos pipelines para que cada vez que alguien sube código a `main` o abre un PR hacia `main`, GitHub ejecute chequeos automáticos. Así no mergeamos algo que ni siquiera compila o que rompe los charts.

## Pipeline de aplicación

**Archivo:** `.github/workflows/ci-apps.yml`  
**Nombre en GitHub:** `CI aplicación`  
**Cuándo corre:** `push` y `pull_request` a `main`.

### Jobs

1. **vote**  
   - Entra a la carpeta `vote/`.  
   - Corre `mvn -B test` con Java 22.

2. **worker**  
   - Entra a `worker/`.  
   - Corre `go test ./...`.

3. **result**  
   - Entra a `result/`.  
   - `npm install` y `node --check server.js`.

4. **docker**  
   - Solo si los tres anteriores pasan.  
   - Construye la imagen Docker de `vote`, `worker` y `result` sin subirlas a ningún registry (`push: false`).

### Scripts aparte

No creamos carpetas `scripts/` con `.sh`. Los comandos van directo en el YAML porque son cortos y se entienden solos.

## Pipeline de infraestructura (Helm)

**Archivo:** `.github/workflows/infra-helm.yml`  
**Nombre:** `Infraestructura Helm`  
**Cuándo corre:** igual, `push` y `pull_request` a `main`.

Instala Helm en el runner y para cada chart corre:

- `helm lint ...`
- `helm template ... > /dev/null`

sobre:

- `infrastructure/`
- `vote/chart`
- `worker/chart`
- `result/chart`