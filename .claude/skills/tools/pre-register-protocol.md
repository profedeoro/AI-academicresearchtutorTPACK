# Pre-Registration Protocol: Hypothesis-Driven Analysis

## Overview

Running analysis without documented expectations is data mining, not science. If you didn't predict the result before seeing it, you don't know if you discovered something or found noise.

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
- If $\gamma$ has opposite sign -> [interpretation]
- If $\gamma$ is zero -> [interpretation]
- If placebo test shows significant effect -> [interpretation]
- If results are not robust to [check] -> [interpretation]
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
| Add controls | Stable | $\gamma$ moved from 0.12 to 0.11 | YES -- within 20% |
| Alt. clustering | Wider SEs | SEs increased 40%, still significant at 5% | YES |
| Placebo | Zero | $\gamma = 0.02$, p = 0.45 | YES -- null as expected |

### Heterogeneity

| Subgroup | Predicted | Actual | Match? |
|---|---|---|---|
| [Group A] | Larger | $\gamma_A = 0.18$*** | YES |
| [Group B] | Null | $\gamma_B = 0.03$, n.s. | YES |

### Surprises and Deviations

List any results that did NOT match predictions:
1. [Describe deviation] -- [Possible explanation] -- [Follow-up needed?]
```

## REFACTOR Phase: Interpret and Strengthen

- If predictions matched: Strengthen confidence in findings, document in paper
- If predictions didn't match: DO NOT hide the deviation
  - Investigate why (return to `/tools debug results`)
  - Document the deviation transparently
  - Revise theory if needed
  - Add additional robustness checks

## Red Flags -- STOP

- "I'll document my predictions after seeing the results" -- That's post-hoc rationalization
- "The result is obvious, no need to predict" -- Obvious results still need documentation
- "Pre-registration is only for RCTs" -- Prediction discipline applies to ALL empirical work
- "I already know what the data shows" -- Then document it. If you're right, it strengthens your claim
- "This is just exploratory" -- Label it as such and skip, but don't pretend exploration is confirmation

## Common Rationalizations

| Excuse | Reality |
|--------|---------|
| "I'll predict after" | Post-hoc prediction is not prediction |
| "Result is obvious" | Obvious still needs documentation |
| "Only for RCTs" | Prediction discipline is universal |
| "Just exploratory" | Label it honestly, then |
| "Theory doesn't predict magnitude" | Predict sign and direction at minimum |
| "Too many specifications" | Pre-register the main spec, note the rest as exploratory |

## Integration with clo-author Pipeline

```
/strategize --> Strategy memo (identification approach)
     |
/tools pre-register --> Documented predictions (BEFORE analysis)
     |
/analyze --> Estimation results
     |
/tools pre-register (update) --> Predictions vs. actuals comparison
     |
/write results --> Paper narrative informed by pre-registration
```

## Pedagogical Value (AI-TPACK: PCK)

For students, this protocol teaches:
1. **Hypothesis formulation** -- Force clear, testable predictions
2. **Theoretical grounding** -- Every prediction needs a "Why"
3. **Scientific integrity** -- Document before, compare after
4. **Transparency** -- Deviations are learning, not failure
5. **Robustness thinking** -- Predict what should and shouldn't change

The tutor IA guides the student through each prediction, asking: "What do you expect? Why? What would falsify this?"
