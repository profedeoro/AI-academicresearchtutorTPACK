# TPACK Agent Redesign — Design Specification

**Date:** 2026-04-09
**Status:** APPROVED
**Author:** Daniel Eduardo Villalba de Oro + Claude Opus 4.6
**Project:** Ecosistema IA como Tutor Virtual para Competencias Investigativas en Posgrado
**Institution:** Politecnico Grancolombiano

---

## 1. Problem Statement

The 18 agents in clo-author are designed for an autonomous economics researcher publishing papers. They assume expert-to-expert communication, give evaluative (not formative) feedback, contain economics-specific jargon, and have zero TPACK logic. This makes them unsuitable for the AI-TPACK ecosystem described in the research spec, where the IA acts as a pedagogical actor (third actor in the student-IA-teacher triad) that teaches research competencies to graduate students.

## 2. Goals

1. Redesign agents with TPACK logic that distinguishes between disciplinary, pedagogical, and technological knowledge
2. Implement two modes: Teacher (expert, current behavior) and Student (tutor with 3 levels)
3. Add a 5-layer pedagogical framework grounded in educational science
4. Create 2 new agents: tutor-pedagogico (supervisor) + tutor-pedagogico-critic (pedagogical quality)
5. Preserve the existing research pipeline logic entirely — add pedagogy, don't replace research

## 3. Theoretical Foundations

### 3.1 Five Pedagogical Layers

| Layer | Framework | Function | Authors |
|---|---|---|---|
| L1: Feedback | Hattie & Timperley + Shute | Structure of feedback (feed up/back/forward + timing + specificity) | Hattie & Timperley (2007), Shute (2008) |
| L2: Self-Regulation | Nicol & Macfarlane-Dick | Foster student self-monitoring and self-regulation | Nicol & Macfarlane-Dick (2006) |
| L3: Disciplinary Scaffolding | Cognitive Apprenticeship + Guided Inquiry | Teach research: modeling, coaching, scaffolding, fading | Collins, Brown & Newman (1989); Kuhlthau et al. (2007) |
| L4: Assessment | Evidence-Centered Design | Model competencies, define evidence, design tasks | Mislevy, Steinberg & Almond (2003) |
| L5: Interaction | ICAP | Design interactions that force thinking, not passive consumption | Chi & Wylie (2014) |

### 3.2 TPACK Mapping

| Dimension | Agents | What it means for the tutor |
|---|---|---|
| CK (Content) | domain-referee | Disciplinary knowledge the student must learn |
| PK (Pedagogical) | tutor-pedagogico | How to teach research competencies |
| TK (Technological) | verifier | Tools (R, LaTeX, databases) as means of learning |
| PCK (Pedagogy + Content) | strategist, writer, methods-referee | Teaching the WHY behind methodological and writing choices |
| TCK (Technology + Content) | librarian, explorer | Using search tools to access disciplinary knowledge |
| TPK (Technology + Pedagogy) | coder, storyteller, data-engineer | Using computational tools as learning artifacts |
| AI-TPACK (Full intersection) | tutor-pedagogico, orchestrator, editor, strategist | Full integration of pedagogy + technology + content |

## 4. Architecture

### 4.1 Modes of Operation

```
CLAUDE.md --> mode: teacher | student
                        |
                  [student]
                        |
              diagnostic-rubric
                        |
            +--------+--------+--------+
        Principiante  Intermedio  Avanzado
```

- `mode: teacher` --> agents operate as current (expert-to-expert), TPACK sections ignored
- `mode: student` --> TPACK sections activated + tutor-pedagogico supervises

### 4.2 New Components

