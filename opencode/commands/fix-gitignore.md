---
description: Fix git cache so current .gitignore rules apply to all tracked files
---

Fix the git cache so the current .gitignore rules are properly applied to all tracked files.

Steps in order:
1. Check if `.gitignore` exists in the root directory. If it does not exist, stop and respond: "No se encontró un archivo .gitignore. Créalo antes de continuar."
2. Run `git rm -r --cached .` to remove all files from the git cache
3. Run `git add .` to re-add only the files allowed by .gitignore
4. Run `git commit -m "chore(git): fix gitignore cache and re-track files"`

Rules:
- Do not modify .gitignore or any project file
- Do not ask for confirmation, execute all steps
