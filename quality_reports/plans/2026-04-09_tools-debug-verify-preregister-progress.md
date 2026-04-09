# New Tools Subcommands Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add 4 new subcommands to the `/tools` skill: `debug`, `verify`, `pre-register`, and `progress` — each adapted from superpowers patterns to the academic research context of clo-author and mapped to AI-TPACK dimensions.

**Architecture:** Each subcommand is added to the existing `tools/SKILL.md` with a concise entry. Subcommands that require detailed protocols get companion `.md` files in the same `tools/` directory. No new agents are created — these subcommands integrate with existing worker-critic pairs.

**Tech Stack:** Markdown (SKILL.md + companion files), Bash (git/LaTeX commands for verify), existing clo-author agent infrastructure.

---

## File Structure

```
clo-author/.claude/skills/tools/
├── SKILL.md                          # MODIFY: Add 4 new subcommand entries
├── debug-protocol.md                 # CREATE: Systematic debugging for academic research
├── debug-root-cause-tracing.md       # CREATE: Root cause tracing adapted for scripts/LaTeX
├── verify-protocol.md                # CREATE: Verification gate function for research artifacts
├── pre-register-protocol.md          # CREATE: Hypothesis-driven analysis (TDD for science)
└── progress-protocol.md              # CREATE: Student/teacher progress dashboard
```

**Responsibilities:**
- `SKILL.md` — Entry point with concise description of each subcommand (routing)
- `*-protocol.md` — Detailed protocol, phases, examples, red flags (loaded on demand)

---

### Task 1: Add `/tools debug` subcommand entry to SKILL.md

**Files:**
- Modify: `clo-author/.claude/skills/tools/SKILL.md`

- [ ] **Step 1: Add debug subcommand entry after the upgrade section**

Add this block before the `## Principles` section in SKILL.md:

```markdown
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
```

- [ ] **Step 2: Update the SKILL.md frontmatter description and argument-hint**

Change the frontmatter to include new subcommands:

```yaml
---
name: tools
description: Utility commands — commit, compile, validate-bib, journal, context-status, deploy, learn, debug, verify, pre-register, progress. Replaces individual utility skills.
argument-hint: "[subcommand: commit | compile | validate-bib | journal | context | deploy | learn | upgrade | debug | verify | pre-register | progress] [args]"
allowed-tools: Read,Grep,Glob,Write,Edit,Bash,Task
---
```

- [ ] **Step 3: Verify SKILL.md is valid markdown**

Run: `cat clo-author/.claude/skills/tools/SKILL.md | head -5`
Expected: Updated frontmatter with new subcommands listed.

---

### Task 2: Create debug-protocol.md

**Files:**
- Create: `clo-author/.claude/skills/tools/debug-protocol.md`

- [ ] **Step 1: Write the debug protocol adapted for academic research**