| Component | Type | Location | Function |
|---|---|---|---|
| tutor-pedagogico | Agent (worker) | `.claude/agents/tutor-pedagogico.md` | Diagnostic, progress supervision, fading decisions, ICAP monitoring |
| tutor-pedagogico-critic | Agent (critic) | `.claude/agents/tutor-pedagogico-critic.md` | Evaluates pedagogical quality of feedback from all agents |
| tpack-pedagogical-framework.md | Reference | `.claude/references/tpack-pedagogical-framework.md` | 5 frameworks operationalized (loaded on demand) |
| tpack-competency-model.md | Reference | `.claude/references/tpack-competency-model.md` | ECD: competencies, evidence, tasks by phase |
| tpack-diagnostic-rubric.md | Reference | `.claude/references/tpack-diagnostic-rubric.md` | Scientific diagnostic rubric |

### 4.3 Modified Components

All 18 existing agents receive a `## Modo Tutor (TPACK)` section (~40-55 lines each) at the end of their `.md` file. This section is ONLY active when `mode: student`.

### 4.4 Student Mode Pipeline Flow

```
New session --> tutor-pedagogico runs diagnostic
    --> Generates student-profile.md
    --> Orchestrator reads profile, injects into each agent
    --> For each phase:
        1. PRE: tutor-pedagogico briefing (adapted to level)
        2. WORKER: executes with TPACK section active
           --> Includes self-assessment pre-delivery (Nicol P2)
        3. CRITIC: feedback in Feed Up/Back/Forward format
        4. POST: tutor-pedagogico translation + comprehension checkpoint
        5. QUALITY: tutor-pedagogico-critic evaluates pedagogical quality
        6. FADING: tutor-pedagogico updates profile
        7. NEXT: next phase per dependency graph
```

## 5. Diagnostic System

### 5.1 Six Diagnostic Dimensions

| # | Dimension | TPACK | Phases Impacted | What It Measures |
|---|---|---|---|---|
| D1 | Problem Formulation | CK | discover, strategize | Can articulate a researchable question with clear contribution |
| D2 | Literature Mastery | TCK | discover lit | Can search, evaluate, and synthesize academic sources |
| D3 | Methodological Design | PCK | strategize | Understands method assumptions, can defend choices |
| D4 | Analytical Competence | TPK | analyze | Can implement, interpret, and verify analysis in code |
| D5 | Academic Writing | PCK | write | Can construct evidence-based arguments without hedging |
| D6 | Scientific Communication | TPK | talk, review | Can present and defend findings to critical audience |

### 5.2 Diagnostic Method

Semi-structured interview conducted by tutor-pedagogico using Guided Inquiry (Kuhlthau et al., 2007). 6-8 adaptive questions — each response determines depth of next question.

### 5.3 Classification Rubric

| Level | Observable Indicators | Scaffolding Mode |
|---|---|---|
| Principiante | Cannot articulate without guidance. Unfamiliar with technical vocabulary. Has not practiced the competency. | Modeling (Cognitive Apprenticeship) |
| Intermedio | Articulates with imprecisions. Knows vocabulary but applies inconsistently. Has practiced with guidance. | Coaching + Scaffolding |
| Avanzado | Articulates precisely. Applies vocabulary correctly. Has practiced autonomously. | Fading |

### 5.4 Output: Student Profile

Saved to `quality_reports/student-profile.md`:

```markdown
# Student TPACK Profile
**Generated:** YYYY-MM-DD
**Updated:** YYYY-MM-DD
**Overall Level:** [Principiante/Intermedio/Avanzado]

## Competency Map
| Dimension | Level | Evidence | TPACK | Scaffolding Mode |
|---|---|---|---|---|
| D1 | [level] | [diagnostic evidence] | CK | [mode] |
| D2 | [level] | [diagnostic evidence] | TCK | [mode] |
| D3 | [level] | [diagnostic evidence] | PCK | [mode] |
| D4 | [level] | [diagnostic evidence] | TPK | [mode] |
| D5 | [level] | [diagnostic evidence] | PCK | [mode] |
| D6 | [level] | [diagnostic evidence] | TPK | [mode] |

## Fading Criteria
Principiante --> Intermedio: score >= 75 AND comprehension >= 2/3 AND ICAP >= Active AND 2/3 ECD evidences
Intermedio --> Avanzado: score >= 85 AND comprehension 3/3 AND ICAP >= Constructive AND 3/3 ECD evidences AND 2 consecutive improving phases
```

