---
description: Create or update planning.md — mark implemented tasks and process new ones
---

Check the project for a file called `planning.md` in the root directory.

If it does not exist:

- Explore the project to understand its name, description, and structure
- Create `planning.md` with this exact format:

# Project Name

Project description (if available)

## Plan

### Module Name

#### Submodule Name

- [ ] Task 1
- [ ] Task 2

## Nuevas tareas

- Use this format to add new tasks

- Run `git add planning.md` and `git commit -m "chore(planning): initialize planning.md"`
- Stop, do not continue

If it exists, execute all of the following steps:

**Step 1 — Mark implemented tasks:**

- Read `planning.md` and explore the full project code
- For each unchecked item `- [ ]` under `## Plan`, determine if it is already implemented
- If implemented, change `- [ ]` to `- [x]` — do not change the text, do not remove or add items

**Step 2 — Process new tasks from `## Nuevas tareas`:**

- Read each `- <task>` item listed under `## Nuevas tareas`
- For each item, analyze the task and determine which module and submodule it belongs to within `## Plan`
- Convert it to `- [ ] Task` and insert it in the correct module/submodule section
- If the module or submodule does not exist yet, create it following the same heading format (### Module / #### Submodule)
- After moving all items, leave `## Nuevas tareas` empty with only the placeholder line: `- Use this format to add new tasks`

**Step 3 — Commit:**

- Run `git add planning.md`
- Generate a commit message following strict conventional commits: type(scope): description
- Run `git commit -m "type(scope): description"`

The commit message must follow this format:
type(scope): description in English

- Acción en español
- Acción en español

Rules:

- Only modify checkbox state and process new tasks — do not rewrite or reorder existing items
- `## Nuevas tareas` is always present at the bottom of the file, before `## Actualizado`
- `## Actualizado` is always the last section of the file
- Only commit planning.md, nothing else
- Do not ask for confirmation, execute all steps
