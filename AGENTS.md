# AGENTS.md

Guía de trabajo para agentes (humanos o IA) que editan este repositorio.

## 1. Propósito del repositorio

Este repositorio contiene el contenido de una asignatura que enseña, de forma
gamificada: programación orientada a objetos, Git, Java, Maven, Spring,
algoritmos y patrones de diseño.

El contenido se organiza como un mapa:

- Cada **unidad** de la asignatura es un directorio raíz y, en la ficción del
  juego, una **isla**.
- Los subdirectorios de una unidad son **subsecciones**, **desafíos**
  (prácticos o teóricos) o **contenido teórico** en Markdown.
- El repositorio es la **fuente de verdad** del contenido y de su estructura.
- El sitio web que publica el contenido todavía no tiene un contrato de formato
  definido. Por eso este documento define un esquema provisional y centralizado.
  No inventes formatos alternativos por tu cuenta.

## 2. Principios de trabajo

1. **No improvises estructura.** Antes de crear, mover o renombrar contenido,
   leé el `roadmap.yml` de la raíz, el de la unidad y el del directorio destino.
2. **Un directorio, un tipo.** No mezcles teoría, subsecciones y desafíos en el
   mismo directorio. Si hace falta mezclar, creá subdirectorios.
3. **Metadatos centralizados.** La metadata estructural y editorial vive en
   `roadmap.yml`. Los archivos `.md` contienen contenido, no frontmatter.
4. **Contenido en español.** Títulos, consignas, explicaciones y textos de
   interfaz en español. Nombres de archivos, slugs, IDs y claves de metadata en
   kebab-case ASCII, sin acentos ni espacios. Los directorios de contenido
   agregan un prefijo numérico de tres cifras (`001-`, `002-`) delante del slug
   para mantenerlos ordenados en el repositorio.
5. **Estabilidad de referencias.** Los `id` y `slug` son contratos. Cambiarlos
   exige actualizar todas las referencias en el mismo cambio.
6. **Cambios mínimos y coherentes.** Seguí el estilo de los directorios vecinos.
   No reestructures contenido ajeno al pedido.
7. **No publiques ni confirmes cambios** (`git commit`, `git push`, estados
   `published`) salvo pedido explícito.
8. **No agregues tooling, dependencias ni archivos generados** sin aprobación.

## 3. Modelo mental del contenido

Cada nodo del árbol de contenido es un directorio con un `roadmap.yml`.

```text
contenido-progra-3/
├── AGENTS.md
├── roadmap.yml                  # catálogo raíz (orden de islas y assets globales)
├── assets/                      # material formal, NO es una unidad
│   └── git/
│       └── manual-git.pdf
├── 001-bienvenida-y-onboarding/ # unidad / isla
│   ├── roadmap.yml
│   ├── 001-bienvenida-a-la-aventura/   # teoría
│   │   ├── roadmap.yml
│   │   └── 01-bienvenida-a-la-aventura.md
│   ├── 002-exploracion-del-roadmap/    # teoría
│   │   ├── roadmap.yml
│   │   └── 01-exploracion-del-roadmap.md
│   ├── 003-las-reglas-del-juego/       # teoría
│   │   ├── roadmap.yml
│   │   └── 01-las-reglas-del-juego.md
│   ├── 004-prueba-del-explorador/      # desafío teórico
│   │   ├── roadmap.yml
│   │   ├── consigna.md
│   │   ├── preguntas.yml
│   │   └── respuestas.yml
│   └── 005-campamento-base/            # subsección de onboarding
│       ├── roadmap.yml
│       └── ...                         # instalación y validación de herramientas
├── 002-git/
│   └── roadmap.yml
├── 003-java/
│   └── roadmap.yml
├── 004-maven/
│   └── roadmap.yml
├── 005-testing/
│   └── roadmap.yml
├── 006-algoritmos/
│   └── roadmap.yml
├── 007-patrones-de-diseno/
│   └── roadmap.yml
└── 008-microservicios-y-spring/
    └── roadmap.yml
```

### 3.1 Prefijo numérico de directorios

- Todo directorio de contenido (unidad, subsección, teoría o desafío) se nombra
  `NNN-<slug>`, con exactamente tres dígitos y un guion: `002-git`,
  `002-desafios`, `001-primer-commit`.
