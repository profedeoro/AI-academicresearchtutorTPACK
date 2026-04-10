# Research Progress Dashboard

## Overview

Track research progress through the pipeline phases using data from the research journal, quality reports, student profile, and git history. Provides Learning Analytics for both students and supervisors.

**AI-TPACK dimension:** TPK (Tecnologia + Pedagogia) -- monitoreo pedagogico mediado por tecnologia.

**Theoretical basis:**
- Learning Analytics (Siemens & Long, 2011; Ferguson, 2012)
- Supervision monitoring predicts student success (De Kleijn et al., 2012; Pyhaltto et al., 2015)
- Self-regulated learning (Zimmerman, 2002; Pintrich, 2000)
- Evidence-Centered Design (Mislevy et al., 2003)
- ICAP Framework (Chi & Wylie, 2014)

---

## Student Version (Default)

### Data Collection

Read from these sources:
1. `quality_reports/student-profile.md` -- competency levels, TPACK dimensions, fading history
2. `quality_reports/research_journal.md` -- agent actions, scores, phase transitions
3. `SESSION_REPORT.md` -- session history, decisions, commits
4. `quality_reports/reviews/` -- critic reports and scores
5. `git log --oneline --since="30 days ago"` -- activity frequency

### Dashboard Output

```markdown
# Research Progress Report -- [Project Name]
**Generated:** YYYY-MM-DD HH:MM
**Mode:** Student
**Overall Level:** [Principiante/Intermedio/Avanzado]
**Overall Score:** XX/100 (weighted aggregate)

## TPACK Competency Map

| Dimension | Level | Scaffolding | Last Score | Trend | ECD Status |
|-----------|-------|-------------|------------|-------|------------|
| D1: Problem Formulation | [level] | [Modeling/Coaching/Fading] | [score] | [up/down/stable] | [C1: X/3 evidences] |
| D2: Literature Mastery | [level] | [mode] | [score] | [trend] | [C2: X/3 evidences] |
| D3: Methodological Design | [level] | [mode] | [score] | [trend] | [C3: X/3 evidences] |
| D4: Analytical Competence | [level] | [mode] | [score] | [trend] | [C4: X/3 evidences] |
| D5: Academic Writing | [level] | [mode] | [score] | [trend] | [C5: X/3 evidences] |
| D6: Scientific Communication | [level] | [mode] | [score] | [trend] | [C6: X/3 evidences] |

## Pipeline Status

| Phase | Status | Score | Last Activity | Agent |
|-------|--------|-------|--------------|-------|
| Discovery: Literature | [status] | [score] | [date] | [agent] |
| Discovery: Data | [status] | [score] | [date] | [agent] |
| Strategy | [status] | [score] | [date] | [agent] |
| Execution: Code | [status] | [score] | [date] | [agent] |
| Execution: Paper | [status] | [score] | [date] | [agent] |
| Peer Review | [status] | [score] | [date] | [agent] |
| Submission | [status] | [score] | [date] | [agent] |

## Quality Gate Status

| Gate | Required | Current | Status |
|------|----------|---------|--------|
| Commit | >= 80 | [score] | [PASS/NOT YET] |
| PR | >= 90 | [score] | [PASS/NOT YET] |
| Submission | >= 95 | [score] | [PASS/NOT YET] |

## Learning Interaction Summary (ICAP)

| Level | Count | Percentage |
|-------|-------|------------|
| Passive | [n] | [%] |
| Active | [n] | [%] |
| Constructive | [n] | [%] |
| Interactive | [n] | [%] |

## Activity Summary (Last 30 Days)

- Sessions: [count]
- Commits: [count]
- Agent invocations: [count]
- Most active phase: [phase]
- Days since last activity: [count]

## Fading Progress

- Levels gained: [list of dimension level-ups with dates]
- Next level-up target: [dimension closest to meeting fading criteria]
- Blocking criteria: [what's missing for next level-up]

## Recommended Next Steps

Based on dependency graph, competency status, and current state:
1. [Most impactful next action]
2. [Second priority]
3. [Third priority]
```

