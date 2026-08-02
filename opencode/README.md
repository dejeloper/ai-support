# OpenCode — Configuración para OpenCode

Configuración global y comandos personalizados para [OpenCode](https://opencode.ai).

## Archivos

- `opencode.jsonc` — Configuración del proyecto para OpenCode
- `commands/` — Comandos slash personalizados

## Instalación

```bash
git clone https://github.com/dejeloper/ai-support.git
cd ai-support
```

### Windows (PowerShell)

```powershell
Copy-Item -Path ".\opencode\commands\*" -Destination "$env:USERPROFILE\.config\opencode\commands\" -Recurse -Force
```

### macOS / Linux

```bash
cp -r opencode/commands/* ~/.config/opencode/commands/
```

Para instalación local (solo el proyecto actual), copia a `.opencode/commands/`.

Coloca `opencode.jsonc` en la raíz del proyecto o en `~/.config/opencode/config.jsonc` para uso global.

## Comandos

| Comando | Descripción |
|---------|-------------|
| `/commit-all` | Agrupa cambios en commits semánticos con validación y control de push |
| `/commit-this` | Genera un mensaje de commit convencional en inglés con bullets en español para los cambios de la sesión actual |
| `/fix-gitignore` | Limpia la caché de git para que las reglas actuales de `.gitignore` se apliquen correctamente |
| `/pre-commit` | Revisa los cambios staged y sugiere mensajes de commit agrupados por scope |
| `/pre-pr` | Genera título, descripción y recursos visuales sugeridos para un PR a partir del diff con `origin/main` |
| `/update-plan` | Crea o actualiza `planning.md` marcando tareas implementadas. Soporta `--commit` para hacer commit automático |
| `/update-readme` | Analiza el proyecto y actualiza `README.md` con todas las secciones requeridas |
| `/use-council` | Convoca un consejo local de 4 roles (Seguridad, Rendimiento, Mantenibilidad, Abogado del Diablo) para analizar una pregunta sobre el código del proyecto, con opción `--impl` para implementar las recomendaciones una a una |
