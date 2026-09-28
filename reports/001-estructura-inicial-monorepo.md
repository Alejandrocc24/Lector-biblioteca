# Informe 001 — Estructura inicial del monorepo y archivos base

**Estado:** completada

## Qué se hizo

Creada la estructura de carpetas del monorepo definida en `docs/guia_inicio_desarrollo.md` §4
y los cinco archivos fundacionales de la raíz. **No se escribió ningún código de producto**
(ni `flutter create`, ni `cargo init`, ni `npm init`), tal como pedía la tarea.

1. **Carpetas del monorepo** con `.gitkeep` cada una: `app-flutter/`, `reader-engine/`,
   `web-shell/`, `core-rust/`, `backend/`.
2. **`README.md`** con las secciones pedidas: qué es el proyecto (2 párrafos desde `AGENTS.md`),
   stack por carpeta (tabla), estado actual (Fase 0, sin código todavía), cómo clonar
   (usando el remoto real `https://github.com/Alejandrocc24/Lector-biblioteca.git`) y
   requisitos de las próximas fases, enlaces a `docs/` y licencia AGPL-3.0.
3. **`LICENSE`** con el texto completo de la AGPL-3.0 (235 líneas, 34 020 bytes).
4. **`CONTRIBUTING.md`** con la convención de commits Conventional Commits (`feat:`, `fix:`,
   `docs:`, `chore:`, `test:`, `refactor:`), la excepción `task NNN:` para el flujo
   ingeniero/ejecutor resumida en 5 líneas, y el requisito de linter/formato (pendiente,
   tarea 002).
5. **`.gitignore`** raíz cubriendo Flutter/Dart, Node/TS, Rust, Python, SO, editores y logs,
   con la decisión sobre `Cargo.lock` documentada dentro del propio archivo.
6. **`.editorconfig`** raíz con `utf-8`, `lf`, `insert_final_newline`, `trim_trailing_whitespace`,
   `indent_style=space`, `indent_size=2` y override `[*.rs] indent_size = 4` (con comentario).

## Archivos creados o modificados

Creados y commiteados en `de5a35e task 001: estructura inicial del monorepo`:

| Archivo | Líneas | Notas |
| --- | --- | --- |
| `README.md` | 56 | nuevo |
| `LICENSE` | 235 | nuevo — texto íntegro AGPL-3.0 |
| `CONTRIBUTING.md` | 50 | nuevo |
| `.gitignore` | 65 | nuevo |
| `.editorconfig` | 23 | nuevo |

Creados **fuera** de mi commit (ver "Problemas" abajo): los cinco `.gitkeep`.
`git show --stat HEAD`:

```
 .editorconfig   |  23 ++++++
 .gitignore      |  65 ++++++++++++++++
 CONTRIBUTING.md |  50 ++++++++++++++++
 LICENSE         | 235 +++++++++++++++++++++++++++++++++++++++++++++++++++++++
 README.md       |  56 ++++++
 5 files changed, 429 insertions(+)
```

## Verificación

### 1. Las cinco carpetas existen con su `.gitkeep` y Git las conserva

`ls -Ra app-flutter reader-engine web-shell core-rust backend`:

```
app-flutter:
.
..
.gitkeep

backend:
.
..
.gitkeep

core-rust:
.
..
.gitkeep

reader-engine:
.
..
.gitkeep

web-shell:
.
..
.gitkeep
```

`git ls-files | grep gitkeep` (confirma que están **rastreadas**, no solo en disco):

```
app-flutter/.gitkeep
backend/.gitkeep
core-rust/.gitkeep
reader-engine/.gitkeep
web-shell/.gitkeep
```

### 2. `ls -R` del repo

```
$ ls -R -I .git -I .opencode .
.:
AGENTS.md
app-flutter
backend
CONTRIBUTING.md
core-rust
docs
LICENSE
opencode.json
reader-engine
README.md
reports
tasks
web-shell

./app-flutter:

./backend:

./core-rust:

./docs:
funcionalidades_lector_libros.md
guia_inicio_desarrollo.md
PROGRESO.md

./reader-engine:

./reports:
_PLANTILLA.md

./tasks:
001-estructura-inicial-monorepo.md
_PLANTILLA.md

./web-shell:
```

### 3. `git status --short` — limpio, sin basura

Antes de commitear, en el working tree solo estaban mis 5 archivos nuevos
(`docs/`, `tasks/`, `reports/` y `AGENTS.md` no se tocaron). Después del commit:

```
$ git status --short
(vacio = nada sin rastrear)
```

