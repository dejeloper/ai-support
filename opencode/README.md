# OpenCode — Configuración para OpenCode

Configuración global y comandos personalizados para [OpenCode](https://opencode.ai).

## Archivos

- `opencode.jsonc` — Configuración del proyecto para OpenCode
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
# Copiar todos los comandos al directorio global de OpenCode
Copy-Item -Path ".\opencode\commands\*" -Destination "$env:USERPROFILE\.config\opencode\commands\" -Recurse -Force
```

Para instalarlos solo en el proyecto actual, copia los comandos a `.opencode/commands/` dentro del proyecto.

### macOS / Linux

```bash
cp -r opencode/commands/* ~/.config/opencode/commands/
```

Para el proyecto actual:

```bash
cp -r opencode/commands/* .opencode/commands/
```

### Uso

Una vez instalados, los comandos están disponibles escribiendo `/` en el chat de OpenCode:

- `/commit-all`
- `/commit-this`
- `/fix-gitignore`
- `/pre-commit`
- `/pre-pr`
- `/update-plan`
- `/update-readme`

## Configuración

El archivo `opencode.jsonc` se coloca en la raíz del proyecto para configurar OpenCode. Para uso global, colócalo en `~/.config/opencode/config.jsonc`.
