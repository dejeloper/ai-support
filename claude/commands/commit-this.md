Based on what you just implemented in this conversation:

If you have not made any changes in this session, respond only with: "No he hecho nada en esta sesión, no hay nada para commitear."

If you did make changes, execute the following steps in order:

1. Run `git reset HEAD .` to clear the current staging area
2. Run `git add` for each file you modified or created in this session
3. Generate the commit message with this format:

type(scope): description in English following conventional commits

- Acción en español
- Acción en español
- Acción en español

Rules:
- Commit message always in English, strict conventional commits: type(scope): description
- Bullets always in Spanish
- Do not assume multiple scopes, everything goes under the same scope
- Do not commit, only generate the text
- Do not add explanations outside the defined format
