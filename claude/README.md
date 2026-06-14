# Claude — Configuración para Claude Code

Configuración global y comandos personalizados para [Claude Code](https://docs.anthropic.com/en/docs/claude-code).

## Archivos

- `settings.json` — Configuración global del cliente Claude Code (modelo, tema, etc.)
- `commands/` — Comandos personalizados de proyecto

## Instalación global de comandos

Los comandos en `commands/` se instalan a nivel global para que estén disponibles en cualquier proyecto.

Primero clona el repo y navega a él:

```bash
git clone <repo-url>
cd ai-support
```

### Windows (PowerShell)

```powershell
# Copiar todos los comandos al directorio global de Claude Code
Copy-Item -Path ".\claude\commands\*" -Destination "$env:USERPROFILE\.claude\commands\" -Recurse -Force
```

### macOS / Linux

```bash
cp claude/commands/* ~/.claude/commands/
```

### Uso

Una vez instalados, los comandos están disponibles escribiendo `/` en el chat de Claude Code:

- `/commit-this`
- `/fix-gitignore`
- `/pre-commit`
- `/pre-pr`
- `/update-plan`
- `/update-readme`

## Instalación de settings.json

Copia `settings.json` a `~/.claude/settings.json` (global) o al `settings.json` del proyecto.