```markdown
# Debugging Protocol for Academic Research

## Overview

Random fixes waste time and create new bugs in scripts, LaTeX, and data pipelines. Quick patches mask underlying issues that will resurface during peer review or replication.

**Core principle:** ALWAYS find root cause before attempting fixes. Symptom fixes are failure.

**Violating the letter of this process is violating the spirit of debugging.**

## The Iron Law

```
NO HAY FIX SIN INVESTIGACION DE CAUSA RAIZ PRIMERO
```

If you haven't completed Phase 1, you cannot propose fixes.

## When to Use

Use `/tools debug` for ANY technical issue in the research pipeline:

| Context | Examples |
|---------|----------|
| `latex` | Compilation errors, missing references, overfull hboxes, broken citations, package conflicts |
| `script` | R/Stata/Python runtime errors, package loading failures, unexpected NAs, convergence failures |
| `data` | Merge mismatches, encoding issues, missing observations, inconsistent variable types |
| `results` | Wrong sign on coefficients, implausible magnitudes, failed sanity checks, non-convergent models |

**Use ESPECIALLY when:**
- Under deadline pressure (urgency makes guessing tempting)
- "Just rerun the script" seems like the fix
- Previous fix didn't resolve the issue
- Coder-critic flagged an issue you don't fully understand

## The Four Phases

Complete each phase before proceeding to the next.

### Phase 1: Root Cause Investigation

**BEFORE attempting ANY fix:**

1. **Read Error Messages Carefully**
   - LaTeX: Read the full `.log` file, not just the terminal summary
   - R: Read the full traceback including `warnings()`
   - Stata: Check return codes and `r()`/`e()` scalars
   - Python: Read the full traceback, check imported module versions

2. **Reproduce Consistently**
   - Can you trigger it reliably with `set.seed()` and same data?
   - Does it happen on clean run or only after partial execution?
   - If not reproducible -> gather more data, don't guess

3. **Check Recent Changes**
   - `git diff` — what changed since last working version?
   - New packages? Changed data cleaning steps? Modified variable names?
   - Did the data source update?

4. **Trace Data Flow (for script/data/results issues)**
   - Where does the problematic value originate?
   - Track the variable through the pipeline: raw data -> cleaning -> transformation -> analysis
   - Add diagnostic output at each stage:
   ```r
   # R diagnostic example
   cat("=== After merge ===\n")
   cat("Rows:", nrow(df), "\n")
   cat("NAs in treatment:", sum(is.na(df$treatment)), "\n")
   cat("Treatment values:", unique(df$treatment), "\n")
   ```

5. **Trace Reference Chain (for LaTeX issues)**
   - Which `.tex` file triggers the error?
   - Is the problem in the preamble, a specific section, or a generated table?
   - Does `\input{}` or `\include{}` point to the right file?
   - Is `Bibliography_base.bib` missing the cited key?

### Phase 2: Pattern Analysis

1. **Find Working Examples**
   - Locate similar working code in `scripts/` or `paper/sections/`
   - Compare a working table `.tex` with the broken one
   - Check the reference preamble in `working-paper-format.md`

2. **Compare Against References**
   - LaTeX: Check against `preambles/` and `working-paper-format.md`
   - R/Stata: Check against the strategy memo in `quality_reports/`
   - Data: Check against the data assessment from explorer

3. **Identify Differences**
   - List every difference between working and broken
   - Don't assume "that can't matter" — package load order matters in LaTeX, library order matters in R

### Phase 3: Hypothesis and Testing

1. **Form Single Hypothesis**
   - "The merge is dropping observations because the key variable has trailing whitespace"
   - Be specific, not "something is wrong with the merge"

2. **Test Minimally**
   - ONE change at a time
   - For scripts: isolate the failing step in a minimal reproduction
   - For LaTeX: compile a minimal document with just the problematic element

3. **Verify Before Continuing**
   - Hypothesis confirmed? -> Phase 4
   - Not confirmed? -> NEW hypothesis, don't stack fixes

### Phase 4: Implementation

1. **Fix the Root Cause**
   - Address the source, not the symptom
   - ONE change at a time
   - No "while I'm here" improvements

2. **Verify Fix**
   - LaTeX: Full 3-pass compilation clean
   - Scripts: Full run from clean state with `set.seed()`
   - Data: Check row counts, NA counts, summary statistics match expectations

3. **Dispatch for Review**
   - Script fixes -> coder-critic reviews
   - Data fixes -> coder-critic reviews (data-engineer context)
   - LaTeX fixes -> verifier compilation check
   - Results issues -> strategist-critic sanity check

4. **If 3+ Fixes Failed: Escalate**
   - Script issues -> strategist-critic re-evaluates if strategy is implementable
   - Data issues -> explorer re-evaluates data feasibility
   - Results issues -> User (fundamental design question)
   - LaTeX issues -> Check if preamble needs restructuring

## Red Flags — STOP

If you catch yourself thinking:
- "Just rerun the script, maybe it's a random error"
- "Just add `try-catch` around it"
- "Comment out the problematic line for now"
- "The results are close enough, probably a rounding issue"
- "Just change the package version"
- "Add `results='hide'` so the warning doesn't show"

**ALL of these mean: STOP. Return to Phase 1.**

## Context-Specific Quick Reference

### LaTeX Debugging
```bash
# Step 1: Find the actual error (not just "there were errors")
grep -n "^!" paper/main.log | head -20

# Step 2: Check for undefined references
grep -c "undefined" paper/main.log

# Step 3: Check for missing citations
grep "Citation.*undefined" paper/main.log

# Step 4: Verify bib entries exist
grep "key_name" Bibliography_base.bib
```

### R Script Debugging
```r
# Step 1: Clean environment
rm(list = ls()); set.seed(12345)

