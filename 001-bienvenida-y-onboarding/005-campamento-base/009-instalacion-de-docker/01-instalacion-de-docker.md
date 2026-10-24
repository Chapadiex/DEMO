## Qué vas a instalar

Docker permite ejecutar aplicaciones dentro de contenedores. En la asignatura lo
vas a usar para levantar servicios y reproducir entornos de desarrollo.

## Antes de empezar

Verificá si Docker ya está instalado:

```bash
docker --version
```

## Instalación

### Windows y macOS

1. Descargá Docker Desktop desde https://docs.docker.com/get-docker/.
2. Ejecutá el instalador y seguí las instrucciones para tu sistema.
3. Abrí Docker Desktop y esperá a que el motor de Docker esté iniciado.

En Windows, Docker Desktop puede requerir WSL 2. El instalador te indica si
necesitás habilitarlo.

### Linux

Instalá Docker Engine siguiendo la guía oficial para tu distribución en
https://docs.docker.com/engine/install/.

Después de instalarlo, verificá que el servicio esté iniciado y que tu usuario
tenga los permisos necesarios para usar Docker.

## Verificación

Ejecutá:

```bash
docker --version
docker run hello-world
```

El primer comando muestra la versión del cliente. El segundo descarga y ejecuta
un contenedor de prueba; si ves un mensaje de bienvenida, Docker está
funcionando.

Si `docker run` falla porque el motor no está iniciado, abrí Docker Desktop o
iniciá el servicio de Docker según tu sistema operativo.

## Siguiente paso

Cuando la verificación funcione, resolvé la validación de Docker.
