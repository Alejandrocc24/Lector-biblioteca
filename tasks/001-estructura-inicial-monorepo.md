# Tarea 001 — Estructura inicial del monorepo y archivos base

**Fase:** 0
**Carpetas que toca:** raíz del repo (`README.md`, `LICENSE`, `CONTRIBUTING.md`, `.gitignore`, `.editorconfig`, carpetas `app-flutter/`, `reader-engine/`, `web-shell/`, `core-rust/`, `backend/`)

## Objetivo
Crear la estructura base del monorepo y los archivos fundacionales para que cualquier colaborador pueda clonar y entender el proyecto, sin escribir aún código de producto.

## Contexto
- Leer antes de empezar: `AGENTS.md`, `docs/guia_inicio_desarrollo.md` (sección 4, estructura sugerida) y `docs/PROGRESO.md`.
- El repo está vacío (solo `docs/`, `tasks/`, `reports/`, `AGENTS.md`, `opencode.json`). Verificar con `git status` y `ls -la`.

## Pasos
1. Crear las carpetas del monorepo según `docs/guia_inicio_desarrollo.md` §4: `app-flutter/`, `reader-engine/`, `web-shell/`, `core-rust/`, `backend/`. Añadir un `.gitkeep` en cada una para que Git las conserve.
2. Crear `README.md` en la raíz: qué es el proyecto (1-2 párrafos desde `AGENTS.md`), stack por carpeta, estado actual (Fase 0), cómo clonar, enlace a `docs/` y licencia AGPL-3.0.
3. Crear archivo `LICENSE` con el texto completo de la AGPL-3.0 (descargar de https://www.gnu.org/licenses/agpl-3.0.txt, no resumir ni inventar).
4. Crear `CONTRIBUTING.md` básico: convención de commits Conventional Commits (`feat:`, `fix:`, `docs:`, `chore:`, `task NNN:` para tareas de ejecutor), flujo ingeniero/ejecutor en 5 líneas, requisito de linter/formato futuro.
5. Crear `.gitignore` raíz que cubra Flutter (`build/`, `.dart_tool/`), Node (`node_modules/`, `dist/`), Rust (`target/`, `Cargo.lock` solo si aplica a binarios — documentar decisión en el informe), Python si se usa para scripts, y `.DS_Store` / `*.log`.
6. Crear `.editorconfig` raíz: `utf-8`, `lf`, `final_newline=true`, `trim_trailing_whitespace=true`, `indent_style=space`, `indent_size=2` (excepto Rust 4 — dejar comentario).
7. Verificar con `ls -R` y `git status --short`.

## Criterios de aceptación (verificables)
- [ ] Existen `app-flutter/`, `reader-engine/`, `web-shell/`, `core-rust/`, `backend/` cada una con `.gitkeep`.
- [ ] Existe `README.md` con secciones: qué es, stack, estado, cómo clonar, docs y licencia.
- [ ] Existe `LICENSE` con el texto completo AGPL-3.0 (contiene la cadena `GNU AFFERO GENERAL PUBLIC LICENSE` y `Version 3`).
- [ ] Existen `CONTRIBUTING.md`, `.gitignore` y `.editorconfig` con el contenido descrito.
- [ ] `git status --short` muestra solo los archivos nuevos esperados, sin basura (sin `node_modules`, `target/`, etc.).
- [ ] Informe escrito en `reports/001-estructura-inicial-monorepo.md` según `reports/_PLANTILLA.md`, con salida real pegada de `ls -R` y `git status --short`.

## Fuera de alcance
- Configurar linters/formateadores (tarea 002).
- Inicializar proyectos Flutter, Cargo, npm o cualquier código fuente.
- Modificar `docs/`, `tasks/` o `AGENTS.md`.
