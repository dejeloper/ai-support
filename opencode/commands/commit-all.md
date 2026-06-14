---
description: Safely group changes into semantic commits with validation and controlled push
---

Group all current changes into meaningful semantic commits while preserving repository integrity and minimizing incorrect assumptions.

Optional context for commit messages: ``

## Priorities

1. Security
2. Historical consistency
3. Semantic quality
4. Speed

If conflicts arise, prioritize in this order.

---

## Rules

- First inspect the full repository state:
  - `git status --short`
  - `git diff --stat`
  - `git diff`
  - `git log --oneline -10`

- Identify related file groups by impact and intent: feature, fix, refactor, tests, docs, chore, release, or config.
  - Prioritize semantic precision
  - Group by impact over intention when necessary

- Commit grouping strategy:
  - Prefer small, semantically precise commits
  - Even minimal changes (e.g., typo fixes) can be standalone commits
  - If a change cannot be safely split, group into a single broader commit
  - If a file mixes concerns:
    - Attempt splitting into multiple commits (order: fix → refactor → feature)
    - If not viable, create a single commit explaining the mixture

- Include new, modified, and deleted files relevant to each group
  - Partially related files should be included in the closest semantic group

- Only create multiple commits when changes are reasonably separable
  - Avoid artificial fragmentation

- Use clear, semantic, and concise commit messages
  - Follow existing repository conventions (e.g., conventional commits) if present

- Before committing, check for:
  - Sensitive files (`.env`, credentials, tokens, secrets)
  - Generated artifacts (`dist/`, `build/`, `.next/`, etc.)
  - Unexpected large files
  - If any appear, stop and ask

- Do not:
  - Revert existing changes
  - Use `--no-verify`
  - Amend commits
  - Force push
  - Perform `git push` under any circumstance

---

## Remote Awareness

- Always synchronize remote state before evaluation:
  - `git fetch`
  - `git status`

- If the branch is behind remote:
  - Notify only (do not auto-resolve)

- If conflicts are likely:
  - Stop and notify

---

## Validation

- Perform validation only after all commits are created:
  - Build (required)
  - Lint (required)
  - Tests (only if they exist)

- If any validation fails:
  - Do not block commits
  - Clearly warn about failures

---

## Flow

1. Analyze changes and propose a commit plan:
   - List each commit
   - Include files per commit
   - Provide a short justification

2. If grouping is reasonably clear, continue
   - If there is high risk (sensitive files or severe ambiguity), stop and ask

3. For each group:
   - Stage only relevant files: `git add <files>`
   - Create commit with semantic message
   - Ensure logical consistency

4. After all commits:
   - Re-check repository status
   - Run validation (build, lint, tests if available)
   - Verify remote state (`git fetch` + `git status`)
   - Warn about any issues

5. When finished:
   - Summarize commits created
   - Specify current branch
   - Report assumptions made
   - Highlight any risks or inconsistencies
   - Leave repository ready for manual push
