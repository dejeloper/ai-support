This command accepts an optional flag:

- `--commit` → update `planning.md` and create a git commit.
- No flag → only update `planning.md`.

Determine whether the `--commit` flag was provided before executing the final step.

Check the project for a file called `planning.md` in the root directory.

If it does not exist:

- Explore the project to understand its name, description, and structure.
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

## Actualizado

- YYYY-MM-DD HH:mm

If the `--commit` flag was provided:

- Run `git add planning.md`
- Run `git commit -m "chore(planning): initialize planning.md"`

Stop. Do not continue.

---

If `planning.md` already exists, execute the following steps.

## Step 1 — Mark implemented tasks

- Read `planning.md` and explore the entire project.
- For every unchecked task (`- [ ]`) under `## Plan`, determine whether it has already been implemented.
- If implemented, change it to `- [x]`.
- Do not modify the task text.
- Do not remove, rewrite, or reorder existing tasks.

## Step 2 — Process new tasks

- Read every item under `## Nuevas tareas`.
- Determine the appropriate module and submodule for each task.
- Convert each item into a checkbox (`- [ ] Task`) and insert it into the correct location under `## Plan`.
- If the required module or submodule does not exist, create it using the existing heading structure.
- After processing all tasks, leave `## Nuevas tareas` containing only:

- Use this format to add new tasks

## Step 3 — Update timestamp

Update the `## Actualizado` section with the current date and time.

## Step 4 — Optional commit

Only execute this step if the `--commit` flag was provided.

- Run `git add planning.md`.
- Generate a Conventional Commit message using the format:

type(scope): description

where:

- `type(scope): description` must be written in English.
- The optional commit body must be written in Spanish.

Example:

feat(planning): update project planning

- Marca tareas implementadas
- Procesa nuevas tareas

Run:

git commit -m "type(scope): description"

Rules:

- Only modify checkbox states, process new tasks, and update the timestamp.
- Do not rewrite existing task descriptions.
- Do not reorder existing tasks.
- `## Nuevas tareas` must always appear before `## Actualizado`.
- `## Actualizado` must always be the last section.
- Only stage and commit `planning.md`.
- Do not ask for confirmation.
