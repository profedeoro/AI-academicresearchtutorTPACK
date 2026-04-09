# Research Progress Dashboard

## Overview

Track research progress through the pipeline phases using data from the research journal, quality reports, and git history. Provides Learning Analytics for both students and supervisors.

**AI-TPACK dimension:** TPK (Tecnologia + Pedagogia) -- monitoreo pedagogico mediado por tecnologia.

**Theoretical basis:**
- Learning Analytics (Siemens & Long, 2011; Ferguson, 2012)
- Supervision monitoring predicts student success (De Kleijn et al., 2012; Pyhaltto et al., 2015)
- Self-regulated learning (Zimmerman, 2002; Pintrich, 2000)

## Student Version (Default)

### Data Collection

Read from these sources:
1. `quality_reports/research_journal.md` -- Agent actions, scores, phase transitions
2. `SESSION_REPORT.md` -- Session history, decisions, commits
3. `quality_reports/reviews/` -- Critic reports and scores
4. `git log --oneline --since="30 days ago"` -- Activity frequency

### Dashboard Output

```markdown
# Research Progress Report -- [Project Name]
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

- [ ] Explorer-critic score (78) below 80 -- needs revision before submission
- [ ] Execution: Code not yet started -- depends on Strategy (COMPLETE)

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

### Supervision Alerts

```markdown
## Supervision Alerts

| Alert | Student | Details | Severity |
|-------|---------|---------|----------|
| INACTIVITY | [name] | No activity for 14+ days | HIGH |
| STALLED | [name] | Strategy phase: 3 rounds without convergence | MEDIUM |
| LOW SCORE | [name] | Literature score 65/100, below 80 threshold | HIGH |
| ON TRACK | [name] | Execution phase, score 88 | INFO |
```

### Comparative Progress

```markdown
## Comparative Progress

| Student | Phase | Overall Score | Activity (30d) | Risk |
|---------|-------|---------------|----------------|------|
| [A] | Execution | 85 | 12 sessions | LOW |
| [B] | Strategy | 72 | 3 sessions | HIGH |
| [C] | Discovery | 68 | 8 sessions | MEDIUM |
```

### Intervention Recommendations

Based on Learning Analytics patterns:
- **Low activity + low score:** Suggests disengagement. Recommend: scheduled check-in
- **Active but low score:** Suggests skill gaps. Recommend: targeted feedback on weak dimensions
- **High activity + high score:** On track. Minimal intervention needed
- **Declining scores:** Regression pattern. Recommend: review recent changes, possible conceptual confusion

### Version Comparison (Teacher Only)

Compare successive versions of student deliverables:
```bash
git diff [old_hash]..[new_hash] -- paper/sections/introduction.tex
```

Highlight:
- Structural improvements (sections added/reorganized)
- Argument strengthening (new citations, clearer claims)
- Writing quality (hedging reduction, clarity improvements)
- Quantitative changes (new tables, updated figures)

### Automated Rubric (Teacher Only)

Map quality scores to rubric dimensions:

| Dimension | Source | Weight | Score |
|-----------|--------|--------|-------|
| Problem Formulation | strategist-critic | 20% | [score] |
| Literature Review | librarian-critic | 15% | [score] |
| Methodology | strategist-critic + coder-critic | 25% | [score] |
| Writing Quality | writer-critic | 20% | [score] |
| Data Handling | explorer-critic + coder-critic | 10% | [score] |
| Presentation | storyteller-critic (advisory) | 10% | [score] |

**Principle:** This is a preliminary assessment. The teacher validates, modifies, or overrides -- it is NEVER the final evaluation.

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
- All data derived from existing artifacts -- no new instrumentation required
- Rubric scores are NEVER presented to students as final grades
- Teacher dashboard is a supervision aid, not an automated evaluation system