- `NNN` es único entre hermanos y debe respetar el `order` declarado por el
  padre. No hace falta que sea consecutivo, pero sí creciente según el orden.
- El `slug` y el `id` **no** incluyen el prefijo: el directorio `002-git`
  corresponde a `slug: git` e `id: git`.
- En `children` y `units`, `path` es el nombre completo del directorio,
  incluyendo el prefijo: `path: 001-introduccion`.
- Si se reordena un grupo, renombrá los directorios y actualizá los `path` en el
  mismo cambio. El prefijo es una ayuda de lectura; el orden oficial sigue
  siendo el `order` del padre.
- El prefijo aplica a directorios, no a archivos.
- `assets/` y sus subdirectorios son la excepción: no se numeran, para no atar
  las URLs de los materiales a la progresión de las unidades.

Reglas del árbol:

- `assets/` es un directorio reservado de infraestructura. No es una isla y no
  lleva `roadmap.yml` propio; su metadata se declara donde se referencia.
- Todo directorio de contenido (unidad, subsección, teoría o desafío) debe tener
  exactamente un `roadmap.yml`.
- El orden de los hijos lo define el **padre** en `children` o `units`, no el
  hijo.
- No debe haber directorios de contenido huérfanos: todo directorio debe estar
  declarado por su padre.
- Un directorio de teoría contiene páginas `.md` en su mismo nivel. No contiene
  subdirectorios de contenido.
- Un desafío contiene sus archivos canónicos (`consigna.md`, etc.). Si necesita
  más material, usa `recursos/`.

## 4. Contrato de `roadmap.yml`

### 4.1 Reglas generales

- Formato YAML 1.2, codificación UTF-8, indentación de 2 espacios.
- Todo roadmap empieza con `schemaVersion: 1`.
- Claves de metadata en inglés; valores de contenido en español.
- Valores de enumeración en inglés (`draft`, `in-review`, `published`,
  `beginner`, `intermediate`, `advanced`).
- Un `id` es único en todo el repositorio y estable. Formato recomendado:
  ruta de slugs separada por `/`, por ejemplo `git/desafios/primer-commit`. El
  `id` nunca incluye los prefijos numéricos de los directorios.
- Un `slug` es único entre hermanos y se deriva del nombre del directorio sin su
  prefijo numérico.
- En `children` y `units`, `path` debe ser el nombre completo del directorio
  hijo, incluyendo el prefijo (`001-introduccion`), y debe existir.
- Los `id` de prerequisitos deben existir y formar un grafo sin ciclos.
- `summary` tiene una o dos oraciones (idealmente menos de 200 caracteres).
- Las fechas usan ISO 8601 (`YYYY-MM-DD`).
- Rutas de archivos y assets: siempre relativas a la raíz del repositorio y
  comenzando con `/`, por ejemplo `/assets/git/manual-git.pdf`.
- No agregues campos nuevos sin actualizar este documento y todos los roadmaps
  afectados en el mismo cambio.

Campos comunes a todos los nodos (excepto el catálogo raíz):

| Campo | Obligatorio | Descripción |
| --- | --- | --- |
| `schemaVersion` | sí | Versión del contrato. Actualmente `1`. |
| `type` | sí | Tipo de nodo (ver tabla de tipos). |
| `id` | sí | Identificador global y estable. |
| `slug` | sí | Identificador legible único entre hermanos. |
| `title` | sí | Título visible, sin punto final. |
| `summary` | sí | Descripción breve para navegación y tarjetas. |
| `status` | sí | `draft`, `in-review` o `published`. |
| `tags` | no | Lista de etiquetas en kebab-case. |
| `prerequisites` | no | IDs de nodos que deben completarse antes. Lista vacía si no hay. |
| `gamification` | según tipo | Recompensas, dificultad, isla, mapa. |
| `updated` | no | Fecha de la última revisión de contenido. |
| `children` | según tipo | Hijos directos con su orden. |

Formato de un hijo:

```yaml
children:
  - path: 001-introduccion   # nombre del directorio, no ruta completa
    order: 1
```

`path` debe ser un directorio hijo inmediato que exista y tenga su propio
`roadmap.yml`. El `order` debe ser único entre hermanos.

### 4.2 Tipos de nodo