## 6. Five Pedagogical Layers — Operationalization

### 6.1 Layer 1: Structured Feedback (Hattie & Timperley, 2007 + Shute, 2008)

Applied in: Every critic agent's TPACK section.

Every feedback MUST contain:
- **Feed Up:** Learning objective for this phase + success criteria
- **Feed Back:** Strengths first, then max 3 priority gaps with WHY each matters (Shute: elaborative, specific, task-oriented)
- **Feed Forward:** Concrete action per gap + example if Principiante + resource if Intermedio

Language adaptation:
- Principiante: explain every technical concept
- Intermedio: jargon with brief definition
- Avanzado: free jargon

### 6.2 Layer 2: Self-Regulation (Nicol & Macfarlane-Dick, 2006)

Applied in: Worker agents (pre-delivery) + critic agents (post-feedback).

| Principle | Where | How |
|---|---|---|
| P1: Clarify criteria | Worker (pre-task) | Show criteria BEFORE student works |
| P2: Foster self-assessment | Worker (pre-delivery) | 3 self-assessment questions before critic review |
| P3: Quality information | Critic (feedback) | Specific, elaborative, manageable (Shute) |
| P4: Foster dialogue | Agent (post-feedback) | "What part of the feedback is unclear? Do you disagree?" |
| P5: Motivate positively | Critic (feedback) | Always start with genuine strengths |
| P6: Close the gap | Critic (feed forward) | Concrete action + resource + example |
| P7: Inform teacher | tutor-pedagogico | Reports for /tools progress --teacher |

Self-assessment mechanism: Worker asks 3 domain-specific questions before sending artifact to critic. Critic RECEIVES self-assessment and contrasts with own evaluation. Differences = learning opportunities.

### 6.3 Layer 3: Disciplinary Scaffolding (Collins et al., 1989 + Kuhlthau et al., 2007)

Applied in: Worker agents' TPACK section.

| Method | Level | Tutor IA | Student |
|---|---|---|---|
| Modeling | Principiante | Shows complete solved example, narrates decisions | Observes, asks questions, replicates |
| Coaching | Intermedio | Guides while student executes, asks probing questions | Executes with support, makes decisions |
| Scaffolding | Intermedio | Provides partial structure (templates, checklists) | Completes structure, justifies decisions |
| Fading | Avanzado | Withdraws support, reviews at end | Executes autonomously, asks for help if needed |

Guided Inquiry phases mapped to pipeline:
- Open --> /discover interview
- Immerse --> /discover lit
- Explore --> /discover data + /strategize
- Identify --> /strategize
- Gather --> /analyze
- Create --> /write + /talk

### 6.4 Layer 4: Evidence-Based Assessment (Mislevy et al., 2003)

Applied in: Critic agents' TPACK section + tutor-pedagogico.

ECD 3-layer model: Competency --> Evidence --> Task

| Competency | Evidences | Tasks | Phase |
|---|---|---|---|
| C1: Formulates researchable problems | E1.1: Delimited question. E1.2: Literature-justified relevance. | /discover interview | discover |
| C2: Evaluates literature critically | E2.1: Identifies gaps. E2.2: Distinguishes primary/secondary. E2.3: Organizes by relevance. | /discover lit | discover |
| C3: Designs empirical strategy | E3.1: Specifies and defends assumptions. E3.2: Anticipates objections. E3.3: Proposes robustness. | /strategize | strategy |
| C4: Implements analysis | E4.1: Code matches strategy exactly. E4.2: Sanity checks pass. E4.3: Can explain each step. | /analyze | execution |
| C5: Writes academically | E5.1: Clear contribution in first 2 pages. E5.2: Evidence-backed claims. E5.3: No hedging/AI language. | /write | execution |
| C6: Communicates findings | E6.1: Coherent narrative. E6.2: Clear visuals. E6.3: Defends under questioning. | /talk + /review | presentation |

