---
name: tools
description: Utility commands — commit, compile, validate-bib, lint, journal, context-status, deploy, learn, debug, verify, pre-register, progress. Replaces individual utility skills.
argument-hint: "[subcommand: commit | compile | validate-bib | lint | journal | context | deploy | learn | upgrade | debug | verify | pre-register | progress] [args]"
allowed-tools: Read,Grep,Glob,Write,Edit,Bash,Task
---

# Tools

Utility subcommands for project maintenance and infrastructure.

**Input:** `$ARGUMENTS` — subcommand followed by any arguments.

---

## Subcommands

### `/tools commit [message]` — Git Commit
Stage changes, create commit, optionally create PR and merge.
- Run git status to identify changes
- Stage relevant files (never stage .env or credentials)
- Create commit with descriptive message
- If quality score available and >= 80, note in commit

### `/tools compile [file]` — LaTeX Compilation
3-pass XeLaTeX + biber compilation.

For papers:
```bash
cd paper && TEXINPUTS=preambles:$TEXINPUTS xelatex -interaction=nonstopmode [file]
BIBINPUTS=..:$BIBINPUTS biber [file_base]
TEXINPUTS=preambles:$TEXINPUTS xelatex -interaction=nonstopmode [file]
TEXINPUTS=preambles:$TEXINPUTS xelatex -interaction=nonstopmode [file]
```

For talks:
```bash
cd paper/talks && TEXINPUTS=../preambles:$TEXINPUTS xelatex -interaction=nonstopmode [file]
```

### `/tools validate-bib` — Bibliography Validation
Cross-reference all \cite{} keys in paper and talk files against Bibliography_base.bib.
Report: missing entries, unused entries, duplicate keys.

### `/tools lint [file|dir]` — Mechanical Code Linting
Run grep-based checks on R/Python/Julia scripts against the coding standards' prohibited patterns. Catches mechanical violations before the coder-critic's judgment review.

```bash
"$CLAUDE_PROJECT_DIR"/.claude/hooks/lint-scripts.sh [target]
```

- **Single file:** `/tools lint scripts/02_estimate.R`
- **Directory:** `/tools lint scripts/` (recursive)
- **Default:** `/tools lint` (lints `scripts/`)

**What it checks (drawn from `.claude/references/coding-standards-*.md`):**

| Check | R | Python | Julia | Severity |
|-------|---|--------|-------|----------|
| Absolute paths | x | x | x | HIGH |
| `setwd()` / `os.chdir()` / `cd()` | x | x | x | HIGH |
| Missing seed (stochastic code) | x | x | x | HIGH |
| `install.packages()` / `pip install` | x | x | | HIGH |
| `rm(list = ls())` | x | | | MEDIUM |
| `T`/`F` literals | x | | | MEDIUM |
| `sapply()` | x | | | MEDIUM |
| `attach()`/`detach()` | x | | | MEDIUM |
| `<<-` global assignment | x | | | MEDIUM |
| `stargazer` / `plyr` | x | | | MEDIUM |
| `set.seed()` position (after line 30) | x | | | MEDIUM |
| Wildcard imports | | x | | MEDIUM |
| `np.random.seed()` global state | | x | | MEDIUM |
| Bare `except:` | | x | | MEDIUM |
| `eval`/`@eval` runtime | | | x | MEDIUM |
| Late `library()`/`import`/`using` | x | x | x | LOW |
| `print()` for status | x | | | LOW |
| `require()` | x | | | LOW |
| `1:n` patterns | x | | | LOW |

**Output:** Findings by file with severity, line number, and fix suggestion. Always advisory (exit 0).

**When to use:**
- Before `/review --code` — catches mechanical violations instantly
- Before commits — quick sanity check
- The coder-critic focuses on judgment (strategy alignment, numerical plausibility, design); this catches the grep-able stuff

### `/tools journal` — Research Journal
Regenerate the research journal timeline from quality reports and git history.
Shows chronological record of agent actions, phase transitions, scores, decisions.

### `/tools context` — Context Status
Show current context status and session health.
Check context usage, whether auto-compact is approaching, what state will be preserved.

### `/tools deploy` — Deploy Guide Site
Render Quarto guide site and publish to GitHub Pages.
```bash
cd guide && quarto publish gh-pages --no-browser
```

### `/tools learn` — Extract Learnings
Extract reusable knowledge from the current session. Auto-memory handles corrections automatically; this is for multi-step workflows worth turning into a full skill.

### `/tools upgrade` — Upgrade Clo-Author Infrastructure
Upgrade an existing project to the latest clo-author architecture.

**What it does:**
1. Clone the latest clo-author release into a temp directory
2. Save the user's filled-in domain-profile.md and any custom journal profiles
3. Delete the old `.claude/` directory
4. Copy the new `.claude/` in
5. Restore the user's domain-profile.md and custom journal profiles
6. Optionally copy new `templates/`
7. Report what changed