| `type` | Qué representa | Contenido esperado |
| --- | --- | --- |
| `catalog` | Raíz del repositorio. Solo existe uno. | `units` y assets globales. |
| `unit` | Unidad de la asignatura / isla. | `children`, datos de isla y recompensa. |
| `section` | Subsección dentro de una unidad. | `children`; puede tener gamificación propia. |
| `theory` | Lectura teórica. | `pages` con archivos `.md` del directorio. |
| `challenge-practical` | Desafío con código o práctica. | `consigna.md`, plantilla/solución opcionales. |
| `challenge-theory` | Desafío de preguntas. | `consigna.md`, `preguntas.yml`, `respuestas.yml`. |

### 4.3 Catálogo raíz

Archivo: `/roadmap.yml`. No es una isla ni un nodo gamificado.

```yaml
schemaVersion: 1
type: catalog
title: Mapa de la asignatura
summary: Recorrido completo por las islas de la asignatura.
units:
  - path: 001-bienvenida-y-onboarding
    order: 1
  - path: 002-git
    order: 2
  - path: 003-java
    order: 3
  # ... continúa con el resto de las unidades
assets:
  - file: /assets/bienvenida-y-onboarding/guia-general.pdf
    title: Guía general de la asignatura
    kind: pdf
    description: Material formal de lectura inicial.
```

Reglas:

- `units` declara todas las unidades raíz y su orden.
- No debe existir un directorio raíz de unidad que no esté en `units`.
- `assets` es opcional y solo para material global, no asociado a una unidad.

### 4.4 Unidad / isla

```yaml
schemaVersion: 1
type: unit
id: git
slug: git
title: El Bosque de las Ramas
summary: Control de versiones con Git, desde el primer commit hasta el trabajo con ramas.
status: draft
tags:
  - git
  - control-de-versiones
prerequisites: []
updated: 2026-10-22
gamification:
  island:
    name: El Bosque de las Ramas
    theme: Un bosque donde cada rama abre un camino distinto.
children:
  - path: 001-introduccion
    order: 1
  - path: 002-desafios
    order: 2
assets:
  - file: /assets/git/manual-git.pdf
    title: Manual de Git
    kind: pdf
    description: Lectura formal complementaria de la unidad.
    required: false
```

Este nodo vive en el directorio `002-git/`. Las coordenadas del mapa y las
recompensas se agregan cuando el material de la asignatura las defina.

Reglas:

- `gamification.island` es obligatorio en una unidad.
- No inventes nombres de islas, temas, recompensas ni coordenadas si no están
  definidos en el material de la asignatura. Si falta ese dato, dejá el nodo en
  `draft` y registrá la duda.
- `assets` declara material formal de la unidad que vive en `/assets/`.
- Los objetivos pedagógicos opcionales van en `objectives` como lista de textos.

### 4.5 Subsección

```yaml
schemaVersion: 1
type: section
id: git/desafios
slug: desafios
title: Desafíos de Git
summary: Actividades para practicar lo aprendido en la unidad.
status: draft
prerequisites: []
gamification:
  xp: 50
children:
  - path: 001-primer-commit
    order: 1
  - path: 002-modelo-mental
    order: 2
```

Reglas:

- `children` debe tener al menos un hijo.
- `gamification` es opcional; si se usa, debe ser coherente con la unidad.
- Una subsección no contiene páginas `.md` propias: esas páginas van en un
  nodo `theory` o en un desafío.

### 4.6 Teoría

```yaml
schemaVersion: 1
type: theory
id: git/introduccion
slug: introduccion
title: Introducción a Git
summary: Modelo mental de repositorio, commit y rama.
status: draft
tags:
  - fundamentos
  - commits
prerequisites: []
pages:
  - file: 01-que-es-git.md
    slug: que-es-git
    title: ¿Qué es Git?
    summary: Modelo mental de repositorio, commit y rama.
    estimatedMinutes: 10
  - file: 02-instalacion.md
    slug: instalacion
    title: Instalación y configuración
    summary: Preparación del entorno local.
    estimatedMinutes: 15
```

Este nodo vive en el directorio `001-introduccion/` y las páginas de `pages`
están en ese mismo nivel.

Reglas:

