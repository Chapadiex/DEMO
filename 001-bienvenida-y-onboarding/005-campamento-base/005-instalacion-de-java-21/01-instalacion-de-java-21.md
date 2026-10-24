## Qué vas a instalar

Java 21 es una versión LTS (Long Term Support) del JDK. En la asignatura vas a
usar esta versión para compilar y ejecutar los ejemplos y desafíos.

## Antes de empezar

Asegurate de tener SDKMAN funcionando. Podés comprobarlo con:

```bash
sdk version
```

## Instalación

Listá las versiones disponibles de Java:

```bash
sdk list java
```

Elegí la última versión 21.x de una distribución, por ejemplo Temurin. El
identificador exacto aparece en el listado. Luego instalala y establecela como
versión predeterminada:

```bash
sdk install java 21.0.5-tem
sdk default java 21.0.5-tem
```

Reemplazá `21.0.5-tem` por el identificador exacto que hayas elegido.

## Verificación

Ejecutá:

```bash
java -version
javac -version
```

Ambos comandos deben mostrar la versión 21. Si `java -version` muestra otra
versión, volvé a ejecutar `sdk default java` con el identificador correcto y
abrí una terminal nueva.

## Siguiente paso

Cuando la verificación funcione, resolvé la validación de Java 21.