No hay basura: no aparece `node_modules/`, `target/`, `build/` ni `dist/`, y las reglas de
`.gitignore` se comprobaron de verdad con `git check-ignore -v`:

```
$ for p in app-flutter/build/x.o app-flutter/.dart_tool/x.json web-shell/node_modules/a.js \
           backend/dist/a.js core-rust/target/debug/x backend/.pytest_cache/x.py \
           .DS_Store app.log foo.swp .vscode/settings.json; do
    printf '%-38s -> ' "$p"; git check-ignore -v "$p" || echo "NO IGNORADO"; done

app-flutter/build/x.o                  -> .gitignore:28:build/	app-flutter/build/x.o
app-flutter/.dart_tool/x.json          -> .gitignore:24:.dart_tool/	app-flutter/.dart_tool/x.json
web-shell/node_modules/a.js            -> .gitignore:34:node_modules/	web-shell/node_modules/a.js
backend/dist/a.js                      -> .gitignore:35:dist/	backend/dist/a.js
core-rust/target/debug/x               -> .gitignore:44:target/	core-rust/target/debug/x
backend/.pytest_cache/x.py             -> .gitignore:59:.pytest_cache/	backend/.pytest_cache/x.py
.DS_Store                              -> .gitignore:4:.DS_Store	.DS_Store
app.log                                -> .gitignore:16:*.log	app.log
foo.swp                                -> .gitignore:7:*.swp	foo.swp
.vscode/settings.json                  -> .gitignore:11:.vscode/	.vscode/settings.json
```

### 4. `LICENSE` es el texto íntegro de la AGPL-3.0

```
$ wc -lc LICENSE
 235 34020 LICENSE

$ for s in "GNU AFFERO GENERAL PUBLIC LICENSE" "Version 3, 19 November 2007" \
           "TERMS AND CONDITIONS" "17. Interpretation of Sections 15 and 16" \
           "How to Apply These Terms to Your New Programs" \
           "13. Remote Network Interaction"; do
    printf '%-46s -> %s ocurrencia(s)\n' "$s" "$(grep -c "$s" LICENSE)"; done
GNU AFFERO GENERAL PUBLIC LICENSE              -> 1 ocurrencia(s)
Version 3, 19 November 2007                    -> 1 ocurrencia(s)
TERMS AND CONDITIONS                           -> 2 ocurrencia(s)
17. Interpretation of Sections 15 and 16       -> 1 ocurrencia(s)
How to Apply These Terms to Your New Programs -> 1 ocurrencia(s)
13. Remote Network Interaction                 -> 1 ocurrencia(s)

$ sha256sum LICENSE
d8a6cc31abc16b6748c7a21f21611f5a1ec33f67d22ca23d7da1c19b95496bee
```

Está completo: Preamble, TERMS AND CONDITIONS, secciones 0–17, "END OF TERMS AND CONDITIONS"
(línea 214) y el apéndice "How to Apply These Terms to Your New Programs".

### 5. `.editorconfig`

```
# Configuración base de todos los editores del monorepo.
# Ver https://editorconfig.org
root = true

[*]
charset = utf-8
end_of_line = lf
insert_final_newline = true
trim_trailing_whitespace = true
indent_style = space
indent_size = 2

# Rust usa 4 espacios (convención de cargo fmt / rustfmt).
[*.rs]
indent_size = 4

# Markdown: los trailing spaces son saltos de línea intencionales.
[*.md]
trim_trailing_whitespace = false

# El texto de la licencia (LICENSE) se copia literal de la FSF: no reformatear.
[LICENSE]
trim_trailing_whitespace = false
```

## Problemas, dudas o decisiones que tomé

### ⚠️ `gnu.org` es inalcanzable desde esta máquina (resuelto, pero conviene que lo sepas)

`curl https://www.gnu.org/licenses/agpl-3.0.txt` da **timeout** (conexión bloqueada; otros
sitios como `gutenberg.org` y `raw.githubusercontent.com` sí responden). `webfetch` también
da timeout. Así que **no pude descargar el archivo directamente de gnu.org** como pedía el paso 3.

Lo resolví con una copia textual canónica igualmente literal, contrastada por dos vías:

- `https://raw.githubusercontent.com/spdx/license-list-data/main/text/AGPL-3.0-only.txt`
  (34 020 bytes, sha256 `d8a6cc31…96bee`) — copia literal del `agpl-3.0.txt` de gnu.org,
  con el encabezado plano tal cual lo publica la FSF
  (`GNU AFFERO GENERAL PUBLIC LICENSE` / `Version 3, 19 November 2007` / `<http://fsf.org/>`).
