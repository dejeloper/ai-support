# Comandos personalizados para Claude Code

Comandos slash (`/`) para usar con [Claude Code](https://docs.anthropic.com/en/docs/claude-code).

## Listado

| Comando | Descripción |
|---------|-------------|
| `/commit-this` | Genera un mensaje de commit convencional en inglés con bullets en español para los cambios de la sesión actual |
| `/fix-gitignore` | Limpia la cache de git para que las reglas actuales de `.gitignore` se apliquen correctamente |
| `/pre-commit` | Revisa los cambios staged y sugiere mensajes de commit agrupados por scope |
| `/pre-pr` | Genera el título, descripción y recursos visuales sugeridos para un PR a partir del diff con `origin/main` |
| `/update-plan` | Crea o actualiza `planning.md` marcando tareas implementadas y moviendo nuevas tareas a su lugar |
| `/update-readme` | Analiza el proyecto y actualiza `README.md` con todas las secciones requeridas |

## Instalación global

Ver instrucciones en el [README principal](../README.md) de la carpeta `claude/`.

## Formato de comandos

Cada comando es un archivo Markdown que contiene las instrucciones que el asistente debe seguir al ser invocado. El formato varía según el asistente:

- **Claude Code:** Archivo `.md` plano con instrucciones en lenguaje natural.

Para más información sobre comandos personalizados, consulta la [documentación de Claude Code](https://docs.anthropic.com/en/docs/claude-code/overview#custom-slash-commands).
