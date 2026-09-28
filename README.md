# Lector de Libros

Lector y gestor de libros multiplataforma, open source y **100% offline**. Funciona bien
en hardware de gama baja, y trae biblioteca con colecciones y etiquetas, estadísticas
de lectura, notas, parte social y soporte serio de cómics (CBZ/CBR).

La arquitectura es *offline-first*: la base de datos **SQLite local es la fuente de
verdad** en cada dispositivo. El backend (Node.js/TypeScript + PostgreSQL) solo sirve
para cuentas y sincronización — nunca es un requisito para que la app funcione. En
iOS no hay app nativa por ahora: se cubre con la PWA instalable desde Safari.

## Stack por carpeta

| Carpeta | Qué contiene | Stack |
| --- | --- | --- |
| [`app-flutter/`](app-flutter) | Shell nativo de la app (Android, Windows, macOS, Linux) | Flutter (Dart) |
| [`reader-engine/`](reader-engine) | Motor de lectura HTML/JS: `epub.js`, `pdf.js` y el lector de cómics | JavaScript / TypeScript |
| [`web-shell/`](web-shell) | PWA standalone | React o Svelte |
| [`core-rust/`](core-rust) | Lógica compartida delicada: normalización de duplicados, reconciliación offline, parseo de contenedores | Rust → nativo (vía `dart:ffi`) y WebAssembly |
| [`backend/`](backend) | API de cuentas y sincronización | Node.js / TypeScript + PostgreSQL |
| [`docs/`](docs) | Documentación del proyecto | Markdown |

## Estado actual

**Fase 0 — Fundaciones del repositorio.** El repositorio tiene su estructura, licencia
y documentación; **todavía no hay código de producto**. No hay nada que compilar ni
ejecutar todavía.

El plan de fases está en [`docs/guia_inicio_desarrollo.md`](docs/guia_inicio_desarrollo.md)
(Fase 0 a Fase 7) y el estado vivo en [`docs/PROGRESO.md`](docs/PROGRESO.md).

## Cómo clonar

```bash
git clone https://github.com/Alejandrocc24/Lector-biblioteca.git
cd Lector-biblioteca
```

Requisitos para las próximas fases (aún no instalados en el repo):

- **Flutter SDK** — para `app-flutter/`
- **Node.js + npm** — para `web-shell/` y `backend/`
- **Rust (cargo) + toolchain `wasm32`** — para `core-rust/`

## Documentación

- [`docs/funcionalidades_lector_libros.md`](docs/funcionalidades_lector_libros.md) — funcionalidades y decisiones de arquitectura
- [`docs/guia_inicio_desarrollo.md`](docs/guia_inicio_desarrollo.md) — orden de fases de construcción
- [`docs/PROGRESO.md`](docs/PROGRESO.md) — estado actual del proyecto
- [`AGENTS.md`](AGENTS.md) — contexto del proyecto y protocolo de trabajo
- [`CONTRIBUTING.md`](CONTRIBUTING.md) — cómo contribuir

## Licencia

[AGPL-3.0](LICENSE) — GNU Affero General Public License v3.0. El texto completo está en
[`LICENSE`](LICENSE).