- Contrastado contra la copia de Nextcloud (`COPYING`, 34 520 bytes) y el `AGPL-3.0-or-later`
  del propio SPDX. La diferencia con la de Nextcloud/Mastodon es **solo el formato** (encabezado
  centrado y párrafos con wrap duro a ~70 columnas); el texto es el mismo. El
  `AGPL-3.0-or-later` de SPDX es **byte a byte idéntico** al que puse.

**Recomendación para el ingeniero:** cuando haya red que llegue a gnu.org, confirma con
`curl -o /dev/null -w '%{size_download}' https://www.gnu.org/licenses/agpl-3.0.txt` que da
34 020 bytes. Si da otro número, hay que revisar el `LICENSE`.

### Decisión: `Cargo.lock` **sí** se versiona (no está en `.gitignore`)

La tarea lo dejaba abierto ("solo si aplica a binarios — documentar decisión"). Elegí
**versionarlo**, porque:
- El proyecto construye un **producto final** (una app), no una librería para crates.io, y la
  guía oficial de Rust recomienda commitear el lock en ese caso.
- El proyecto apunta explícitamente a hardware de gama baja: fijar versiones hace que
  "funciona en mi máquina" sea reproducible para quien compile en un equipo modesto.
- `core-rust/` se compila a nativo **y** a WASM; Reproducibility en ambos casos es valiosa.

La decisión está escrita como comentario dentro de `.gitignore`, con la instrucción de
invertirla si algún crate llega a publicarse como librería. Mismo criterio apliqué a
`pubspec.lock` (tampoco se ignora).

### Nota de concurrencia: los `.gitkeep` quedaron en el commit del ingeniero

Al empezar, `git status --short` mostraba `?? tasks/001-…md`, `?? .opencode/memory.jsonl` y
` M docs/PROGRESO.md`. Yo creé los `.gitkeep` a las 00:28; a las 00:29:32 otra sesión
(sesión ingeniero, en paralelo) hizo `commit 041daa2 "docs: tarea 001 y progreso"` y se llevó
por delante mis cinco `.gitkeep` con un `git add -A`. Por eso **no aparecen en mi commit**,
aunque sí están en el repo y rastreados por Git (verificado arriba con `git ls-files`).

Mi commit `de5a35e` contiene **solo** los 5 archivos de la raíz, ninguno de `docs/`, `tasks/`
ni `AGENTS.md`. No edité esos archivos.

### Cosas que vi y **no** toqué (fuera de alcance)

1. **`docs/PROGRESO.md` tiene dos secciones `## Decisiones importantes` duplicadas**
   (líneas 12 y 16). La segunda dice "(ninguna todavía)" y contradice a la primera. Es archivo
   del ingeniero; lo anoto para que lo arregle al actualizar el progreso.
2. **Falta `.env` en `.gitignore`.** Lo mencioné como nota dentro del propio `.gitignore` para
   la tarea 002, pero no lo añadí porque la tarea no lo pedía. Debería agregarse antes de que
   exista el backend de Node.
3. **`.opencode/` está versionado** (incluye `memory.jsonl` con el grafo de decisiones).
   No sé si es intencional; si el `memory.jsonl` no debe salir al repo público, conviene
   decidirlo antes de publicar en GitHub.
4. **El `.gitignore` ignora `build/` sin anclar**, así que también afectaría a cualquier
   carpeta llamada `build` en el futuro (p. ej. si el backend usa un `build/` propio de TypeScript).
   Es el comportamiento deseado; lo dejo anotado por si molesta más adelante.
5. **No verifiqué nada de compilación** porque no hay código: no hay `flutter`, `cargo` ni `npm`
   que ejecutar. Ningún criterio de aceptación lo requería.
6. Amplié un peldaño el `.gitignore` (SO, editores, logs) más allá de la lista mínima de la
   tarea; es contenido estándar de un `.gitignore` fundacional, pero es una decisión mía.

## Sugerencia para el siguiente paso

Continuar con la **tarea 002** (configurar linters/formateadores: `rustfmt` + `clippy` con
`rustfmt.toml` en `core-rust/`, `analysis_options.yaml` en `app-flutter/`, ESLint+Prettier en
`web-shell/`/`backend/`) y de paso añadir `.env` a `.gitignore`. Eso cierra la Fase 0 tal como
la describe la guía §2 y deja el repo listo para la Fase 1 (esquema de datos SQLite +
PostgreSQL + tests de la lógica Rust).

Nota para el ingeniero: como `docs/PROGRESO.md` sigue diciendo "Fase 0 sin iniciar", conviene
actualizarlo junto con la limpieza del encabezado duplicado que mencioné arriba.
