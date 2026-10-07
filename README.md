# Calculadora frontend

Aplicación React con Vite que replica la interfaz BlueCompute de
`stitch_minimalist_blue_calculator_ui` e invoca las operaciones básicas descritas
en `api-docs.json`.

## Desarrollo local

```bash
npm install
npm run dev
```

El proxy de Vite dirige `/api/` y `/health` a `http://localhost:8080`. Inicia el
backend Spring Boot en ese host/puerto antes de probar operaciones.

## Docker y Nginx

Con Spring Boot escuchando en el puerto `8080` de la máquina host:

```bash
docker compose up --build
```

Abre `http://localhost:3000`. Nginx sirve el frontend y envía `/api/` y `/health`
al backend. Si la API está en otro host o puerto, configura `API_HOST` y
`API_PORT`; también puedes cambiar el puerto público con `FRONTEND_PORT`.

Por ejemplo:

```bash
API_HOST=host.docker.internal API_PORT=8080 FRONTEND_PORT=3000 docker compose up --build
```

La API debe exponer `GET /health` y las rutas
`/api/v1/calculadora/{sumar,restar,multiplicar,dividir}` con los parámetros de
consulta `numero1` y `numero2`. La respuesta satisfactoria puede ser un decimal
como texto o JSON; los errores `application/problem+json` se muestran en la UI.
