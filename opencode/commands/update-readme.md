---
description: Analyze the project and update or create README.md
---

Analyze the current state of the project to update the README.md. Do not base this on the conversation — read the actual project.

Steps in order:
1. Explore the full project structure (all folders, files, entry points, configuration files, stack)
2. Read the current README.md if it exists
3. Update or create the README.md with the sections below. Do not remove sections that are still valid; only update or add what is missing or outdated. Include a section only if there is enough information in the project to populate it meaningfully.

**Required sections (always include all of them):**
- Project name and short description — what it does
- Project goal or scope (if not obvious from the description)
- Stack / technologies used
- Prerequisites
- How to install and run the project locally
- Environment variables needed (names only, no values)
- Folder structure — especially if it has well-defined layers or is a monorepo
- Main endpoints or key features
- Basic usage examples
- How to run tests (only if tests exist in the project)
- Available scripts (dev, build, test, lint, etc.)
- Architecture or relevant technical decisions
- Deployment flow (Docker, CI/CD, Kubernetes, VPS, etc.)
- Contribution guide
- Roadmap or future features
- Troubleshooting / common issues
- License

4. Run `git add README.md`
5. Generate the commit message following strict conventional commits: type(scope): description
6. Run `git commit -m "type(scope): description"`

The commit message must follow this format:
type(scope): description in English

- Acción en español
- Acción en español
- Acción en español

Rules:
- Commit message always in English, strict conventional commits
- Bullets always in Spanish
- Only commit README.md, nothing else
- Works even if the project has no commits yet
- Do not ask for confirmation, execute all steps