# Step 2: Run line by line, checking dimensions
source("scripts/R/00_clean_data.R")
cat("After cleaning:", nrow(df), "obs,", ncol(df), "vars\n")

# Step 3: Check for silent coercion
str(df$treatment_var)
summary(df$outcome_var)

# Step 4: Isolate the failing estimation
tryCatch(
  model <- feols(Y ~ D | FE, data = df),
  error = function(e) cat("Error:", conditionMessage(e), "\n")
)
```

### Stata Script Debugging
```stata
* Step 1: Check data state
describe, short
codebook treatment_var, compact

* Step 2: Check merge quality
merge 1:1 id using "data/cleaned/panel.dta"
tab _merge

* Step 3: Isolate estimation
cap noi reghdfe Y D, absorb(FE) cluster(cluster_var)
if _rc != 0 di "Error code: " _rc
```

## Severity by Phase (from quality.md)

| Project Phase | Debug Urgency | Rationale |
|---------------|---------------|-----------|
| Discovery | Low — document and continue | Early exploration, issues are learning |
| Strategy | Medium — fix before coding | Strategy errors cascade to all code |
| Execution | High — fix immediately | Bugs in code produce wrong results |
| Peer Review | Critical — fix and re-verify | Referees will catch what you don't |

## Integration with Three-Strikes Escalation

If the debug protocol reaches Phase 4 Step 4 (3+ fixes failed), it connects to the escalation routing in `agents.md`:
- Coder issues -> strategist-critic
- Data-engineer issues -> strategist-critic
- Writer issues -> Orchestrator
- Strategist issues -> User

This is NOT a failed hypothesis — it may be a wrong approach.
```

---

### Task 3: Create debug-root-cause-tracing.md

**Files:**
- Create: `clo-author/.claude/skills/tools/debug-root-cause-tracing.md`

- [ ] **Step 1: Write root cause tracing adapted for research pipelines**

```markdown
# Root Cause Tracing for Research Pipelines

## Overview

Bugs in research pipelines manifest downstream but originate upstream. A wrong coefficient in your regression table may trace back to a merge error in data cleaning, not to the estimation code.

**Core principle:** Trace backward through the data/compilation pipeline until you find the original trigger, then fix at the source.

## The Tracing Process

### 1. Observe the Symptom
```
Example: "Treatment effect has wrong sign (positive instead of negative)"
```

### 2. Find Immediate Cause
What code directly produces this output?
```r
# The regression producing the wrong sign
model <- feols(Y ~ treatment | fe_state + fe_year, data = panel)
```

### 3. Ask: What Fed This?
```
feols() <- panel dataset <- merge of treatment + outcome
  <- treatment assignment from 00_clean_data.R
  <- raw data from data/raw/treatment_assignments.csv
```

### 4. Keep Tracing Up
Check at each stage:
```r
# After merge
table(panel$treatment)  # Expected: ~50/50 split
# Result: 95% treated, 5% control — WRONG

# Before merge — treatment file
table(treatment_df$treated)  # Expected: ~50/50
# Result: 50/50 — correct here

# The merge itself
merged <- merge(outcomes, treatment_df, by = "id", all.x = TRUE)
table(merged$treated)  # 95/5 — merge introduced the problem
sum(is.na(merged$treated))  # 450 NAs coded as... 1?!
```

### 5. Find Original Trigger
```r
# The merge has NAs for unmatched observations
# Those NAs were filled with 1 (treated) by a coalesce() call
merged$treated <- coalesce(merged$treated, 1L)  # ROOT CAUSE
# Should be: coalesce(merged$treated, 0L) for control group default
```

## Common Research Pipeline Traces

### Wrong Regression Results
```
Wrong coefficient
  <- estimation code (check specification)
  <- dataset (check merge, check variable construction)
  <- raw data (check encoding, check import)
  <- data source (check documentation, check vintage)
```

### LaTeX Compilation Failure
```
Undefined reference error
  <- \ref{} or \cite{} call in section file
  <- label exists in target? (check \label{} in tables/figures)
  <- file included? (check \input{} path in main.tex)
  <- file generated? (check if script produced the .tex table)
```

### Broken Replication
```
Different results on clean run
  <- random seed (check set.seed() placement)
  <- package versions (check renv.lock or sessionInfo())
  <- data vintage (check data/raw/ matches original)
  <- OS differences (check floating point, sorting)
