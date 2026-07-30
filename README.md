# AI Support

Configuraciones y comandos personalizados para asistentes de IA (Claude Code y OpenCode) usados en proyectos de desarrollo.

## Propósito

Centralizar y versionar los comandos personalizados y configuraciones usados entre proyectos, para que cada sesión del asistente tenga las mismas herramientas de productividad sin importar el proyecto. Evita copiar las mismas instrucciones manualmente y mantiene al equipo alineado en un flujo de trabajo compartido.

## Stack / tecnologías

- **Markdown** — Comandos definidos como archivos `.md` con instrucciones en lenguaje natural
- **JSON** — Archivos de configuración (`settings.json`, `opencode.jsonc`)
- **Claude Code CLI** — Asistente de IA de Anthropic
- **OpenCode CLI** — Asistente de IA
- **PowerShell / Bash** — Scripts de instalación multiplataforma

## Estructura

```
ai-support/
├── [claude/](claude/README.md)          # Configuración para Claude Code
│   ├── settings.json
│   └── commands/    # Comandos personalizados para Claude
└── [opencode/](opencode/README.md)      # Configuración para OpenCode
    ├── opencode.jsonc
    └── commands/    # Comandos personalizados para OpenCode
```

## Instalación global

Cada subdirectorio tiene su propio README con instrucciones de instalación. En general, los comandos se instalan copiando o enlazando los archivos `.md` al directorio de comandos del asistente correspondiente.

## Licencia

No especificada. Consultar en el [repositorio](https://github.com/dejeloper/ai-support).