---

## Teacher Version (`--teacher`)

### Additional Data Sources

- `quality_reports/student-profile.md` -- per student
- `quality_reports/pedagogical-review.md` -- tutor-pedagogico-critic scores
- Multiple student project directories (if accessible)

### Teacher Dashboard (Text Version)

```markdown
# Teacher Dashboard -- [Course/Program Name]
**Generated:** YYYY-MM-DD HH:MM
**Students monitored:** [count]

## Supervision Alerts

| Alert | Student | Details | Severity |
|-------|---------|---------|----------|
| INACTIVITY | [name] | No activity for 14+ days | HIGH |
| STALLED | [name] | Strategy phase: 3 rounds without convergence | MEDIUM |
| LOW SCORE | [name] | Literature score 65/100, below 80 threshold | HIGH |
| DECLINING | [name] | Scores dropped from 82 to 68 over 3 sessions | HIGH |
| PASSIVE LEARNING | [name] | 80% of interactions are Passive/Active | MEDIUM |
| SELF-ASSESSMENT GAP | [name] | Self-assessment accuracy < 40% | MEDIUM |
| ON TRACK | [name] | Execution phase, score 88, ICAP mostly Constructive | INFO |

## Comparative Progress

| Student | Phase | Overall | Activity (30d) | ICAP Dominant | ECD Status | Risk |
|---------|-------|---------|----------------|---------------|------------|------|
| [A] | Execution | 85 | 12 sessions | Constructive | 14/18 evidences | LOW |
| [B] | Strategy | 72 | 3 sessions | Active | 6/18 evidences | HIGH |
| [C] | Discovery | 68 | 8 sessions | Passive | 4/18 evidences | HIGH |

## Competency Heatmap (Text)

| Student | C1 | C2 | C3 | C4 | C5 | C6 |
|---------|----|----|----|----|----|----|
| [A] | ADV | INT | INT | INT | PRI | PRI |
| [B] | INT | PRI | PRI | -- | -- | -- |
| [C] | PRI | PRI | -- | -- | -- | -- |

(PRI=Principiante, INT=Intermedio, ADV=Avanzado, --=not evaluated)

## Pedagogical Quality Summary

| Agent | Avg Score /20 | Lowest Dimension | Action Needed |
|-------|---------------|------------------|---------------|
| strategist-critic | 16 | Scaffolding (3/4) | Improve Guided Inquiry use |
| writer-critic | 14 | ICAP (2/4) | Enforce Constructive minimum |
| coder-critic | 18 | -- | No action needed |

## Intervention Recommendations

Based on Learning Analytics patterns:
- **[Student B]:** Low activity + low score + Principiante across D2-D3. Recommend: diagnostic review, possible level recalibration. Consider dispatching error-detective for root cause analysis.
- **[Student C]:** Active but Passive ICAP. Student is engaging but not thinking deeply. Recommend: increase ICAP threshold enforcement, add think-aloud protocols.
```

### Deep Investigation (Teacher Only)

When the teacher needs deeper analysis of a specific student:

```
/tools progress --teacher --investigate [student]
```

This dispatches the **error-detective** agent to perform root cause analysis:
- Correlate issues across pipeline phases
- Apply Five Whys for learning difficulties
- Map cross-dimension cascades
- Recommend specific interventions

