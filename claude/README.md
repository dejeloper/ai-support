# Claude — Configuración para Claude Code

Configuración global y comandos personalizados para [Claude Code](https://docs.anthropic.com/en/docs/claude-code).

## Archivos

- `settings.json` — Configuración del cliente (modelo, tema, etc.)
- `commands/` — Comandos slash personalizados

## Instalación

```bash
git clone https://github.com/dejeloper/ai-support.git
cd ai-support
```

### Windows (PowerShell)

```powershell
Copy-Item -Path ".\claude\commands\*" -Destination "$env:USERPROFILE\.claude\commands\" -Recurse -Force
```

### macOS / Linux

```bash
cp claude/commands/* ~/.claude/commands/
```

Copia `settings.json` a `~/.claude/settings.json` para aplicar la configuración global.

## Comandos

| Comando | Descripción |
|---------|-------------|
| `/commit-this` | Genera un mensaje de commit convencional en inglés con bullets en español para los cambios de la sesión actual |
| `/fix-gitignore` | Limpia la caché de git para que las reglas actuales de `.gitignore` se apliquen correctamente |
| `/pre-commit` | Revisa los cambios staged y sugiere mensajes de commit agrupados por scope |
| `/pre-pr` | Genera título, descripción y recursos visuales sugeridos para un PR a partir del diff con `origin/main` |
| `/update-plan` | Crea o actualiza `planning.md` marcando tareas implementadas. Soporta `--commit` para hacer commit automático |
| `/update-readme` | Analiza el proyecto y actualiza `README.md` con todas las secciones requeridas |