Key principle: Artifact score and competency demonstration are INDEPENDENT. Score 85/100 but E3.1 = NO means competency C3 is NOT demonstrated. Scores measure product quality; ECD measures learning.

### 6.5 Layer 5: Interaction Design (Chi & Wylie, 2014)

Applied in: All agents' TPACK section + tutor-pedagogico-critic verification.

| ICAP Level | Student Activity | Learning | Example |
|---|---|---|---|
| Passive | Receives without processing | Minimal | Reads feedback without responding |
| Active | Manipulates/repeats | Low | Corrects errors without understanding why |
| Constructive | Generates new ideas beyond input | High | Explains choices, anticipates objections |
| Interactive | Co-constructs with agent | Maximum | Debates validity of assumptions with critic |

Minimum ICAP by student level:
- Principiante: Active (must correct AND explain what changed and why)
- Intermedio: Constructive (must generate justifications, anticipate objections)
- Avanzado: Interactive (must debate, defend decisions, co-construct)

Enforcement: Agents do NOT proceed until student response reaches minimum ICAP level. Max 2 attempts per checkpoint; if not reached, register as "needs reinforcement" and continue.

## 7. New Agents

### 7.1 tutor-pedagogico

**Role:** Third pedagogical actor in AI-TPACK triad. Not a tool — an actor with its own pedagogical functions.
**TPACK Dimension:** AI-TPACK (full intersection)
**Pairing:** tutor-pedagogico-critic evaluates its work.

**Six functions:**
| Function | When | Framework | Output |
|---|---|---|---|
| F1: Diagnostic | Session start (if no profile) | ECD + Guided Inquiry | student-profile.md |
| F2: Phase briefing | Before each phase | Cognitive Apprenticeship | Adapted instructions per level |
| F3: Pedagogical translation | After critic feedback | Hattie + Shute | Verified/complemented feedback |
| F4: Comprehension checkpoint | Between phases | Nicol P2 + ICAP | Reflection questions, ICAP verification |
| F5: Fading decision | After phase completion | Cognitive Apprenticeship | Updated student-profile.md |
| F6: Teacher report | On demand (/tools progress --teacher) | Learning Analytics | Dashboard with alerts |

### 7.2 tutor-pedagogico-critic

**Role:** Evaluates pedagogical quality of the SYSTEM, not student work.
**TPACK Dimension:** AI-TPACK
**Separation of powers:** Never gives feedback to student. Only evaluates feedback from other agents.

**Evaluation protocol (5 dimensions, 20 points):**
- D1: Feedback quality (Hattie+Shute) — /5
- D2: Self-regulation fostering (Nicol) — /4
- D3: Appropriate scaffolding (Cognitive Apprenticeship) — /4
- D4: Evidence-based assessment (ECD) — /3
- D5: Interaction level (ICAP) — /4

**Classification:**
- 17-20: EXCELLENT
- 13-16: GOOD
- 9-12: INSUFFICIENT — recommend improvements
- 0-8: PEDAGOGICAL FAILURE — tutor-pedagogico intervenes directly

**Escalation:** 3 consecutive scores < 13 from same agent --> tutor-pedagogico takes over feedback, alerts teacher.

## 8. Modifications to Existing Agents

### 8.1 Universal Template

Every agent receives at end of its .md file:

```markdown
## Modo Tutor (TPACK)

**Activation:** Only when `mode: student` in CLAUDE.md.

**TPACK Dimension:** [specific to agent]
**Diagnostic Dimension:** [D1-D6]
**ECD Competency:** [C1-C6]

### Scaffolding by Level
[Principiante: MODELING instructions]
[Intermedio: COACHING instructions]  
[Avanzado: FADING instructions]

### Self-Assessment Pre-Delivery (Nicol P2)
[3 domain-specific questions]

### ICAP Minimum Interaction
[Principiante: Active mechanism]
[Intermedio: Constructive mechanism]
[Avanzado: Interactive mechanism]
```