- `pages` declara todas las páginas del directorio y su orden.
- Cada `file` debe existir en el mismo directorio y terminar en `.md`.
- Cada página tiene `slug` único dentro del nodo, `title` y `summary`.
- No agregues páginas `.md` no declaradas en `pages`.
- No uses frontmatter en los `.md`; la metadata vive en `roadmap.yml`.

### 4.7 Desafío práctico

```yaml
schemaVersion: 1
type: challenge-practical
id: git/desafios/primer-commit
slug: primer-commit
title: Primer commit
summary: Crear un repositorio y registrar el primer cambio.
status: draft
tags:
  - commits
prerequisites:
  - git/introduccion
difficulty: beginner
estimatedMinutes: 30
gamification:
  xp: 100
  badge: primer-commit
validation:
  mode: site
  siteRef: git-primer-commit
contents:
  statement: consigna.md
  starter: plantilla
  solution: solucion
  resources: recursos
publishSolution: false
```

Este desafío vive en el directorio `002-desafios/001-primer-commit/`.

Reglas:

- `validation.mode` es `site`. La validación **no** se ejecuta en este
  repositorio. `siteRef` es opcional y lo define el sitio cuando exista.
- `consigna.md` es obligatorio.
- `plantilla/`, `solucion/` y `recursos/` son opcionales; si se declaran en
  `contents`, deben existir.
- `publishSolution: false` por defecto. No expongas la solución en la consigna.
- No agregues tests locales salvo que el sitio o el pedido lo exijan.

### 4.8 Desafío teórico

```yaml
schemaVersion: 1
type: challenge-theory
id: git/desafios/modelo-mental
slug: modelo-mental
title: Modelo mental de Git
summary: Comprobar la comprensión de repositorio, commit y rama.
status: draft
tags:
  - fundamentos
prerequisites:
  - git/introduccion
difficulty: beginner
estimatedMinutes: 10
gamification:
  xp: 40
validation:
  mode: site
  siteRef: git-modelo-mental
contents:
  statement: consigna.md
  questions: preguntas.yml
  solution: respuestas.yml
publishSolution: false
```

Este desafío vive en el directorio `002-desafios/002-modelo-mental/`.

`preguntas.yml` contiene solo lo que ve el alumno:

```yaml
schemaVersion: 1
questions:
  - id: q1
    type: multiple-choice
    prompt: ¿Qué guarda un commit?
    options:
      - id: a
        text: Solo el último archivo modificado.
      - id: b
        text: Una instantánea del estado del proyecto y su metadata.
      - id: c
        text: Únicamente el mensaje de commit.
```

`respuestas.yml` contiene la clave y no debe publicarse:

```yaml
schemaVersion: 1
answers:
  - question: q1
    correct: b
    explanation: Un commit registra una instantánea y metadata asociada.
```

Reglas:

- Los IDs de preguntas son únicos dentro del desafío.
- No incluyas la respuesta correcta en `preguntas.yml`.
- Si el sitio define otro esquema de preguntas, actualizá este documento y el
  adaptador correspondiente; no cambies los archivos de forma especulativa.

## 5. Markdown

- Sin frontmatter. La metadata está en `roadmap.yml`.
- No repitas el título del roadmap como `# H1`. Empezá el contenido con una
  introducción breve y usá `##` en adelante.
- Una idea principal por página. Párrafos cortos y ejemplos concretos.
- Bloques de código con lenguaje explícito (` ```java `, ` ```bash `, etc.).
- Enlaces descriptivos, nunca "click aquí".
- Las imágenes deben tener texto alternativo y apuntar a `/assets/...`.
- No uses HTML salvo que sea imprescindible.
- Codificación UTF-8 y saltos de línea LF. Sin espacios al final de línea.
- Escribí en español claro y neutro. Mantené el registro de la unidad; no
  introduzcas regionalismos nuevos sin motivo.
- Definí los términos en su primera aparición. Los identificadores de código
  conservan las convenciones del lenguaje.
- En desafíos, no reveles la solución en la consigna. Usá `## Objetivo`,
  `## Consigna`, `## Criterios de aceptación` y, si corresponde, `## Pistas`
  dentro de un bloque desplegable o sección aparte.

## 6. Assets

`/assets/` contiene material formal de lectura y recursos de contenido: PDFs,
imágenes, diagramas, videos u otros formatos.