See `agents/error-detective.md` for the full investigation protocol.

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
- Feedback processing (did student address critic's gaps?)

### Automated Rubric (Teacher Only)

Map quality scores + ECD evidences to rubric dimensions:

| Dimension | Source | Weight | Score | ECD Evidence |
|-----------|--------|--------|-------|-------------|
| Problem Formulation | tutor-pedagogico (diagnostic) | 15% | [score] | C1: [X/3] |
| Literature Review | librarian-critic | 15% | [score] | C2: [X/3] |
| Methodology | strategist-critic + coder-critic | 25% | [score] | C3: [X/3] |
| Implementation | coder-critic | 15% | [score] | C4: [X/3] |
| Writing Quality | writer-critic | 20% | [score] | C5: [X/3] |
| Communication | storyteller-critic (advisory) | 10% | [score] | C6: [X/3] |

**Principle:** This is a preliminary assessment. The teacher validates, modifies, or overrides -- it is NEVER the final evaluation. ECD evidence status provides richer information than scores alone.

---

## Visual Dashboard (`--teacher --visual`)

When the teacher requests a visual dashboard, use the **canvas-design** skill to generate a designed PDF/PNG dashboard.

### Invocation

```
/tools progress --teacher --visual
```

### What It Generates

A single-page designed PDF or PNG using the canvas-design skill that visualizes:

1. **Competency Radar Chart** -- 6 dimensions (D1-D6) plotted as a radar/spider chart with student level (1=Principiante, 2=Intermedio, 3=Avanzado) on each axis. Shows current state and previous state for trajectory.

2. **Pipeline Progress Bar** -- Horizontal progress bar showing completed/in-progress/not-started phases with color coding (green/yellow/gray).

3. **ICAP Distribution** -- Pie or bar chart showing percentage of interactions at each ICAP level (Passive/Active/Constructive/Interactive) with color coding (red/yellow/green/blue).

4. **Score Trajectory** -- Line chart showing overall weighted score across sessions over time. Horizontal lines at 80 (commit), 90 (PR), 95 (submission) thresholds.

5. **Alert Badges** -- Visual indicators for HIGH/MEDIUM/LOW risk with student count per category.

6. **ECD Evidence Matrix** -- Grid showing C1-C6 competencies vs. evidence status (colored dots: green=DEMONSTRATED, yellow=PARTIAL, red=NOT DEMONSTRATED, gray=NOT EVALUATED).

### Design Philosophy

The visual dashboard follows these principles:
- **Academic aesthetic:** Clean, professional, data-forward. Not corporate or flashy.
- **Information density:** One page must communicate the full picture. No fluff.
- **Color palette:** Limited, intentional. Use university/academic tones (deep blues, warm grays, accent gold/teal).
- **Typography:** Minimal text. Data speaks through visual encoding.
- **Craftsmanship:** Must look like a publication-quality figure, not a screenshot.

### Canvas Design Integration

To generate the visual, the progress command:
1. Collects all data (same as text dashboard)
2. Structures data as JSON for visualization
3. Invokes canvas-design skill with the data and design philosophy
4. Outputs PDF to `quality_reports/progress/YYYY-MM-DD_visual_dashboard.pdf`

The canvas-design skill handles the visual rendering. The progress protocol provides the data and layout specification.

---

## Risk Detection Heuristics

| Pattern | Risk Level | Indicator |
|---------|-----------|-----------|
| No activity for 7+ days | MEDIUM | Possible disengagement |
| No activity for 14+ days | HIGH | Intervention needed |
| 3+ rounds same phase | MEDIUM | Possible conceptual block |
| Score declining across sessions | HIGH | Regression, not progress |
| Only using 1-2 commands | LOW | May need guidance on pipeline |
| High activity but low scores | MEDIUM | Effort without direction |
| ICAP > 60% Passive | HIGH | Student not engaging cognitively |
| Self-assessment accuracy < 40% | MEDIUM | Metacognitive gap |
| ECD evidences declining | HIGH | Competency regression |
| Pedagogical quality < 13 consistently | MEDIUM | System not teaching effectively |

## Implementation Notes

- Student version: reads only from current project directory
- Teacher version: needs access to multiple project directories (one per student)
- Visual dashboard: requires canvas-design skill installed
- All data derived from existing artifacts -- no new instrumentation required
- Rubric scores are NEVER presented to students as final grades
- Teacher dashboard is a supervision aid, not an automated evaluation system
- Error-detective dispatch is optional and teacher-initiated only
