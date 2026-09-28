# Funcionalidades del Lector de Libros

Este documento reúne **todas** las funcionalidades discutidas hasta ahora: las que salieron del análisis de Calibre, las que definimos como diferenciadores propios, y las nuevas que agregaste en tu lista. Cada una incluye una explicación clara y un ejemplo de uso real.

> 📌 Al final de cada categoría se indica si la funcionalidad ya estaba en el cuadro anterior o es **nueva** (aportada por ti).

---

## 1. Gestión de biblioteca

### Importar libros arrastrando y soltando
El sistema detecta automáticamente el formato del archivo al soltarlo en la ventana, sin que el usuario tenga que especificar nada.
**Ejemplo:** arrastras `El_Hobbit.epub` y `Dune.cbz` juntos a la biblioteca; el sistema los identifica y cataloga como libro y cómic respectivamente, sin pasos adicionales.
*(Nueva — no estaba explícita en el cuadro anterior, se daba por hecho dentro de "importar")*

### Metadatos automáticos (portada, sinopsis, ISBN)
Al importar un libro, el sistema busca en fuentes externas (Google Books, Open Library) y completa portada, autor, año, sinopsis e ISBN sin intervención manual.
**Ejemplo:** subes un EPUB llamado `mishima_confesiones.epub` sin metadatos; el sistema identifica "Confesiones de una máscara" de Yukio Mishima y rellena automáticamente la ficha completa.
*(Ya estaba en el cuadro)*

### Fusionar libros duplicados o fusionar formatos del mismo libro
Si tienes el mismo título en dos formatos distintos (o dos copias), el sistema los reconoce y los une en **una sola entrada** con ambos archivos disponibles, en lugar de duplicar la ficha en tu biblioteca.
**Ejemplo:** tienes `1984.epub` y `1984.pdf` importados por separado; el sistema detecta que son el mismo libro (por título+autor o hash) y los fusiona en una sola tarjeta con selector de formato al abrir.
*(Nueva — antes estaba solo como "comparador de duplicados" descartado; ahora se especifica como fusión automática, que es una función distinta y más útil)*

### Columnas personalizadas
El usuario puede crear sus propios campos de metadatos, no limitados a los predefinidos (título, autor, tags...).
**Ejemplo:** creas una columna "Leído en papel: sí/no" o "Prestado a: [nombre]" y la usas como filtro de búsqueda igual que cualquier otro campo del sistema.
*(Nueva — no estaba en el cuadro)*

### Búsquedas avanzadas con operadores + búsquedas guardadas
Permite construir filtros complejos combinando campos y operadores lógicos, y guardarlos como accesos reutilizables.
**Ejemplo:** `author:Tolkien and rating:>=4 and status:terminado` guardado como "Tolkien favoritos" — un clic y siempre ves ese filtro actualizado, sin rehacerlo.
*(Nueva versión más específica — el cuadro anterior solo tenía "búsqueda full-text", esto es un nivel adicional: **búsqueda estructurada por campos**, no solo texto libre)*

---

## 2. Lectura

### Visor integrado (modo página/scroll, notas, búsqueda de texto, diccionario, modo noche)
El lector interno soporta ambos modos de navegación, permite anotar directamente, buscar cualquier palabra dentro del libro abierto, consultar el diccionario con clic derecho sobre una palabra, y cambiar a modo noche.
**Ejemplo:** lees de noche, activas modo noche (fondo negro, texto gris claro), y al encontrar una palabra desconocida haces clic derecho sobre ella para ver su definición sin salir de la página.
*(Ya estaba en el cuadro, como varias funciones separadas: temas, subrayados, diccionario, búsqueda de texto — aquí se agrupan)*

### Ajustar tipografía y estilos sin alterar el archivo original
Los cambios de fuente, tamaño o interlineado son una capa de presentación separada del archivo fuente; el EPUB/PDF original nunca se modifica en disco.
**Ejemplo:** cambias la fuente de "Georgia" a "OpenDyslexic" para lectura más cómoda; si envías el mismo libro a otro dispositivo o usuario, el archivo original sigue intacto con su tipografía por defecto.
*(Ya estaba en el cuadro, dentro de "tipografía ajustable")*

---

