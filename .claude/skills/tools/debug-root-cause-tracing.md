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
model <- fixest::feols(Y ~ treatment | fe_state + fe_year, data = panel)
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
# Result: 95% treated, 5% control -- WRONG

# Before merge -- treatment file
table(treatment_df$treated)  # Expected: ~50/50
# Result: 50/50 -- correct here

# The merge itself
merged <- merge(outcomes, treatment_df, by = "id", all.x = TRUE)
table(merged$treated)  # 95/5 -- merge introduced the problem
sum(is.na(merged$treated))  # 450 NAs coded as... 1?!
```

### 5. Find Original Trigger
```r
# The merge has NAs for unmatched observations
# Those NAs were filled with 1 (treated) by a coalesce() call
merged$treated <- dplyr::coalesce(merged$treated, 1L)  # ROOT CAUSE
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

## Key Principle

**NEVER fix just where the error appears.** The wrong sign fix is NOT "multiply by -1" -- it's fixing the merge default upstream.
