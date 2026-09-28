# Cómo contribuir

Gracias por querer colaborar. Este proyecto es open source bajo **AGPL-3.0** y toda
contribución se publica bajo la misma licencia.

## Convención de commits

Usamos [Conventional Commits](https://www.conventionalcommits.org/es/v1.0.0/):

- `feat:` — funcionalidad nueva
- `fix:` — corrección de un error
- `docs:` — solo documentación
- `chore:` — mantenimiento que no cambia comportamiento (config, scripts)
- `test:` — solo tests
- `refactor:` — cambio de estructura sin cambiar comportamiento

Prefiere siempre un alcance: `feat(biblioteca): agregar filtro por etiqueta`.

### Excepción del flujo con asistentes de IA

En este proyecto el trabajo se hace con dos tipos de sesión (ver `AGENTS.md`), y las
tareas las implementa un agente "ejecutor". Para esos commits el prefijo es
`task NNN:`, donde `NNN` es el número de la tarea en `tasks/`:

```
task 001: estructura inicial del monorepo
task 002: configurar linters y formateadores
```

Si el commit resuelve más de una tarea: `task 001-002: estructura inicial y linters`.

## Flujo ingeniero/ejecutor (en 5 líneas)

1. El ingeniero escribe una tarea en `tasks/NNN-titulo.md` (plantilla en `tasks/_PLANTILLA.md`).
2. El ejecutor lee solo esa tarea, la implementa sin ampliar alcance y escribe su informe en `reports/NNN-titulo.md` (plantilla en `reports/_PLANTILLA.md`).
3. El ejecutor hace commit con el mensaje `task NNN: titulo` e incluye en el informe la salida real de los comandos de verificación.
4. El ingeniero revisa el informe y el diff real (`git log`, `git show`), y actualiza `docs/PROGRESO.md`.
5. El ingeniero define la siguiente tarea. Las fases no se saltan y las tareas en paralelo solo se dan si tocan carpetas distintas.

## Linter y formato

Aún no hay linter ni formateador configurados (eso llega en la tarea 002). Cuando se
configuren, formatea el código antes de commitear y no mezcles reformateo masivo con
cambios funcionales en el mismo commit.

## Alcance de una contribución

- Una contribución = una tarea, no un "¿me haces la app entera?".
- No incluyas archivos generados: `build/`, `node_modules/`, `target/`, `dist/` (ver `.gitignore`).
- Las decisiones de arquitectura se documentan en `docs/`, no solo en el código.
