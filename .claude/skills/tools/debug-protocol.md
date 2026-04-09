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
   - `git diff` -- what changed since last working version?
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
   - See `debug-root-cause-tracing.md` for the complete backward tracing technique.

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
   - Don't assume "that can't matter" -- package load order matters in LaTeX, library order matters in R

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

   This connects to the three-strikes escalation routing in `agents.md`.

## Red Flags -- STOP

If you catch yourself thinking:
- "Just rerun the script, maybe it's a random error"
- "Just add `try-catch` around it"
- "Comment out the problematic line for now"
- "The results are close enough, probably a rounding issue"
- "Just change the package version"
- "Add `results='hide'` so the warning doesn't show"

**ALL of these mean: STOP. Return to Phase 1.**

## Common Rationalizations

| Excuse | Reality |
|--------|---------|
| "Issue is simple, don't need process" | Simple issues have root causes too. Process is fast for simple bugs. |
| "Deadline pressure, no time for process" | Systematic debugging is FASTER than guess-and-check thrashing. |
| "Just try this first, then investigate" | First fix sets the pattern. Do it right from the start. |
| "The warning is harmless" | Warnings become errors at peer review. Investigate now. |
| "Multiple fixes at once saves time" | Can't isolate what worked. Causes new bugs. |
| "I see the problem, let me fix it" | Seeing symptoms != understanding root cause. |

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
  model <- fixest::feols(Y ~ D | FE, data = df),
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
| Discovery | Low -- document and continue | Early exploration, issues are learning |
| Strategy | Medium -- fix before coding | Strategy errors cascade to all code |
| Execution | High -- fix immediately | Bugs in code produce wrong results |
| Peer Review | Critical -- fix and re-verify | Referees will catch what you don't |
