---
description: Local council of 4 fixed roles (Security, Performance, Maintainability, Devil's Advocate) that analyze a question + this project's code, and can optionally implement the resulting recommendations one by one. No external dependencies or AI providers — 4 Claude subagents, each with its own lens, followed by a final synthesis. Output is entirely in Spanish.
argument-hint: '--q "your question" | --impl'
allowed-tools: Agent, AskUserQuestion, Read, Glob, Grep, Write, Edit
---

# /use-council

Convenes a local council of 4 fixed roles to analyze a question about this
project's code. No external APIs or scripts — 4 Claude subagents
(`general-purpose`), each blind to the others, each with a fixed lens.

**IMPORTANT — language split:** every instruction below is written in English
for you (the orchestrating model) to follow. Every user-facing question,
status message, and — critically — the entire generated `council.md` output
MUST be written in Spanish. Do not mix languages in the deliverable.

**Honest framing (never drop this from the final output):** the 4 members are
the same model playing different roles. They share prior knowledge, so
agreement between them is a weak signal, not cross-validation. The real value
is angle coverage and blind-spot detection, not consensus.

## Step -1 — Detect mode

If `--impl` is present anywhere in `$ARGUMENTS`, this is **Implementation
Mode** — skip straight to the "Implementation Mode (--impl)" section at the
bottom of this file, ignore everything else, and do not treat `--impl` as
part of a question.

Otherwise, this is **Analysis Mode** — continue with Step 0 below.

## Step 0 — Extract the question and the goal

From `$ARGUMENTS`, take the text following `--q` (quoted or not) as the
user's question. If there is no `--q` but `$ARGUMENTS` has text, use all of
`$ARGUMENTS` as the question.

**If `$ARGUMENTS` is completely empty** (you ran `/use-council` with nothing
after it), follow this conversational sequence in the chat, one thing at a
time, waiting for the user's reply before moving to the next:

1. Ask directly, in Spanish: "¿Cuál es tu pregunta para el consejo?" and wait
   for the answer — that is Step 0's question.
2. Then ask, in Spanish: "¿Cuál es el objetivo de este análisis?" (e.g.
   revisión antes de un PR, decisión de diseño, debugging, evaluación previa a
   producción) and wait for the answer. Keep this goal alongside the question
   — it gets added to the context the 4 roles receive.

These two questions go straight into the chat as plain text, not via
`AskUserQuestion` — just two simple conversational turns before Step 1.

## Step 1 — Up to 5 context questions

Before analyzing, use `AskUserQuestion` to surface context the code alone
can't give you. Maximum 5 questions, and only the ones that genuinely help —
don't pad to 5 if 2 or 3 already give you what you need. Think of questions
like:

- Which specific files, folder, or module should be reviewed? (if not obvious
  from the question)
- What's the goal of this analysis? (PR review, design decision, debugging,
  pre-production evaluation, etc.)
- Are there constraints or priorities that should weigh more? (performance
  over readability, tight deadline, acceptable tech debt, etc.)
- Is there anything already decided that you do NOT want the council to
  second-guess? (closed decisions)
- Expected depth? (quick / standard / exhaustive)

Every question and its options must be written in Spanish — the user
interacts in Spanish. Each question needs concrete options (the UI adds
"Otro" automatically for free text). Don't ask about roles or output format —
those are fixed by this command's design.

## Step 1.5 — Status message before starting

Before reading code or spawning subagents, write a short, direct message in
the chat (plain text, not a file), in Spanish, confirming you have what you
need and the process is starting — e.g. "Perfecto, ya tengo lo necesario.
Convoco al consejo y en un momento te traigo el resumen." This message must
be visible in the console before Step 2 begins, so the user knows the command
is already working instead of waiting on another question.

## Step 2 — Gather code context

With the question and Step 1's answers:

1. If the user pointed at specific files/folders, read them with `Read`.
2. Otherwise, use `Glob`/`Grep` to locate relevant files from keywords in the
   question (function names, paths, domain terms). Cap at ~5-8 files so you
   don't overload each role's context.
3. Assemble one context block (question + goal + Step 1 answers + relevant
   code snippets with their paths) that gets sent identically to all 4 roles.

## Step 3 — Convene the 4 roles in parallel

The 4 roles are fixed, not configurable. Their Spanish display names below
are the ones that must appear in the final output:

| Role (Spanish name to use in output) | Lens |
|---|---|
| **Seguridad** | Vulnerabilities, injection risks, authentication/authorization issues, data exposure, OWASP Top 10. |
| **Rendimiento** | Bottlenecks, unnecessary allocations, N+1 queries, caching opportunities, time/space complexity, scalability. |
| **Mantenibilidad** | Code clarity, naming, modularity, test coverage, how easy this will be for another dev to understand and change in 6 months. |
| **Abogado del Diablo** | Challenges design assumptions, points out what could go wrong, hidden complexity, argues for alternatives even if unconventional. |

Launch **all 4 in a single message** (4 parallel `Agent` calls) with
`subagent_type: "general-purpose"` and `run_in_background: true`, so they run
concurrently and blind to each other.

For each role, the subagent prompt must include:

1. The context block from Step 2 (question + goal + answers + code).
2. The assigned lens (one row from the table above, verbatim).
3. An explicit instruction: "You are independent, you do not see the other
   roles' answers. Respond ONLY in Spanish and ONLY in this exact Markdown
   format, with no text outside these sections":

```markdown
## Posición
(2-4 frases: tu postura general desde tu lente, respondiendo directamente la pregunta del usuario)

## Puntos clave
- (3-6 bullets con lo más importante que encontraste desde tu lente)

## Riesgos y puntos ciegos
- (qué podría salir mal si se ignora tu lente; incluye riesgos que las otras lentes probablemente no vean)

## Veredicto
(una categoría: Aprobado / Aprobado con reservas / Necesita cambios / Rechazado — la que mejor represente tu conclusión desde esta lente)

## Calidad
(nota X/10 específica a tu lente, con una frase justificándola)
```

## Step 4 — Collect results

Wait for all 4 background subagents to finish (they arrive as automatic
notifications). If one fails, note it and continue with the rest — don't
relaunch the call.

## Step 5 — Display each perspective

First show this banner, verbatim, in Spanish:

> **Consejo local** — las 4 perspectivas vienen de Claude interpretando roles
> distintos, no de proveedores de IA diferentes. Trata las coincidencias entre
> roles como un punto de partida común a cuestionar, no como validación
> independiente.

Then, for each role, a heading with its Spanish name and its full answer:

```
## 🗳️ {Nombre del rol}

{Posición / Puntos clave / Riesgos y puntos ciegos / Veredicto / Calidad del subagente}
```

## Step 6 — Final synthesis

Close with your own synthesis (not delegated to a subagent), written in
Spanish, focused on angles and coverage, NOT on "how many agreed":

- **Puntos de partida compartidos** — where 2+ roles converged. Frame this
  explicitly as a shared prior to stress-test, not confirmation, and ask what
  they might all be missing for the same reason.
- **Tensiones reales** — where the roles pull in different directions, and
  what the user's specific situation implies about which tension matters
  most here.
- **Puntos ciegos cruzados** — risks one role raised that another role's
  approach would walk straight into. Also flag anything no role covered.
- **Veredictos y calidad en conjunto** — a summary table with each role's
  verdict and score.
- **Recomendación final** — your best actionable synthesis, naming which
  roles support it and where real uncertainty remains. Write this section so
  each recommendation is a **clear, standalone, actionable statement**
  (concrete change, not a vague opinion) — Implementation Mode below parses
  this section to build its checklist.

## Step 7 — Save the result

