## Qué vas a instalar

SDKMAN es un gestor de versiones para herramientas del ecosistema Java. En este
curso lo vas a usar para instalar y cambiar entre versiones de Java y Maven.

## Antes de empezar

Abrí Git Bash en Windows o la terminal en macOS y Linux. En Windows, SDKMAN se
usa desde el entorno que indique la cátedra (Git Bash o WSL).

Necesitás tener `curl` y `unzip` disponibles. En la mayoría de las instalaciones
de Git Bash y de macOS o Linux ya vienen incluidos.

## Instalación

Ejecutá el instalador oficial:

```bash
curl -s "https://get.sdkman.io" | bash
```

Cuando termine, cargá SDKMAN en la sesión actual:

```bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
```

El instalador también agrega la inicialización a tu archivo de configuración de
la terminal para que esté disponible en las próximas sesiones.

## Verificación

Ejecutá:

```bash
sdk version
```

Deberías ver una salida similar a `SDKMAN 5.x.x`. Si `sdk` no se reconoce, cerrá
y volvé a abrir la terminal o ejecutá nuevamente el comando `source`.

## Siguiente paso

Cuando la verificación funcione, resolvé la validación de SDKMAN.
