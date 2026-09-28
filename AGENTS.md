# Lector de Libros — Contexto del proyecto

Lector/gestor de libros multiplataforma, open source (AGPL-3.0). Diferenciadores: funciona 100% offline, corre bien en hardware de gama baja, biblioteca con colecciones/etiquetas, estadísticas de lectura, notas, parte social, y soporte serio de cómics (CBZ/CBR).

## Documentos de referencia
- `docs/funcionalidades_lector_libros.md` — todas las funcionalidades y decisiones de arquitectura
- `docs/guia_inicio_desarrollo.md` — orden de fases de construcción; no saltar fases
- `docs/PROGRESO.md` — estado actual del proyecto (lo mantiene el agente ingeniero)

Los dos primeros son largos: léelos solo cuando la tarea lo requiera. Para la mayoría de tareas basta con el archivo de la tarea.

## Stack
- Shell de la app: Flutter (Android + Desktop Windows/macOS/Linux)
- Motor de lectura EPUB/PDF: epub.js + pdf.js embebidos vía WebView; servidos directo en la web
- Web standalone (PWA): React o Svelte, liviano
- Cómics (CBZ/CBR): componente de lectura propio (página a página, doble página, scroll webtoon, dirección occidental/manga)
- Lógica compartida delicada: Rust → nativo (Flutter vía dart:ffi) y WebAssembly (web)
- Backend: Node.js/TypeScript + PostgreSQL — solo sincronización y cuentas, nunca requisito para que la app funcione
- Arquitectura offline-first: SQLite local es la fuente de verdad en cada dispositivo
- iOS: sin app nativa por ahora; cubierto vía PWA instalable desde Safari

## Protocolo de trabajo (dos tipos de sesión sobre la misma carpeta)
- Sesión "ingeniero": planea, decide y revisa. No escribe código de la aplicación.
- Sesión(es) "ejecutor": cada una implementa UNA tarea.
- La comunicación entre sesiones es SOLO por archivos del repositorio. Nunca dependas de lo que el usuario recuerde o resuma.
  1. El ingeniero escribe `tasks/NNN-titulo-corto.md` (formato en `tasks/_PLANTILLA.md`).
  2. El ejecutor lee esa tarea, la implementa y escribe `reports/NNN-titulo-corto.md` (formato en `reports/_PLANTILLA.md`).
  3. El ejecutor hace commit con el mensaje `task NNN: titulo`.
  4. El ingeniero lee el informe y el diff real (`git log`, `git show`), verifica, actualiza `docs/PROGRESO.md` y define la siguiente tarea.
- Numeración correlativa de 3 dígitos (001, 002, ...).
- Tareas en paralelo solo si tocan carpetas distintas; cada tarea declara qué carpetas toca.
- Los informes deben ser honestos: pega la salida real de los comandos de verificación; si algo no se pudo probar, dilo.

## Reglas de código
- Fases pequeñas y verticales (de la interfaz al dato guardado); no avanzar de fase sin revisar la anterior.
- Tests para toda la lógica en Rust (normalización de duplicados, reconciliación offline).

## Memoria (servidor MCP `memory`)
Grafo de decisiones del proyecto. Solo el agente ingeniero escribe en él; los ejecutores pueden consultarlo. Al iniciar: `search_nodes` o `read_graph`. Guardar decisiones nuevas de arquitectura con `create_entities` / `add_observations`. No duplicar lo que ya está en `docs/`.
