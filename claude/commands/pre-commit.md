Review the staged changes. Do not commit. Analyze the modified files and group them by scope (detected automatically by folder or module).

Rules:

1. If there is a single scope:
   - Provide the commit message in English following strict conventional commits: type(scope): description
   - List the changes as bullets in Spanish

2. If there are multiple scopes:
   - Show at the top: "⚠️ Warning: multiple scopes detected in Staged"
   - Show a global suggested message (in case everything is committed together)
   - Then break down each scope with its own commit message and bullets in Spanish

Output format for multiple scopes:
⚠️ Warning: multiple scopes detected in Staged

Global suggested message:
type(scope): description

---

Scope: ScopeName
type(scope): description
- Acción en español
- Acción en español

Scope: ScopeName
type(scope): description
- Acción en español
- Acción en español

Additional rules:
- Commit message always in English, strict conventional commits
- Bullets always in Spanish
- Do not commit, only generate the text
- Do not add explanations outside the defined format
