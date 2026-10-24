## Qué vas a instalar

Maven es una herramienta para construir y gestionar proyectos Java. Vas a usarla
para compilar, ejecutar pruebas y empaquetar aplicaciones.

## Antes de empezar

Asegurate de tener Java 21 activo:

```bash
java -version
```

## Instalación

Instalá Maven con SDKMAN:

```bash
sdk install maven
```

Si ya tenías Maven instalado, SDKMAN te pedirá confirmar si querés establecer
esta versión como predeterminada. Aceptá para usar la versión gestionada por
SDKMAN.

## Verificación

Ejecutá:

```bash
mvn -version
```

La salida debe mostrar la versión de Maven y la versión de Java en uso. Revisá
que aparezca Java 21.

Si Maven muestra otra versión de Java, verificá que Java 21 sea la versión
predeterminada en SDKMAN y abrí una terminal nueva.

## Siguiente paso

Cuando la verificación funcione, resolvé la validación de Maven.
