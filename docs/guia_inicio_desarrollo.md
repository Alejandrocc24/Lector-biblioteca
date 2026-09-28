# Guía de inicio: cómo empezar a programar este proyecto

Este documento responde a la pregunta práctica: *"¿qué haría realmente un ingeniero de software para arrancar esto?"* — no es la lista de funcionalidades (ver `funcionalidades_lector_libros.md`), sino el orden de trabajo, la estructura del proyecto, y cómo encaja tu plan de usar un asistente de IA (OpenCode + modelos gratuitos) hasta llegar a un MVP funcional antes de subirlo a GitHub.

---

## 1. Principio general: no se programa "todo a la vez"

Un error común al arrancar un proyecto de este tamaño es intentar construir todas las piezas en paralelo. Un ingeniero de software real trabaja por **capas verticales delgadas**: una porción mínima que atraviese todo el sistema (de la interfaz al dato guardado) y funcione de punta a punta, antes de ampliarla. Esto aplica también trabajando con IA: es mucho más fácil para un asistente (y para ti revisando su trabajo) generar código correcto sobre una base pequeña y probada, que sobre un esqueleto vacío con 40 funcionalidades a medio definir.

---

## 2. Orden real de construcción (fases)

### Fase 0 — Fundaciones del repositorio (antes de escribir una sola función)

Esto no es "código de producto", es la base que hace que todo lo demás sea sostenible, especialmente importante porque el proyecto nacerá open source:

- Estructura de carpetas del repositorio (monorepo vs. repos separados — ver sección 4)
- Configuración de linter/formateador desde el día uno (evita que el código generado por IA en distintas sesiones tenga estilos inconsistentes)
- `README.md` inicial: qué es el proyecto, cómo se levanta en local, qué falta
- Archivo `LICENSE` con el texto completo de AGPL-3.0
- `CONTRIBUTING.md` básico (aunque esté vacío al inicio, se llena antes de publicar en GitHub)
- Definición de convención de commits (ej. Conventional Commits: `feat:`, `fix:`, `docs:`) — esto importa mucho cuando luego lleguen colaboradores externos

### Fase 1 — El núcleo de datos, sin interfaz todavía

Antes de tocar Flutter o React, se define y construye:

- El esquema de la base de datos **SQLite local** (tablas: libros, metadatos, progreso, notas, colecciones, etiquetas)
- El esquema de **PostgreSQL** del backend (usuarios, sincronización, clubes de lectura)
- La lógica en **Rust** para lo que ya definimos como compartido: normalización de duplicados, parseo de contenedor EPUB/CBZ

**Por qué primero:** todo lo demás depende de que esta estructura exista y esté bien pensada. Cambiar el esquema de datos después de tener interfaz construida encima es mucho más costoso que definirlo bien una vez.

### Fase 2 — Un solo formato, de punta a punta

Se elige **un solo formato** (recomendación: EPUB, por ser el más simple y con la librería más madura) y se construye el camino completo:
1. Importar un archivo EPUB de prueba
2. Extraer metadatos y portada
3. Guardarlo en SQLite local
4. Mostrarlo en una lista mínima (sin diseño pulido todavía)
5. Abrirlo y leerlo con `epub.js` embebido
6. Guardar el progreso de lectura al cerrar

Esto es, literalmente, el primer MVP interno — no se le muestra a nadie todavía, pero prueba que la arquitectura elegida (Flutter + WebView + SQLite) funciona en la práctica antes de construir 20 funcionalidades sobre una base no probada.

### Fase 3 — Ampliar formatos

Con el camino de EPUB funcionando, se replica el patrón para:
- PDF (con `pdf.js`)
- CBZ/CBR (con el componente de lectura de cómics aparte, como ya definimos)
- TXT y MOBI/AZW3

### Fase 4 — Biblioteca y organización

Colecciones, etiquetas, búsqueda, columnas personalizadas, fusión de duplicados — todo lo que ya está en la sección 1 del documento de funcionalidades.

### Fase 5 — Backend y sincronización

Este es un punto de decisión importante: **el backend se construye después de que el cliente ya funciona 100% offline**, no en paralelo. Razón: si el proyecto es offline-first de verdad, el backend nunca debe ser un bloqueante para que la app funcione, así que probarlo así desde el inicio (app funcionando sin backend) valida que la arquitectura offline-first es real y no solo una intención.

Una vez ahí: cuentas, sincronización entre dispositivos, conexión con nube externa (Drive/Dropbox).