For critic agents, add:
```markdown
### Formative Feedback (Hattie + Shute)
[Feed Up / Feed Back / Feed Forward format]

### ECD Assessment
[Specific evidences to evaluate]
```

### 8.2 Agent-Dimension Mapping

| Agent | Type | TPACK | Competency | Approx. Lines |
|---|---|---|---|---|
| librarian | Worker | TCK | C2 | ~50 |
| librarian-critic | Critic | TCK | C2 | ~40 |
| explorer | Worker | TCK | C2 | ~50 |
| explorer-critic | Critic | TCK | C2 | ~40 |
| data-engineer | Worker | TPK | C4 | ~45 |
| strategist | Worker | AI-TPACK | C3 | ~55 |
| strategist-critic | Critic | PCK | C3 | ~45 |
| coder | Worker | TPK | C4 | ~50 |
| coder-critic | Critic | TPK | C4 | ~40 |
| writer | Worker | PCK | C5 | ~55 |
| writer-critic | Critic | PCK | C5 | ~40 |
| storyteller | Worker | TPK | C6 | ~45 |
| storyteller-critic | Critic | TPK | C6 | ~40 |
| domain-referee | Referee | CK | C6 | ~35 |
| methods-referee | Referee | PCK | C3 | ~35 |
| editor | Infrastructure | AI-TPACK | C6 | ~40 |
| orchestrator | Infrastructure | AI-TPACK | -- | ~45 |
| verifier | Infrastructure | TK | -- | ~20 |

### 8.3 Orchestrator Flow (Student Mode)

```
1. PRE-PHASE:   tutor-pedagogico (F2: briefing)
2. WORKER:      agent with TPACK active + self-assessment
3. CRITIC:      agent with Feed Up/Back/Forward + ECD
4. POST:        tutor-pedagogico (F3: translation + F4: checkpoint)
5. QUALITY:     tutor-pedagogico-critic (pedagogical score >= 13)
6. FADING:      tutor-pedagogico (F5: update profile)
7. NEXT:        next phase per dependency graph
```

## 9. Integration Points

### 9.1 CLAUDE.md

New fields:
```markdown
**Mode:** student
**Student Level:** auto
```

### 9.2 quality_reports/student-profile.md

Generated by tutor-pedagogico diagnostic. Updated after each phase. Read by all agents in student mode.

### 9.3 /tools progress --teacher

tutor-pedagogico (F6) generates teacher dashboard using student-profile.md data + progress-protocol.md.

### 9.4 Worker-Critic Pairing (agents.md)

Add new pair:
| Worker | Critic | What's Reviewed |
|---|---|---|
| tutor-pedagogico | tutor-pedagogico-critic | Pedagogical quality of system feedback |

### 9.5 Escalation (agents.md)

Add pedagogical escalation: 3 consecutive pedagogical scores < 13 from same agent --> tutor-pedagogico intervenes.

## 10. What Does NOT Change

- Research pipeline logic (dependency graph, phase activation, quality gates)
- Score thresholds (80 commit, 90 PR, 95 submission)
- Worker-critic separation of powers
- Three-strikes escalation for research quality
- LaTeX format, code standards, bibliography validation
- Mode: teacher operates identically to current system

## 11. File Summary

### New files (5):
- `.claude/agents/tutor-pedagogico.md` (~200 lines)
- `.claude/agents/tutor-pedagogico-critic.md` (~120 lines)
- `.claude/references/tpack-pedagogical-framework.md` (~300 lines)
- `.claude/references/tpack-competency-model.md` (~150 lines)
- `.claude/references/tpack-diagnostic-rubric.md` (~200 lines)

### Modified files (20):
- 18 agent files (add ~40-55 lines each)
- `.claude/rules/agents.md` (add tutor-pedagogico pair + pedagogical escalation)
- `CLAUDE.md` (add Mode and Student Level fields)

### Estimated total new content: ~1,900 lines
