# GovTrace

## Requisitos

> **¿Solo quieres verlo?** No necesitas instalar nada: abre **https://govtrace.duckdns.org** (corre en la red de pruebas de Stellar).

Para correrlo en tu computador necesitas:

- Unos **10 GB libres** en el disco y **8 GB de memoria** (recomendado).
- **Internet** la primera vez, para descargar lo que hace falta.
- Tres programas: **Docker Desktop**, **Git** y **Make**. No hace falta saber programar ni instalar nada más: el resto corre dentro de Docker.

Instálalos según tu sistema:

### Windows 10 u 11

1. Abre el menú Inicio, escribe `PowerShell`, haz clic derecho en **Windows PowerShell** y elige **Ejecutar como administrador**. Escribe este comando y presiona Enter:
   ```
   wsl --install
   ```
   Reinicia el computador cuando termine. Al volver se abre una ventana de **Ubuntu** que te pide crear un usuario y una contraseña (los que quieras). Mientras escribes la contraseña no se ve nada: es normal.
2. Descarga e instala [Docker Desktop](https://www.docker.com/products/docker-desktop/). Ábrelo, entra a **Settings → Resources → WSL Integration**, activa **Ubuntu** y presiona **Apply & restart**.
3. Abre **Ubuntu** desde el menú Inicio y ejecuta:
   ```
   sudo apt update && sudo apt install -y git make
   ```

**Importante:** en Windows, todos los comandos de aquí en adelante se escriben en la ventana de **Ubuntu**, no en PowerShell.

### macOS

1. Descarga e instala [Docker Desktop](https://www.docker.com/products/docker-desktop/). Elige la versión de tu Mac: **Apple Silicon** o **Intel** (lo ves en  → Acerca de este Mac). Ábrelo.
2. Abre la **Terminal** (Cmd + Espacio, escribe `Terminal`) y ejecuta:
   ```
   xcode-select --install
   ```
   Acepta la ventana que aparece. Esto instala Git y Make.

### Linux (Ubuntu o Debian)

1. Instala Docker Engine siguiendo la [guía oficial](https://docs.docker.com/engine/install/ubuntu/).
2. En la terminal:
   ```
   sudo apt install -y git make
   sudo usermod -aG docker $USER
   ```
3. Cierra sesión y vuelve a entrar, para poder usar Docker sin `sudo`.

### Comprueba que todo quedó instalado

Con Docker Desktop abierto, ejecuta en la terminal:

```
docker --version
docker compose version
git --version
make --version
```

Cada comando debe responder con un número de versión. Si alguno dice `command not found` o «no se encontró», repite el paso de ese programa.

## Instalación

1. Abre Docker Desktop y espera a que diga que está corriendo.
2. Abre la terminal (en Windows, **Ubuntu**), copia estas líneas, pégalas (clic derecho → Pegar) y presiona Enter:
   ```
   cd ~
   git clone https://github.com/cristhianbarros/govtrace-app.git
   cd govtrace-app
   make setup
   ```
3. Espera. La primera vez descarga y prepara todo, y puede tardar de 10 a 30 minutos según tu internet. Termina cuando la terminal vuelve a aceptar comandos. Si ves un mensaje con `✘` o `Error`, revisa [Si algo falla](#si-algo-falla).

Esto se hace una sola vez.

## Cómo correrlo

1. En la misma terminal, dentro de la carpeta `govtrace-app`, ejecuta:
   ```
   make demo
   ```
   Levanta la aplicación, una red de Stellar propia en tu computador y una veeduría de demostración con reportes ya sellados. Al terminar, muestra las direcciones y las contraseñas.
2. Abre **Chrome** o **Firefox** y entra con cualquiera de estas cuentas:

   | Rol | Dirección | Correo | Contraseña |
   |---|---|---|---|
   | Super Administrador | http://govtrace.localhost:8080 | `admin@demo.govtrace.test` | `Demo#2026Global` |
   | Administrador de la veeduría | http://veeduria-demo.govtrace.localhost:8080 | `admin@veeduria-demo.org` | `Demo#2026Admin` |
   | Veedor | http://veeduria-demo.govtrace.localhost:8080 | `ana.torres@correo.co` | `Demo#2026Veedor` |

   El sitio público (mapa, obras y validador) está en http://veeduria-demo.govtrace.localhost:8080 y no pide cuenta.
3. Para apagarlo: `make down`. Para volver a encenderlo otro día: abre Docker Desktop y la terminal, y ejecuta `cd ~/govtrace-app` y `make demo`.

### Si algo falla

- **`Cannot connect to the Docker daemon`:** Docker Desktop no está abierto. Ábrelo, espera a que diga que está corriendo y repite el comando.
- **`permission denied` … `docker.sock` (Linux):** te faltó el paso 3 de Linux: cerrar sesión y volver a entrar.
- **`port is already allocated` o `address already in use`:** otro programa usa el puerto 8080. Ejecuta `nano .env.docker`, cambia `HTTP_PORT=8080` por `HTTP_PORT=8090`, guarda con Ctrl + O, Enter y Ctrl + X, y repite `make demo`. Después usa `:8090` en lugar de `:8080` en las direcciones.
- **La página no abre:** revisa que la dirección empiece por `http://` (no `https://`) y termine en `:8080`.
- **Falla la descarga y tienes una VPN encendida:** apágala y repite el comando. Si sigue fallando, `make doctor` dice qué pasa con la red.
