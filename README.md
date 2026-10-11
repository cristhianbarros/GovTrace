# GovTrace

## Requisitos

- [Docker](https://docs.docker.com/get-docker/) con Docker Compose v2
- `make` y `git`
- El puerto `8080` libre (se cambia con `HTTP_PORT` en `.env.docker`)
- Internet en la primera ejecución, para descargar las imágenes

No hace falta instalar PHP, Node.js, Rust ni una billetera de Stellar: todo corre en contenedores, con una red Stellar local.

Para solo verlo, sin instalar nada: https://govtrace.duckdns.org (testnet).

## Instalación

El código de la aplicación está en su propio repositorio:

```bash
git clone https://github.com/cristhianbarros/govtrace-app.git
cd govtrace-app
make setup
```

`make setup` construye las imágenes, instala las dependencias, crea las bases de datos y compila el front. La primera vez tarda unos minutos.

## Cómo correrlo

```bash
make demo
```

Levanta la aplicación, la red Stellar local con el contrato de sellado y una veeduría de demostración con reportes ya sellados. Al terminar, entra con:

| Rol | Dirección | Correo | Contraseña |
|---|---|---|---|
| Super Administrador | http://govtrace.localhost:8080 | `admin@demo.govtrace.test` | `Demo#2026Global` |
| Administrador de la veeduría | http://veeduria-demo.govtrace.localhost:8080 | `admin@veeduria-demo.org` | `Demo#2026Admin` |
| Veedor | http://veeduria-demo.govtrace.localhost:8080 | `ana.torres@correo.co` | `Demo#2026Veedor` |

El sitio público (mapa, obras y validador) no pide cuenta. Para detener todo: `make down`.
