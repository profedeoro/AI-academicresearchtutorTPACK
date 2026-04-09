# Verification Protocol for Research Artifacts

## Overview

Claiming a paper compiles, a script runs, or results are correct without verification is dishonesty, not efficiency. In academic research, unverified claims damage credibility permanently.

**Core principle:** Evidence before claims, always.

**Violating the letter of this rule is violating the spirit of this rule.**

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
```

**Verification checklist:**
- [ ] Exit code 0 on all passes
- [ ] Zero "Undefined reference" warnings
- [ ] Zero "Citation undefined" warnings
- [ ] No overfull hbox > 10pt
- [ ] PDF generated with correct page count

### `/tools verify script [file]`
```bash
# Clean execution from scratch
Rscript --vanilla scripts/R/[file].R
```

**Verification checklist:**
- [ ] Exit code 0
- [ ] No errors in output
- [ ] No unexpected warnings
- [ ] Expected output files created
- [ ] Output dimensions match expectations
- [ ] Key statistics within plausible range

### `/tools verify bib`
```bash
# Cross-reference citations against bibliography
grep -ohrP '\\cite[tp]?\{[^}]+\}' paper/ | grep -oP '\{[^}]+\}' | tr ',' '\n' | sed 's/[{}]//g' | tr -d ' ' | sort -u > /tmp/cited.txt
grep -oP '@\w+\{([^,]+)' Bibliography_base.bib | sed 's/@.*{//' | sort -u > /tmp/bibkeys.txt
```

**Verification checklist:**
- [ ] All cited keys exist in .bib
- [ ] No orphan .bib entries (warning, non-blocking)
- [ ] No duplicate keys

### `/tools verify score`
Read latest quality scores from `quality_reports/`.

**Verification checklist:**
- [ ] Overall weighted aggregate calculated
- [ ] Compare against gate threshold (80 commit, 90 PR, 95 submission)
- [ ] All component scores present
- [ ] No component below 80 (for submission gate)

### `/tools verify replication`
```bash
# Full pipeline re-run from clean state (requires user confirmation for data deletion)
Rscript --vanilla scripts/R/00_clean_data.R
Rscript --vanilla scripts/R/01_main_analysis.R
Rscript --vanilla scripts/R/02_robustness.R
# Then: /tools verify compile
```

**Verification checklist:**
- [ ] All scripts run without error
- [ ] Output files match previous versions (within tolerance)
- [ ] Tables and figures regenerated
- [ ] Paper compiles with new outputs

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

## Red Flags -- STOP

- Using "should compile", "probably runs", "looks correct"
- Expressing satisfaction before running verification
- About to commit without running `/tools verify compile`
- Trusting a previous verification run (stale evidence)
- Relying on partial verification ("the main script runs" without robustness)
- Skipping verification because "only changed a comment"

## Rationalization Prevention

| Excuse | Reality |
|--------|---------|
| "Should work now" | RUN the verification |
| "I'm confident" | Confidence is not evidence |
| "Just this once" | No exceptions |
| "Only changed a comment" | Comments can break LaTeX. Verify. |
| "Previous run was clean" | Stale evidence is no evidence |
| "Partial check is enough" | Partial proves nothing |

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