## 3. Servidor y acceso remoto

### Content Server (servidor local + acceso web)
El sistema puede levantar un servidor accesible desde cualquier navegador en la red local (o internet, si se configura), permitiendo ver y leer la biblioteca sin instalar nada.
**Ejemplo:** activas el servidor en tu PC de casa, y desde el navegador del móvil de un familiar (sin la app instalada) entras a `http://tu-ip:puerto` y lees directamente ahí.
*(Ya estaba en el cuadro)*

### Compatibilidad con apps OPDS de terceros
OPDS es un estándar abierto para catálogos de libros; al ser compatible, cualquier app lectora externa que soporte OPDS puede "ver" tu biblioteca como si fuera una tienda/catálogo remoto.
**Ejemplo:** usas la app KyBook o Moon+ Reader en tu móvil, agregas la URL OPDS de tu servidor, y navegas/descargas libros desde ahí sin usar la app propia del proyecto.
*(Ya estaba en el cuadro)*

---

## 4. Extensibilidad

### Sistema de plugins de terceros
Arquitectura abierta que permite a la comunidad crear extensiones sin tocar el núcleo del programa: integraciones, utilidades, conectores externos.
**Ejemplo:** alguien crea un plugin que sincroniza tus reseñas con Goodreads automáticamente, sin que ese código forme parte del núcleo oficial del proyecto.
*(Ya estaba en el cuadro, marcado como "no mencionado como objetivo" — sigue pendiente de decisión)*

---

## 5. Utilidades

### Generador automático de portadas
Si un libro no trae portada (común en TXT o EPUBs mal formados), el sistema genera una automáticamente usando título y autor como base visual.
**Ejemplo:** importas un TXT sin metadatos; el sistema genera una portada simple con el título centrado sobre un fondo de color derivado del género o etiqueta asignada.
*(Ya estaba en el cuadro)*

### Comparador de ediciones
Permite ver las diferencias de contenido entre dos versiones/ediciones del mismo libro (texto añadido, corregido o eliminado).
**Ejemplo:** tienes la edición 2010 y la edición revisada 2020 de un mismo ensayo; el sistema resalta qué párrafos cambiaron entre ambas.
*(Ya estaba en el cuadro, marcada como "no mencionado como objetivo")*

### Backup de biblioteca en un solo paso
Genera una copia de seguridad completa (archivos + metadatos + notas + progreso) en una sola acción, exportable o restaurable.
**Ejemplo:** antes de formatear tu equipo, das clic en "Backup completo" y obtienes un único archivo comprimido con todo tu historial de lectura y biblioteca.
*(Ya estaba en el cuadro)*

### Catálogo exportable de biblioteca (PDF/CSV/EPUB)
Genera un listado completo de la biblioteca en un formato compartible, útil para mostrar "qué tienes" sin dar acceso a los archivos.
**Ejemplo:** exportas un PDF con portada, título y autor de los 300 libros de tu biblioteca para compartirlo en un grupo de lectores.
*(Ya estaba en el cuadro)*

---

## 6. Nuevas funcionalidades (aportadas directamente por ti — no estaban en el cuadro)

### 📖 Lista de "por leer" tipo Goodreads, con inicio directo si ya lo tienes
Es una wishlist de libros que **quieres leer** (existan o no en tu biblioteca), pero con una diferencia clave frente a una wishlist normal: si el libro ya está en tu biblioteca local, el sistema lo detecta y te deja **empezar a leerlo directamente desde esa lista**, sin tener que ir a buscarlo aparte.
**Ejemplo:** agregas "Cien años de soledad" a tu lista de pendientes. Si ya tienes el EPUB en tu biblioteca, la tarjeta muestra un botón "Leer ahora" en vez de solo "Buscar/Comprar"; si no lo tienes, muestra "Agregar a biblioteca" o un enlace de búsqueda.

Esta funcionalidad es distinta al simple "estado de lectura" que ya teníamos (por leer/leyendo/terminado) porque introduce el **cruce automático entre intención de lectura y disponibilidad real** — es una capa de conveniencia que ni Calibre ni la mayoría de apps resuelven bien (en Goodreads, por ejemplo, la wishlist nunca sabe si tú ya tienes el archivo).