### Fase 6 — Estadísticas, notas, social

Estas capas dependen de tener datos de uso reales fluyendo (progreso, tiempo de lectura), así que van después de que el core de lectura y sincronización estén sólidos.

### Fase 7 — Sistema de plugins

Deliberadamente al final del MVP, aunque el "gancho" de eventos internos (mencionado en el documento de funcionalidades, sección 9.2) sí se diseña desde la Fase 1, para no tener que reestructurar después.

---

## 3. Cómo encaja trabajar con un asistente de IA (OpenCode + modelos gratuitos) en este flujo

Trabajar con un asistente de código funciona mejor cuando cada tarea que le das es del tamaño de **una fase pequeña, no del proyecto completo**. Recomendaciones concretas para tu flujo:

- **Una sesión = una porción vertical delgada.** Pide "implementa el flujo de importar y leer un EPUB con SQLite local" en vez de "constrúyeme el lector completo". Los asistentes de código (incluidos los modelos gratuitos, que suelen tener menos capacidad de mantener contexto largo) producen resultados mucho más confiables en tareas acotadas.
- **Mantén los documentos de este chat (`funcionalidades_lector_libros.md` y esta guía) como referencia que le pegas al asistente al inicio de cada sesión nueva.** Esto le da el contexto de arquitectura sin que tengas que re-explicar las decisiones cada vez.
- **Revisa el código generado antes de avanzar a la siguiente fase**, no acumules fases sin revisar — con modelos gratuitos (generalmente menos capaces que los de pago) es más probable que aparezcan errores sutiles, y es mucho más barato corregir un error en la Fase 2 que descubrirlo en la Fase 6 construido encima.
- **Pide tests automatizados desde la Fase 1**, especialmente para la lógica en Rust (normalización, reconciliación) — es la pieza más delicada y la que un asistente de IA puede modificar sin darse cuenta de que rompe algo si no hay tests que lo detecten.
- **Los prompts largos y específicos rinden mejor que los cortos y abiertos.** Dale al asistente el esquema exacto de tablas, el formato de datos esperado, y un ejemplo concreto de entrada/salida cuando le pidas implementar algo — reduce la ambigüedad que hace que un modelo gratuito "invente" una solución distinta a la que planeaste.

---

## 4. Estructura de repositorio sugerida

Dado que hay múltiples piezas (Flutter, motor web de lectura, shell web, Rust, backend), un **monorepo** (todo en un solo repositorio, en carpetas separadas) es más práctico que repos separados para este tamaño de equipo al inicio — facilita que un colaborador nuevo clone un solo lugar y vea todo el proyecto, y evita el problema de coordinar versiones entre varios repos siendo un equipo pequeño.

```
/lector-libros
├── /app-flutter          → shell nativo (Android, Windows, macOS, Linux)
├── /reader-engine         → motor de lectura HTML/JS (epub.js, pdf.js, lector de cómics)
├── /web-shell             → PWA standalone (React/Svelte)
├── /core-rust             → lógica compartida (normalización, reconciliación, parseo)
├── /backend               → API (Node.js/TS + PostgreSQL)
├── /docs                  → documentación del proyecto (incluye estos .md)
├── LICENSE                → AGPL-3.0
├── README.md
└── CONTRIBUTING.md
```

---

## 5. Qué significa "MVP funcional con todas las funciones" en la práctica

Antes de subir a GitHub para apoyo de la comunidad, conviene tener claro qué nivel de "completo" es razonable exigirle a un MVP, para no atrasar la publicación esperando perfección:

- **Debe funcionar de punta a punta**: importar, organizar, leer, anotar, sincronizar — sin errores que rompan el flujo básico
- **No necesita tener pulida cada funcionalidad secundaria** (catálogo exportable, comparador de ediciones, generador de portadas) — esas pueden quedar como *issues* abiertos en GitHub, que es justo el tipo de tarea ideal para que la comunidad empiece a contribuir
- **Sí necesita tener la arquitectura base sólida** (esquema de datos, offline-first funcionando, el gancho de plugins previsto) porque cambiar esto después de tener contribuidores externos es mucho más costoso políticamente (rompes código de otros) que técnicamente

---

## 6. Siguiente paso sugerido

Con esta guía y el documento de funcionalidades, el trabajo que sigue es empezar la Fase 0 (estructura de repositorio) y Fase 1 (esquema de datos) — que son la base literal sobre la que se apoya todo lo demás, y el punto de partida natural para tu primera sesión con el asistente de código.