Estructura:

```text
/assets/<unidad>/<tema>/<archivo>.<ext>
```

Reglas:

- `<unidad>` es el slug de la unidad, sin el prefijo numérico del directorio.
- Nombres en kebab-case ASCII, sin espacios ni acentos.
- Un asset pertenece a una unidad salvo que sea global; los globales se declaran
  en el roadmap raíz.
- Todo asset referenciado desde contenido debe estar declarado en el `assets`
  del roadmap de la unidad (o en el raíz si es global), con `title`, `kind` y
  `description`.
- Toda imagen usada en un `.md` debe estar en `/assets/`; no guardes imágenes
  junto al Markdown.
- No muevas, renombres ni borres un asset sin actualizar todas las referencias.
- No dupliques assets para evitar dependencias; enlazá el existente.
- No subas binarios grandes, material con derechos dudosos ni archivos
  personales. Si falta licencia o fuente, registralo como pendiente.
- Los PDFs y documentos formales son de solo lectura para los agentes: no los
  edites sin pedido explícito.

## 7. Gamificación

- La unidad es la isla; su metadata va en `gamification.island`.
- `map.x` y `map.y` son coordenadas enteras en un sistema compartido que
  definirá el sitio/mapa. No las inventes.
- `prerequisites` es el mecanismo de desbloqueo. Debe ser un DAG.
- Cada desafío puede otorgar `xp`, `badge` y tener `difficulty`.
- La dificultad permitida es `beginner`, `intermediate` o `advanced`.
- No otorgues XP ni badges arbitrariamente: seguí la progresión de la unidad.
- Mantené los nombres de islas, insignias y regiones estables una vez definidos.

## 8. Flujos de trabajo

### Antes de editar

1. Leé este archivo completo.
2. Leé `/roadmap.yml`, el roadmap de la unidad y el roadmap del directorio más
   cercano al cambio.
3. Revisá `git status` y el contenido vecino para respetar el estilo.
4. Si el cambio afecta estructura, identificá todos los `id`, enlaces y assets
   que podrían romperse.

### Agregar una unidad

1. Creá el directorio raíz `NNN-<slug>` con el prefijo que corresponda al orden.
2. Creá su `roadmap.yml` con `type: unit`, id, isla, recompensa y `children`.
3. Agregá la unidad a `units` del roadmap raíz con `path: NNN-<slug>` y el orden
   correcto.
4. Declará sus assets en el roadmap de la unidad.
5. Verificá que no existan colisiones de `id`, `slug`, `path` ni `order`.

### Agregar una subsección

1. Creá el directorio hijo `NNN-<slug>`.
2. Creá su `roadmap.yml` con `type: section`.
3. Agregalo a `children` del padre con el `path` completo, incluido el prefijo.
4. Si tiene contenido, creá nodos `theory` o desafíos como hijos.

### Agregar teoría

1. Creá el directorio del nodo `NNN-<slug>/` con su `roadmap.yml` y
   `type: theory`.
2. Agregá las páginas `.md` en el mismo directorio.
3. Declaralas en `pages` con orden, slug, título y resumen.
4. Agregá el nodo a `children` del padre con su `path` completo.
5. Revisá enlaces a assets y prerequisitos.

### Agregar un desafío

1. Creá el directorio `NNN-<slug>/` con su `roadmap.yml` y el tipo
   correspondiente.
2. Escribí `consigna.md` sin revelar la solución.
3. Para desafíos prácticos, agregá `plantilla/` y `solucion/` si corresponde.
4. Para desafíos teóricos, agregá `preguntas.yml` y `respuestas.yml`.
5. Agregalo a `children` del padre con su `path` completo y conectá
   `prerequisites` y `xp`.
6. Verificá que `validation.mode` sea `site`.

### Mover, renombrar o eliminar

1. Actualizá el `children` del padre viejo y del nuevo en el mismo cambio.
2. Si cambia el orden, renombrá los directorios con el nuevo prefijo `NNN-` y
   actualizá todos los `path` afectados.
3. Actualizá `id`, `slug` y todas las referencias (`prerequisites`, enlaces,
   assets) en el mismo cambio. Recordá que `id` y `slug` no llevan prefijo.