### ☁️ Conexión con servicios en la nube (Drive, Dropbox, OneDrive, etc.)
Permite vincular cuentas de almacenamiento en la nube para que el sistema **lea directamente los libros guardados ahí**, sin necesidad de descargarlos manualmente a la biblioteca local primero.
**Ejemplo:** conectas tu Google Drive donde tienes una carpeta "Libros" con 200 EPUBs; el sistema los indexa como si fueran parte de tu biblioteca local (metadatos, portadas, progreso), pero el archivo físico permanece en la nube y se transmite/descarga solo cuando lo abres.

Esta es una funcionalidad que **no existía en ningún punto anterior de la conversación** y resuelve un problema real: evita depender de un solo dispositivo como "dueño" de los archivos, y es la base técnica para que la sincronización multi-dispositivo (que ya teníamos como diferenciador) funcione sin fricción — en vez de sincronizar archivos pesados entre dispositivos, todos apuntan a la misma fuente en la nube.

> **Decisión confirmada:** la nube es únicamente almacenamiento de archivos. Todo lo demás (cuentas, progreso, notas, estadísticas, clubes) vive en un **backend propio**. Ver sección 9 para el detalle de esta arquitectura.

---

## 7. Resumen de lo que cambia respecto al cuadro anterior

| Elemento | Estado |
|---|---|
| Importar arrastrando/soltando | Nueva (implícita antes) |
| Fusionar duplicados/formatos | Nueva especificación (antes solo "comparador") |
| Columnas personalizadas | **Nueva** |
| Búsquedas guardadas con operadores | Nueva especificación (antes solo "full-text") |
| Lista "por leer" con inicio directo | **Nueva** |
| Conexión con nube (Drive/Dropbox) | **Nueva** — sin precedente en la conversación |

Todo lo demás en tu lista ya estaba contemplado en el cuadro anterior, solo reorganizado o detallado con más profundidad.

---

## 8. Preguntas resueltas

Las tres preguntas abiertas de la sección anterior ya quedaron decididas:

1. ✅ La nube es solo almacenamiento de archivos; existe un backend propio para cuentas y sincronización.
2. ✅ El sistema de plugins entra en el alcance del proyecto (habilitado por ser open source).
3. ✅ La fusión de duplicados es automática.

El detalle técnico de cada una está en la sección 9.

---

## 9. Decisiones de arquitectura (detalle)

### 9.1 Separación nube ↔ backend propio

Dos responsabilidades completamente distintas que no deben mezclarse:

| | Nube del usuario (Drive/Dropbox/etc.) | Backend propio del proyecto |
|---|---|---|
| **Qué guarda** | Los archivos pesados: EPUB, PDF, CBZ... | Cuentas, metadatos de biblioteca, progreso de lectura, notas/subrayados, estadísticas, clubes de lectura |
| **Rol** | Almacenamiento bruto | Sistema de sincronización y lógica de usuario |
| **Ejemplo** | Tu Drive tiene `dune.epub` | El backend sabe que vas en el capítulo 7, página 142, con 3 subrayados, y que lo empezaste hace 4 días |

**Por qué separarlo así:** si mezclas ambas cosas, quedas atado a que cada proveedor de nube soporte tu lógica de progreso — algo que ningún proveedor de almacenamiento genérico ofrece (Drive no sabe qué es un "subrayado en la posición 4231").

**Pendiente para el diseño técnico:** cuando el usuario abre un libro que vive en la nube, ¿el backend actúa como intermediario (proxy) para leerlo, o el cliente se conecta directo a la nube usando el token de acceso del usuario? La primera opción es más simple de controlar pero carga tu servidor; la segunda es más barata en servidor pero más compleja en el cliente. Se define al hablar del stack.

### 9.2 Sistema de plugins (viable por ser open source)

Al ser open source, la comunidad puede actuar como equipo de desarrollo extendido — así es como Calibre llegó a tener cientos de funciones que un solo desarrollador nunca habría construido solo.

Niveles de exposición posibles, de menor a mayor riesgo/complejidad:

| Nivel | Qué permite | Riesgo | Ejemplo |
|---|---|---|---|
| **Básico** | Hooks de eventos (import, fin de lectura, etc.) que disparan una acción externa | Bajo, fácil de sandboxear | Notificar a Goodreads cuando terminas un libro |
| **Medio** | Nuevas fuentes de metadata o exportadores | Medio, requiere API bien definida | Plugin que busca metadatos en una fuente regional no soportada por defecto |
| **Alto** | Modificar la interfaz o el pipeline de lectura | Alto, difícil de mantener (es lo que hace pesado a Calibre) | Evitar en las primeras versiones |

**Recomendación:** diseñar la arquitectura con el "gancho" de plugins desde el inicio (aunque no se implemente todavía), empezando por niveles básico y medio. Añadir esto después de tener el core ya construido es mucho más costoso que dejarlo previsto desde el diseño de datos y eventos internos.

### 9.3 Fusión automática de duplicados

Automática, pero con dos niveles de confianza para evitar fusiones silenciosas incorrectas:

- **Coincidencia fuerte** (mismo ISBN, o título + autor exactos normalizados) → fusión automática sin preguntar.
- **Coincidencia probable** (título muy similar, autor en formato distinto) → se fusiona automáticamente, pero se muestra un aviso tipo "Se fusionaron X libros, revisar" con opción de deshacer con un clic.

La normalización de título/autor (quitar mayúsculas, tildes, subtítulos) es la base técnica de la comparación cuando no hay ISBN disponible.

---

## 10. Licencia

**AGPL-3.0.** Permite que cualquiera use, modifique y distribuya el proyecto, pero obliga a que toda modificación —incluso si se ofrece como servicio web sin distribuir el binario— se comparta también bajo código abierto. Esto es lo más cercano a "si lo mejoran, esa mejora también debe ser gratuita y abierta para todos" sin salir de la definición formal de Open Source, que es lo que da acceso a comunidad, visibilidad y contribuciones externas.

## 11. Arquitectura offline-first

La app funciona 100% sin conexión; la sincronización es oportunista, no un requisito.

- **SQLite local** en cada dispositivo = fuente de verdad inmediata (biblioteca, progreso, notas — todo funciona sin red)
- El backend (PostgreSQL) deja de ser obligatorio para usar la app y pasa a ser solo el mecanismo de sincronización entre dispositivos cuando hay conexión
- Cada cambio local se guarda con timestamp; al recuperar señal, se reconcilian los cambios entre dispositivos (mismo patrón que usan apps como Obsidian Sync)

## 12. Stack técnico final

| Pieza | Tecnología | Por qué / dónde vive |
|---|---|---|
| Shell de la app (biblioteca, estadísticas, social, ajustes) | **Flutter nativo** | Android + Desktop (Windows/macOS/Linux directo). Prioriza rendimiento en hardware de gama baja: no depende de un puente JS ni de un WebView del sistema variable |
| Motor de lectura (EPUB/PDF) | **`epub.js` + `pdf.js`** (HTML/CSS/JS) | Librerías más maduras del ecosistema para estos formatos; se embebe como WebView dentro de Flutter, y se sirve directo en la versión web |
| Shell web standalone (PWA) | **React o Svelte** (liviano) | Para quien entra por navegador sin instalar nada — prioriza peso mínimo de descarga sobre gama baja de conexión |
| Cómics (CBZ/CBR) | Descompresión + render de imágenes en `<canvas>`/`<img>`, sin motor de lectura de texto | Ver detalle de formatos en la sección 13 |
| MOBI/AZW3 | Parser dedicado (formato menos documentado públicamente, no conviene escribirlo desde cero) | Ver sección 13 |
| Lógica delicada compartida | **Rust** → compilado a nativo (consumido por Flutter vía `dart:ffi`) y a WebAssembly (consumido por React/Svelte) | Normalización para fusión de duplicados, reconciliación de sincronización offline, parseo de contenedores EPUB/CBZ. No dibuja interfaz, es lógica pura reusada por ambos shells |
| Backend | **Node.js/TypeScript + PostgreSQL** | Cuentas, sincronización, clubes de lectura, estadísticas — nunca requisito para que la app funcione |
| Nube del usuario (Drive/Dropbox/etc.) | Conector de almacenamiento | Solo guarda archivos pesados, nunca lógica de progreso (ver sección 9.1) |
| iOS | Sin app nativa por ahora | Cubierto vía PWA instalable desde Safari ("Agregar a inicio"), evita el costo de $99/año y la fricción de revisión de Apple |