Write the full result (banner + all 4 perspectives + synthesis), entirely in
Spanish, to **`council.md` at the project root** — not in a subfolder, not
timestamped. If `council.md` already exists, overwrite it; this command
always keeps a single, current copy at the root. Tell the user the file was
saved at `council.md` when done.

## Error handling (Analysis Mode)

- If a role fails, show it and continue with the rest.
- If all 4 fail, report clearly and suggest retrying.
- If only 1 role answers, say so explicitly — that's not a "council", it's a
  single role-played opinion.

---

## Implementation Mode (--impl)

Walks the recommendations from an existing `council.md` one at a time, asking
whether to implement each before touching any code.

### Step A — Locate or generate `council.md`

Check whether `council.md` exists at the project root.

- **If it does NOT exist**: run the full Analysis Mode flow above (Steps -1
  through 7, treating this as a normal `/use-council` run — ask for the
  question/goal, context questions, spawn the 4 roles, synthesize, save) to
  produce it. Once `council.md` is saved, continue to Step B.
- **If it exists**: read it directly and continue to Step B.

### Step B — Extract actionable recommendations

Parse `council.md`, primarily its **Recomendación final** section, and also
scan **Riesgos y puntos ciegos** (per role) and **Puntos ciegos cruzados**
(synthesis) for anything concrete and actionable.

Build a numbered list of candidate recommendations. Each item must be a
**concrete, implementable change** — a specific edit, refactor, guard, test,
or fix. Discard vague opinions that aren't actionable (e.g. "mejorar la
mantenibilidad en general" is not a candidate; "extraer la validación de
`X` en un Form Request" is). If, after filtering, there are zero actionable
items, tell the user in Spanish and stop — don't invent work.

### Step C — Walk through recommendations one by one

For each recommendation, in order:

1. Print its full text in the chat, in Spanish, so the user can read and
   remember it before deciding — don't summarize it down to a title only.
2. Use `AskUserQuestion` with a single question: "¿Implementar esta
   recomendación?" with options: "Sí, implementar" / "No, omitir" /
   "Modificar antes de implementar". If the user picks "Modificar", ask in
   the chat what to change, adjust the recommendation accordingly, and
   confirm before implementing.
3. If accepted: implement it now, following this project's existing
   conventions (thin, minimal, no unrelated refactors — see the project's own
   CLAUDE.md rules). Use `Read`/`Edit`/`Write` as needed. After implementing,
   show a short summary of what changed (files touched, one line each).
4. If declined: skip it and move to the next recommendation without touching
   any files.
5. Continue until every recommendation from Step B has been resolved.

### Step D — Final summary

Once all recommendations are resolved, print a short summary in Spanish: what
was implemented, what was skipped, and what was modified from the original
suggestion — so the user has a clear record of what actually changed in the
codebase versus what `council.md` originally suggested.

Then **append** (do not overwrite) that same summary to the end of
`council.md`, under a new top-level section, in Spanish:

```markdown
---

## Resultado de la implementación ({FECHA})

Para cada recomendación procesada, una línea:

- ✅ Implementado — {texto de la recomendación} (`{archivos tocados}`)
- ⏭️ Omitido — {texto de la recomendación}
- ✏️ Modificado e implementado — {texto original} → {qué se implementó en su lugar} (`{archivos tocados}`)
```

If `council.md` already has a "Resultado de la implementación" section from a
previous `--impl` run, append this run's results as a **new dated block**
below the existing one rather than replacing it — `council.md` keeps a
running history of implementation runs, even though the analysis above it
gets overwritten on each new `/use-council` (non-`--impl`) run.

### Error handling (Implementation Mode)

- If `council.md` can't be parsed into any recommendation, say so in Spanish
  and stop instead of guessing.
- If implementing a recommendation fails (e.g. file not found, conflicting
  change), report the failure for that item, leave it marked as not
  implemented, and continue with the next recommendation — don't abort the
  whole run over one failure.