```

## Key Principle

**NEVER fix just where the error appears.** The wrong sign fix is NOT "multiply by -1" — it's fixing the merge default upstream.

## Diagnostic Instrumentation

When you can't trace manually, add checkpoints:

```r
# Add to each pipeline stage
cat("=== Stage:", "00_clean", "===\n")
cat("Rows:", nrow(df), "| Cols:", ncol(df), "\n")
cat("Treatment split:", table(df$treatment), "\n")
cat("Outcome range:", range(df$Y, na.rm = TRUE), "\n")
cat("NAs:", colSums(is.na(df)), "\n")
```

Run the full pipeline once with diagnostics. The stage where numbers diverge from expectations is your root cause location.
```

---

### Task 4: Add `/tools verify` subcommand entry to SKILL.md

**Files:**
- Modify: `clo-author/.claude/skills/tools/SKILL.md`

- [ ] **Step 1: Add verify subcommand entry after debug**

```markdown
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
```

---

### Task 5: Create verify-protocol.md

**Files:**
- Create: `clo-author/.claude/skills/tools/verify-protocol.md`

- [ ] **Step 1: Write the verification protocol**

```markdown
# Verification Protocol for Research Artifacts

## Overview

Claiming a paper compiles, a script runs, or results are correct without verification is dishonesty, not efficiency. In academic research, unverified claims damage credibility permanently.

**Core principle:** Evidence before claims, always.

## The Iron Law

```
NO HAY CLAIM DE COMPLETITUD SIN EVIDENCIA FRESCA DE VERIFICACION
```

If you haven't run the verification command in this interaction, you cannot claim it passes.

## The Gate Function

```
BEFORE claiming any status:

1. IDENTIFICAR: Que comando prueba este claim?
2. EJECUTAR: Correr el comando COMPLETO (fresco, no de cache)
3. LEER: Output completo, exit code, conteo de errores/warnings
4. VERIFICAR: El output confirma el claim?
   - Si NO: Reportar estado actual con evidencia
   - Si SI: Declarar claim CON evidencia
5. SOLO ENTONCES: Hacer el claim

Saltar cualquier paso = mentir, no verificar
```

## Verification Targets

### `/tools verify compile`
```bash
# Full 3-pass compilation
cd paper && TEXINPUTS=preambles:$TEXINPUTS xelatex -interaction=nonstopmode main.tex
BIBINPUTS=..:$BIBINPUTS bibtex main
TEXINPUTS=preambles:$TEXINPUTS xelatex -interaction=nonstopmode main.tex
TEXINPUTS=preambles:$TEXINPUTS xelatex -interaction=nonstopmode main.tex

# Verification checklist:
# [ ] Exit code 0 on all passes
# [ ] Zero "Undefined reference" warnings
# [ ] Zero "Citation undefined" warnings
# [ ] No overfull hbox > 10pt
# [ ] PDF generated with correct page count
```

### `/tools verify script [file]`
```bash
# Clean execution from scratch
Rscript --vanilla scripts/R/[file].R

# Verification checklist:
# [ ] Exit code 0
# [ ] No errors in output
# [ ] No unexpected warnings
# [ ] Expected output files created
# [ ] Output dimensions match expectations
# [ ] Key statistics within plausible range
```

### `/tools verify bib`
```bash
# Cross-reference citations
grep -oP '\\cite[tp]?\{[^}]+\}' paper/**/*.tex | sort -u > /tmp/cited_keys.txt
grep -oP '@\w+\{([^,]+)' Bibliography_base.bib | sort -u > /tmp/bib_keys.txt