**Principio de división:** no se elige un framework único para todo el cliente — se divide por responsabilidad. Flutter donde el rendimiento nativo importa más (navegación, listas, gama baja); el motor de lectura web maduro donde la calidad de renderizado del formato importa más; Rust donde la lógica no debe duplicarse ni divergir entre plataformas.

## 13. Formatos: PDF/EPUB no son toda la historia

Aunque la mayoría de la conversación giró en torno a EPUB y PDF por ser los más comunes, el alcance de formatos ya definido es más amplio y necesita trato diferenciado, no todos son "el mismo problema":

### EPUB / MOBI / AZW3 (texto reflowable)
Comparten la misma naturaleza (HTML/XHTML empaquetado, con capítulos y flujo de texto adaptable). EPUB tiene librerías maduras (`epub.js`); MOBI/AZW3 son formatos propietarios de Amazon, menos documentados públicamente — conviene apoyarse en parsers existentes de la comunidad en vez de escribir el soporte desde cero, y tratarlos como "solo lectura" (sin edición ni conversión) para no entrar en la complejidad que descartamos para Calibre.

### PDF (paginado fijo)
No es texto reflowable — es un lienzo con posiciones fijas. `pdf.js` (el motor de Firefox) ya resuelve el renderizado; lo importante de diseño es que la experiencia de usuario (zoom, recorte de márgenes, modo "reflow" aproximado para pantallas pequeñas) es un problema aparte del de EPUB, no debe compartir la misma lógica de paginación.

### TXT (texto plano)
El caso más simple: no tiene estructura de capítulos ni metadatos. El sistema debe inferir capítulos (por patrones como "Capítulo X" o saltos de línea largos) y generar portada automáticamente (ya contemplado en la sección 5).

### CBZ/CBR — cómics y manga (el punto que señalaste)
Es una categoría con necesidades completamente distintas a un libro de texto, y tienes razón en que pocas apps la tratan en serio en vez de como un añadido menor. No hay "texto" que renderizar — es una secuencia de imágenes (CBZ es un ZIP de imágenes, CBR es RAR). Esto implica:

- **Motor de lectura propio**, no reutilizable del motor EPUB/PDF: paginación por imagen completa, con modos específicos del medio:
  - *Página a página* (una imagen = una pantalla)
  - *Doble página* (para simular el libro abierto, común en manga/cómic físico)
  - *Webtoon/scroll vertical continuo* (el formato dominante en manga/manhwa digital moderno, donde la imagen es una tira larga en vez de páginas separadas)
- **Dirección de lectura configurable**: occidental (izquierda→derecha) vs manga (derecha→izquierda) — esto es un ajuste que casi ninguna app genérica de "libros" contempla, y es justamente el hueco que señalas que existe en el mercado
- **Zoom y recorte de márgenes por imagen**, ya que a diferencia del texto, no hay forma de "reflowar" un cómic — el control de visualización de la imagen es la única herramienta de accesibilidad disponible
- **Metadatos específicos del medio**: numeración de volumen/capítulo en vez de solo título, común en series largas de manga
- **Descompresión**: CBZ es trivial (ZIP estándar); CBR requiere una librería de descompresión RAR, que técnicamente es más pesada de mantener por temas de licencias del formato RAR — conviene evaluar si limitar el soporte nativo a CBZ y ofrecer conversión/recomendación para CBR

Esto refuerza que el "lector de cómics" no debería ser una vista genérica reutilizando el visor de EPUB con imágenes en vez de texto — merece su propio componente de interfaz, con su propia lógica de navegación, para no quedar como una función secundaria mal resuelta, que es justo el vacío que identificaste en las apps existentes.

## 14. Siguiente paso

Con funcionalidades, decisiones de arquitectura y stack ya definidos, el siguiente documento cubre cómo arrancar la implementación en la práctica: estructura del repositorio, orden de construcción, y cómo trabajar esto con asistencia de IA hasta llegar a un MVP funcional antes de publicarlo en GitHub para la comunidad.