**Workflow:**
```
Step 1: DOWNLOAD
  - Clone latest clo-author into /tmp/clo-author-upgrade
  - Or: gh release download --repo hugosantanna/clo-author

Step 2: PRESERVE USER CUSTOMIZATIONS
  - Save .claude/references/domain-profile.md if filled in (not just placeholders)
  - Save any custom journal profiles the user added to journal-profiles.md
  - Save .claude/settings.json (user's permissions and hooks)
  - Save .claude/settings.local.json if it exists

Step 3: REPLACE
  - Delete old .claude/ entirely
  - Copy new .claude/ from the downloaded release
  - Restore saved customizations from Step 2

Step 4: DO NOT TOUCH
  - paper/, scripts/, data/, explorations/, quality_reports/
  - CLAUDE.md, Bibliography_base.bib, README.md, .gitignore
  - Any other user content

Step 5: REPORT
  - List what was updated (new agents, skills, rules)
  - List what was preserved (domain profile, settings, custom profiles)
  - Clean up temp directory
```

**No git merge. No upstream remote. No conflicts.** Just delete and replace `.claude/`.

---

### `/tools debug [context]` — Systematic Debugging
Root cause investigation before attempting fixes. Adapted from systematic-debugging for academic research contexts.

**Context types:** `latex` (compilation errors), `script` (R/Stata/Python failures), `data` (pipeline/cleaning issues), `results` (unexpected statistical output).

**Protocol:** See `debug-protocol.md` in this directory.

**AI-TPACK dimension:** TPK (Tecnologia + Pedagogia) — ensenar resolucion sistematica de problemas como competencia investigativa.

**4 phases (must complete in order):**
1. **Investigar causa raiz** — Leer errores, reproducir, revisar cambios recientes
2. **Analizar patron** — Encontrar ejemplos funcionales, comparar diferencias
3. **Hipotesis y prueba** — Formar hipotesis unica, probar minimamente
4. **Implementar fix** — Crear test, fix unico, verificar

**Iron law:** NO HAY FIX SIN INVESTIGACION DE CAUSA RAIZ PRIMERO.

**Integrations:**
- LaTeX errors → dispatches to verifier for compilation check
- Script errors → dispatches to coder + coder-critic for fix + review
- Data issues → dispatches to data-engineer + coder-critic
- Results issues → dispatches to strategist-critic for sanity check

### `/tools verify [target]` — Verification Before Completion
Evidence-based verification gate. No completion claims without fresh verification output.

**Targets:** `compile` (LaTeX 3-pass), `script` (R/Stata/Python execution), `bib` (bibliography cross-reference), `score` (quality gate check), `replication` (full pipeline re-run), `all` (everything).

**Protocol:** See `verify-protocol.md` in this directory.

**AI-TPACK dimension:** AI-TPACK (interseccion total) — verificacion rigurosa es competencia investigativa fundamental.

**The gate function:**
1. IDENTIFICAR — Que comando prueba este claim?
2. EJECUTAR — Correr el comando completo (fresco, no cache)
3. LEER — Output completo, exit code, conteo de errores
4. VERIFICAR — El output confirma el claim?
5. SOLO ENTONCES — Declarar resultado

**Iron law:** NO HAY CLAIM DE COMPLETITUD SIN EVIDENCIA FRESCA DE VERIFICACION.

### `/tools pre-register [analysis]` — Hypothesis-Driven Analysis
Document expected results BEFORE running analysis. Adapted from Test-Driven Development for empirical research — write the "test" (hypothesis) before the "code" (estimation).

**Protocol:** See `pre-register-protocol.md` in this directory.

**AI-TPACK dimension:** PCK (Pedagogia + Contenido) — ensenar investigacion basada en hipotesis, no en fishing de resultados.

**RED-GREEN-REFACTOR for science:**
1. **RED (Hypothesis):** Document expected sign, magnitude, significance BEFORE running
2. **GREEN (Estimation):** Run analysis, compare actual vs. predicted
3. **REFACTOR (Interpretation):** Reconcile differences, add robustness, update narrative

**Iron law:** NO HAY ANALISIS SIN HIPOTESIS DOCUMENTADA PRIMERO.

**Output:** `quality_reports/pre-registration/YYYY-MM-DD_[analysis].md` with prediction vs. actual comparison table.

**Integration:** Works with `/strategize pap` (pre-analysis plan) and `/analyze` (execution).

### `/tools progress [--teacher]` — Research Progress Dashboard
Generate a progress report from the research journal, session reports, and quality scores.

**Protocol:** See `progress-protocol.md` in this directory.

**AI-TPACK dimension:** TPK (Tecnologia + Pedagogia) — Learning Analytics aplicado al seguimiento del proceso investigativo (Siemens & Long, 2011).

**Two versions:**
- **Student version (default):** Own progress, phases completed, current scores, next steps
- **Teacher version (`--teacher`):** All students' progress, alerts, comparative dashboard

**Data sources:** `quality_reports/research_journal.md`, `SESSION_REPORT.md`, `quality_reports/reviews/`, git log.

**Output:** Formatted progress report to console + optionally saved to `quality_reports/progress/YYYY-MM-DD_progress.md`.

---

## Principles
- **Each subcommand is lightweight.** No multi-agent orchestration needed (except debug escalation).
- **Compile always uses 3-pass.** Ensures references and citations resolve.
- **validate-bib catches drift.** Run before commits to catch broken citations.
- **Upgrade preserves content.** Infrastructure changes, your paper doesn't.
- **Debug investigates before fixing.** Root cause first, always.
- **Verify provides evidence.** No claims without fresh verification output.
- **Pre-register predicts before analyzing.** Hypothesis first, estimation second.
- **Progress tracks the journey.** Learning Analytics for students and supervisors.