4. Buscá el nombre viejo en todo el repositorio antes de terminar.
5. No dejes nodos huérfanos ni enlaces rotos.
6. Si se retira contenido, eliminá también sus entradas de metadata y assets
   exclusivos, salvo que se indique archivarlo.

## 9. Validación antes de terminar

No hay tooling de validación en el repositorio todavía. Si en el futuro se
agrega, usalo. Mientras tanto, verificá manualmente:

- [ ] Cada `roadmap.yml` es YAML válido y tiene `schemaVersion: 1`.
- [ ] `type` es uno de los valores permitidos.
- [ ] Los campos obligatorios del tipo están completos.
- [ ] Los `id` son únicos y los `slug` son únicos entre hermanos.
- [ ] Todo directorio de contenido se llama `NNN-<slug>` y su prefijo respeta
      el orden del padre.
- [ ] Los `path` de `children` y `units` incluyen el prefijo y coinciden con el
      nombre real del directorio.
- [ ] Los `id` y `slug` no incluyen el prefijo numérico.
- [ ] Todos los `children` existen, tienen roadmap y están ordenados.
- [ ] No hay directorios de contenido huérfanos.
- [ ] Todos los `prerequisites` existen y no hay ciclos.
- [ ] Todas las `pages` y `contents` apuntan a archivos existentes.
- [ ] Todos los enlaces y assets referenciados existen.
- [ ] No quedaron referencias al nombre viejo tras un rename.
- [ ] El contenido está en español y los archivos usan kebab-case ASCII.
- [ ] Los bloques de código tienen lenguaje y los ejemplos son coherentes.
- [ ] `git diff --check` no reporta errores de espacios.
- [ ] Revisaste el diff completo antes de dar por terminado.

Si el cambio toca código Java/Maven, compilá o ejecutá las pruebas de la unidad
con las instrucciones que existan en esa unidad. No inventes comandos de build ni
dependencias.

## 10. Qué no debe hacer un agente

- Inventar tipos, campos, estados, coordenadas, recompensas o un esquema del
  sitio.
- Cambiar `id` o `slug` sin actualizar todas las referencias.
- Incluir el prefijo numérico en `id`, `slug` o nombres de archivos.
- Renombrar o renumerar directorios sin actualizar los `path` y enlaces.
- Mezclar tipos de contenido en un mismo directorio.
- Editar assets formales sin pedido explícito.
- Duplicar contenido entre páginas o entre teoría y consignas.
- Introducir frontmatter en `.md` mientras el contrato use `roadmap.yml`.
- Agregar tests, dependencias, CI o scripts de build sin aprobación.
- Publicar (`status: published`) o commitear sin pedido explícito.
- Reformatear archivos ajenos al cambio.

## 11. Pendientes del contrato con el sitio

El sitio web todavía no está definido. Cuando se conozca, este documento debe
actualizarse con una sección **Contrato con el sitio** que cubra, como mínimo:

- Formato de entrada: Markdown, MDX, JSON, API u otro.
- Campos obligatorios, rutas, slugs, orden y estados de publicación.
- Cómo se representan teoría, desafíos, preguntas y soluciones.
- Payload de validación de desafíos prácticos: tests, comandos, timeouts,
  lenguajes y visibilidad de resultados.
- Modelo de XP, badges, desbloqueos, mapa y coordenadas.
- Hosting de assets, reescritura de URLs y límites de tamaño.
- Formato de preguntas, tipos soportados y confidencialidad de respuestas.
- Necesidad de un exportador o script de sincronización.

Hasta entonces:

- No adaptes todo el repositorio a un formato supuesto.
- Mantené la metadata en `roadmap.yml` y los `.md` sin frontmatter.
- Si un dato del sitio es imprescindible, dejá el contenido en `draft` y
  registrá la duda en el resumen del cambio o en el roadmap correspondiente.

## 12. Evolución de este documento

- Cambios compatibles: agregar campos opcionales o tipos nuevos, documentados
  aquí y en los roadmaps afectados.
- Cambios incompatibles: incrementar `schemaVersion`, actualizar este documento,
  migrar todos los roadmaps en el mismo cambio y dejar constancia.
- Este archivo es la referencia principal para agentes. Si una instrucción del
  pedido contradice el repositorio, priorizá la estructura existente y consultá
  antes de romper el contrato.