# Verification checklist:
# [ ] All cited keys exist in .bib
# [ ] No orphan .bib entries (optional warning)
# [ ] No duplicate keys
```

### `/tools verify score`
```
# Read latest quality scores from quality_reports/
# Verification checklist:
# [ ] Overall weighted aggregate calculated
# [ ] Compare against gate threshold (80 commit, 90 PR, 95 submission)
# [ ] All component scores present
# [ ] No component below 80 (for submission gate)
```

### `/tools verify replication`
```bash
# Full pipeline re-run from clean state
rm -rf data/cleaned/*  # Only if user confirms
Rscript --vanilla scripts/R/00_clean_data.R
Rscript --vanilla scripts/R/01_main_analysis.R
Rscript --vanilla scripts/R/02_robustness.R
# Then verify compile

# Verification checklist:
# [ ] All scripts run without error
# [ ] Output files match previous versions (within tolerance)
# [ ] Tables and figures regenerated
# [ ] Paper compiles with new outputs
```

### `/tools verify all`
Run all applicable targets in sequence: `bib` -> `script` -> `compile` -> `score`.

## Common Failures

| Claim | Requires | NOT Sufficient |
|-------|----------|----------------|
| "Paper compiles" | 3-pass xelatex output: 0 errors | "It compiled yesterday" |
| "Script runs clean" | Full Rscript output: exit 0 | "I ran the main part" |
| "Bibliography is valid" | Cross-reference check: 0 missing | "I added the entry" |
| "Score >= 80" | Critic report with calculated score | "The code looks good" |
| "Results are correct" | Sanity checks pass: sign, magnitude | "The model converged" |
| "Replication package works" | Full clean run: all outputs match | "I included all files" |

## Red Flags — STOP

- Using "should compile", "probably runs", "looks correct"
- Expressing satisfaction before running verification
- About to commit without running `/tools verify compile`
- Trusting a previous verification run (stale evidence)
- Relying on partial verification ("the main script runs" without robustness)
- Skipping verification because "only changed a comment"

## Integration with Quality Gates

| Gate | Required Verification |
|------|----------------------|
| Commit (>= 80) | `/tools verify compile` + `/tools verify script` |
| PR (>= 90) | `/tools verify all` |
| Submission (>= 95) | `/tools verify replication` + `/tools verify all` |

## Severity Calibration

| Phase | Verification Rigor |
|-------|-------------------|
| Discovery | Compile check sufficient |
| Strategy | Compile + script basics |
| Execution | Full verify all |
| Peer Review | Full verify replication |
| Submission | Full verify replication + independent re-run |
```

---

### Task 6: Add `/tools pre-register` subcommand entry to SKILL.md

**Files:**
- Modify: `clo-author/.claude/skills/tools/SKILL.md`

- [ ] **Step 1: Add pre-register subcommand entry after verify**

```markdown
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
```

---

### Task 7: Create pre-register-protocol.md

**Files:**
- Create: `clo-author/.claude/skills/tools/pre-register-protocol.md`

- [ ] **Step 1: Write the pre-registration protocol**

```markdown
# Pre-Registration Protocol: Hypothesis-Driven Analysis

## Overview

Running analysis without documented expectations is data mining, not science. If you didn't predict the result before seeing it, you don't know if you discovered something or if you found noise.

**Core principle:** Document what you expect BEFORE running the analysis. Compare predictions to results AFTER.

This is Test-Driven Development applied to empirical research.

## The Iron Law

```
NO HAY ANALISIS SIN HIPOTESIS DOCUMENTADA PRIMERO
```

Ran the regression before documenting expectations? The pre-registration is invalid. Document expectations based on theory and prior literature, not on results you've already seen.

## The TDD-Science Mapping

| TDD (Software) | Research (Science) | Purpose |
|---|---|---|
| Write failing test | Document hypothesis with expected sign, magnitude | Forces thinking BEFORE seeing data |
| Run test (RED) | Confirm prediction is falsifiable | Ensures hypothesis is testable |
| Write code (GREEN) | Run estimation, compare to prediction | Tests hypothesis against evidence |
| Refactor | Interpret discrepancies, add robustness | Strengthens or revises understanding |

## When to Use

**Always before:**
- Main specification estimation
- Robustness checks (predict which should/shouldn't change results)
- Heterogeneity analysis (predict which subgroups show effects)
- Placebo tests (predict null results)

**Exceptions (ask user):**
- Purely exploratory analysis (clearly labeled as such)
- Descriptive statistics (no causal claim)
- Data cleaning/validation steps

## RED Phase: Document Hypotheses

Before running ANY estimation, create:

```
quality_reports/pre-registration/YYYY-MM-DD_[analysis_name].md
```

### Template

```markdown
# Pre-Registration: [Analysis Name]
**Date:** YYYY-MM-DD
**Analyst:** [name]
**Strategy memo:** [link to strategy document]

## Main Specification

### Hypothesis 1: [Name]
- **Equation:** $Y_{it} = \alpha + \gamma D_{it} + X_{it}\beta + \delta_i + \theta_t + \varepsilon_{it}$
- **Coefficient of interest:** $\gamma$ (treatment effect)
- **Expected sign:** [positive/negative/zero]
- **Expected magnitude:** [range, with units]
- **Expected significance:** [at what level: 1%, 5%, 10%]
- **Reasoning:** [Why do you expect this? Cite theory or prior evidence]

### Hypothesis 2: [Name]
[Same structure]

## Robustness Predictions

| Check | What Changes | Expected Effect on $\gamma$ | Why |
|-------|-------------|---------------------------|-----|
| Add controls $Z$ | More covariates | Stable (within 20%) | If identification is valid, adding controls shouldn't change point estimate substantially |
| Alternative clustering | Cluster at state level | Wider SEs, same point | Clustering affects inference, not identification |
| Placebo treatment | Fake treatment timing | Zero effect | No effect expected before actual treatment |
| Subsample: [group] | Restricted sample | [Larger/smaller/same] | [Theory-based reasoning] |

## Heterogeneity Predictions

| Subgroup | Expected Effect | Why |
|----------|----------------|-----|
| [Group A] | Larger than average | [Theory] |
| [Group B] | Smaller/null | [Theory] |

## Falsification Criteria

What would DISPROVE your hypothesis?
- If $\gamma$ has opposite sign → [interpretation]
- If $\gamma$ is zero → [interpretation]
- If placebo test shows significant effect → [interpretation]
- If results are not robust to [check] → [interpretation]
```

## GREEN Phase: Run and Compare

After estimation, add to the SAME document:

```markdown
## Results vs. Predictions

### Main Specification

| Hypothesis | Predicted | Actual | Match? | Interpretation |
|---|---|---|---|---|
| H1: Treatment effect | $\gamma > 0$, ~0.15 | $\gamma = 0.12$** | YES | Slightly smaller than expected, consistent with theory |
| H2: [Name] | [prediction] | [actual] | [YES/NO/PARTIAL] | [explanation] |

### Robustness

| Check | Predicted Effect | Actual Effect | Match? |
|---|---|---|---|
| Add controls | Stable | $\gamma$ moved from 0.12 to 0.11 | YES — within 20% |
| Alt. clustering | Wider SEs | SEs increased 40%, still significant at 5% | YES |
| Placebo | Zero | $\gamma = 0.02$, p = 0.45 | YES — null as expected |

### Heterogeneity

| Subgroup | Predicted | Actual | Match? |
|---|---|---|---|
| [Group A] | Larger | $\gamma_A = 0.18$*** | YES |
| [Group B] | Null | $\gamma_B = 0.03$, n.s. | YES |

### Surprises and Deviations

List any results that did NOT match predictions:
1. [Describe deviation] — [Possible explanation] — [Follow-up needed?]
```

## REFACTOR Phase: Interpret and Strengthen

- If predictions matched: Strengthen confidence in findings, document in paper
- If predictions didn't match: DO NOT hide the deviation
  - Investigate why (return to `/tools debug results`)
  - Document the deviation transparently
  - Revise theory if needed
  - Add additional robustness checks

## Red Flags — STOP

- "I'll document my predictions after seeing the results" — That's post-hoc rationalization
- "The result is obvious, no need to predict" — Obvious results still need documentation
- "Pre-registration is only for RCTs" — Prediction discipline applies to ALL empirical work
- "I already know what the data shows" — Then document it. If you're right, it strengthens your claim
- "This is just exploratory" — Label it as such and skip, but don't pretend exploration is confirmation

## Integration with clo-author Pipeline

```
/strategize → Strategy memo (identification approach)
     ↓
/tools pre-register → Documented predictions (BEFORE analysis)
     ↓
/analyze → Estimation results
     ↓
/tools pre-register (update) → Predictions vs. actuals comparison
     ↓
/write results → Paper narrative informed by pre-registration
```

## Pedagogical Value (AI-TPACK: PCK)

For students, this protocol teaches:
1. **Hypothesis formulation** — Force clear, testable predictions
2. **Theoretical grounding** — Every prediction needs a "Why"
3. **Scientific integrity** — Document before, compare after
4. **Transparency** — Deviations are learning, not failure
5. **Robustness thinking** — Predict what should and shouldn't change

The tutor IA guides the student through each prediction, asking: "What do you expect? Why? What would falsify this?"
```

---

### Task 8: Add `/tools progress` subcommand entry to SKILL.md

**Files:**
- Modify: `clo-author/.claude/skills/tools/SKILL.md`

- [ ] **Step 1: Add progress subcommand entry after pre-register**

```markdown
### `/tools progress [--teacher]` — Research Progress Dashboard
Generate a progress report from the research journal, session reports, and quality scores.

**Protocol:** See `progress-protocol.md` in this directory.

**AI-TPACK dimension:** TPK (Tecnologia + Pedagogia) — Learning Analytics aplicado al seguimiento del proceso investigativo (Siemens & Long, 2011).

**Two versions:**
- **Student version (default):** Own progress, phases completed, current scores, next steps
- **Teacher version (`--teacher`):** All students' progress, alerts, comparative dashboard

**Data sources:** `quality_reports/research_journal.md`, `SESSION_REPORT.md`, `quality_reports/reviews/`, git log.

**Output:** Formatted progress report to console + optionally saved to `quality_reports/progress/YYYY-MM-DD_progress.md`.
```

---

### Task 9: Create progress-protocol.md

**Files:**
- Create: `clo-author/.claude/skills/tools/progress-protocol.md`

- [ ] **Step 1: Write the progress dashboard protocol**

```markdown
# Research Progress Dashboard

## Overview

Track research progress through the pipeline phases using data from the research journal, quality reports, and git history. Provides Learning Analytics for both students and supervisors.

**AI-TPACK dimension:** TPK (Tecnologia + Pedagogia) — monitoreo pedagogico mediado por tecnologia.

**Theoretical basis:**
- Learning Analytics (Siemens & Long, 2011; Ferguson, 2012)
- Supervision monitoring predicts student success (De Kleijn et al., 2012; Pyhaltto et al., 2015)
- Self-regulated learning (Zimmerman, 2002; Pintrich, 2000)

## Student Version (Default)

### Data Collection
Read from these sources:
1. `quality_reports/research_journal.md` — Agent actions, scores, phase transitions
2. `SESSION_REPORT.md` — Session history, decisions, commits
3. `quality_reports/reviews/` — Critic reports and scores
4. `git log --oneline --since="30 days ago"` — Activity frequency

### Dashboard Output

```markdown
# Research Progress Report — [Project Name]
**Generated:** YYYY-MM-DD HH:MM
**Overall Score:** XX/100 (weighted aggregate)

## Pipeline Status

| Phase | Status | Score | Last Activity | Agent |
|-------|--------|-------|--------------|-------|
| Discovery: Literature | COMPLETE | 85/100 | 2026-03-15 | librarian-critic |
| Discovery: Data | COMPLETE | 78/100 | 2026-03-18 | explorer-critic |
| Strategy | COMPLETE | 82/100 | 2026-03-22 | strategist-critic |
| Execution: Code | IN PROGRESS | --/100 | 2026-04-01 | coder |
| Execution: Paper | NOT STARTED | --/100 | -- | -- |
| Peer Review | NOT STARTED | --/100 | -- | -- |
| Submission | NOT STARTED | --/100 | -- | -- |

## Quality Gate Status

| Gate | Required | Current | Status |
|------|----------|---------|--------|
| Commit | >= 80 | 82 | PASS |
| PR | >= 90 | 82 | NOT YET |
| Submission | >= 95 | 82 | NOT YET |

## Activity Summary (Last 30 Days)

- Sessions: [count]
- Commits: [count]
- Agent invocations: [count]
- Most active phase: [phase name]
- Days since last activity: [count]

## Blocking Issues

- [ ] Explorer-critic score (78) below 80 — needs revision before submission
- [ ] Execution: Code not yet started — depends on Strategy (COMPLETE)

## Recommended Next Steps

Based on dependency graph and current state:
1. [Most impactful next action]
2. [Second priority]
3. [Third priority]
```

## Teacher Version (`--teacher`)

### Additional Data
- Compare across multiple student projects (if accessible)
- Aggregate activity patterns
- Identify students at risk (low activity, stalled phases)

### Teacher Dashboard Additions

```markdown
## Supervision Alerts

| Alert | Student | Details | Severity |
|-------|---------|---------|----------|
| INACTIVITY | [name] | No activity for 14+ days | HIGH |
| STALLED | [name] | Strategy phase: 3 rounds without convergence | MEDIUM |
| LOW SCORE | [name] | Literature score 65/100, below 80 threshold | HIGH |
| ON TRACK | [name] | Execution phase, score 88 | INFO |

## Comparative Progress

| Student | Phase | Overall Score | Activity (30d) | Risk |
|---------|-------|---------------|----------------|------|
| [A] | Execution | 85 | 12 sessions | LOW |
| [B] | Strategy | 72 | 3 sessions | HIGH |
| [C] | Discovery | 68 | 8 sessions | MEDIUM |

## Intervention Recommendations

Based on Learning Analytics patterns:
- [Student B]: Low activity + low score suggests disengagement. Recommend: scheduled check-in
- [Student C]: Active but low score suggests skill gaps. Recommend: targeted feedback on literature search
```

## Version Comparison (Teacher Only)

Compare successive versions of student deliverables:
```bash
# Compare versions of a section
git diff [old_hash]..[new_hash] -- paper/sections/introduction.tex
```

Highlight:
- Structural improvements (sections added/reorganized)
- Argument strengthening (new citations, clearer claims)
- Writing quality (hedging reduction, clarity improvements)
- Quantitative changes (new tables, updated figures)

## Automated Rubric (Teacher Only)

Map quality scores to rubric dimensions:

| Dimension | Source | Weight | Score |
|-----------|--------|--------|-------|
| Problem Formulation | strategist-critic | 20% | [score] |
| Literature Review | librarian-critic | 15% | [score] |
| Methodology | strategist-critic + coder-critic | 25% | [score] |
| Writing Quality | writer-critic | 20% | [score] |
| Data Handling | explorer-critic + coder-critic | 10% | [score] |
| Presentation | storyteller-critic (advisory) | 10% | [score] |

**Principle:** This is a preliminary assessment. The teacher validates, modifies, or overrides — it is NEVER the final evaluation.

## Risk Detection Heuristics

| Pattern | Risk Level | Indicator |
|---------|-----------|-----------|
| No activity for 7+ days | MEDIUM | Possible disengagement |
| No activity for 14+ days | HIGH | Intervention needed |
| 3+ rounds same phase | MEDIUM | Possible conceptual block |
| Score declining across sessions | HIGH | Regression, not progress |
| Only using 1-2 commands | LOW | May need guidance on pipeline |
| High activity but low scores | MEDIUM | Effort without direction |

## Implementation Notes

- Student version: Reads only from current project directory
- Teacher version: Needs access to multiple project directories (one per student)
- All data derived from existing artifacts — no new instrumentation required
- Rubric scores are NEVER presented to students as final grades
- Teacher dashboard is a supervision aid, not an automated evaluation system
```

---

### Task 10: Update SKILL.md Principles section

**Files:**
- Modify: `clo-author/.claude/skills/tools/SKILL.md`

- [ ] **Step 1: Update the Principles section to reflect new subcommands**

Replace the existing Principles section with:

```markdown
## Principles
- **Each subcommand is lightweight.** No multi-agent orchestration needed (except debug escalation).
- **Compile always uses 3-pass.** Ensures references and citations resolve.
- **validate-bib catches drift.** Run before commits to catch broken citations.
- **Upgrade preserves content.** Infrastructure changes, your paper doesn't.
- **Debug investigates before fixing.** Root cause first, always.
- **Verify provides evidence.** No claims without fresh verification output.
- **Pre-register predicts before analyzing.** Hypothesis first, estimation second.
- **Progress tracks the journey.** Learning Analytics for students and supervisors.
```

---

## Self-Review Checklist

- [x] All 4 subcommands have entries in SKILL.md
- [x] All 4 subcommands have detailed protocol companion files
- [x] Each subcommand maps to an AI-TPACK dimension
- [x] debug integrates with existing worker-critic escalation
- [x] verify integrates with existing quality gates (80/90/95)
- [x] pre-register integrates with /strategize and /analyze
- [x] progress uses existing data sources (research_journal, SESSION_REPORT, quality_reports)
- [x] No redundancy with existing subcommands (commit, compile, validate-bib, journal, context, deploy, learn, upgrade)
- [x] Teacher-specific features clearly separated (--teacher flag)
- [x] No placeholder text — all sections have actual content
- [x] File paths are exact and consistent
