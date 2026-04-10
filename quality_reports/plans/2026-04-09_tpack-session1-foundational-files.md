# TPACK Session 1: Foundational Files — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Create the 5 foundational files for the TPACK agent redesign: 3 reference documents and 2 new agents (tutor-pedagogico + tutor-pedagogico-critic).

**Architecture:** Reference files live in `.claude/references/` (loaded on demand by agents). Agent files live in `.claude/agents/` (loaded when dispatched by orchestrator). All files are Markdown with no code dependencies. Each file is self-contained and can be created independently.

**Tech Stack:** Markdown documentation files following clo-author conventions.

**Spec:** `quality_reports/specs/2026-04-09_tpack-agent-redesign-design.md`

---

## File Structure

```
clo-author/.claude/
├── agents/
│   ├── tutor-pedagogico.md          # CREATE — pedagogical supervisor agent
│   └── tutor-pedagogico-critic.md   # CREATE — pedagogical quality evaluator
└── references/
    ├── tpack-pedagogical-framework.md   # CREATE — 5 layers operationalized
    ├── tpack-competency-model.md        # CREATE — ECD competencies, evidence, tasks
    └── tpack-diagnostic-rubric.md       # CREATE — scientific diagnostic rubric
```

**Responsibilities:**
- `tpack-pedagogical-framework.md` — Operationalizes the 5 pedagogical layers (Hattie+Shute, Nicol, Cognitive Apprenticeship, ECD, ICAP) into concrete instructions that agents read on demand
- `tpack-competency-model.md` — Defines the ECD model: 6 competencies, their evidences, and the tasks that produce those evidences
- `tpack-diagnostic-rubric.md` — The scientific rubric for the initial diagnostic interview (6 dimensions, 3 levels, observable indicators, adaptive questions)
- `tutor-pedagogico.md` — The supervisor agent with 6 functions (diagnostic, briefing, translation, checkpoint, fading, reporting)
- `tutor-pedagogico-critic.md` — The pedagogical quality critic (5-dimension evaluation protocol)

---

### Task 1: Create tpack-pedagogical-framework.md

**Files:**
- Create: `clo-author/.claude/references/tpack-pedagogical-framework.md`

- [ ] **Step 1: Write the complete pedagogical framework reference**

This file operationalizes all 5 pedagogical layers into concrete instructions that agents can follow. It is loaded on demand when agents operate in student mode.

```markdown
# TPACK Pedagogical Framework — Operational Reference

This file operationalizes 5 pedagogical frameworks into concrete instructions
for agents operating in student mode. Loaded on demand — not every session.

**When to load:** Any agent operating in `mode: student` that needs detailed
guidance on applying the pedagogical layers. The TPACK section in each agent
contains the essentials; this file provides the full framework when needed.

---

## Layer 1: Structured Feedback (Hattie & Timperley, 2007 + Shute, 2008)

### Theoretical Foundation

Hattie & Timperley (2007) identify three questions that effective feedback answers:
1. **Feed Up:** Where am I going? (learning goal)
2. **Feed Back:** How am I going? (current status vs. goal)
3. **Feed Forward:** Where to next? (action to close the gap)

Shute (2008) adds that effective feedback must be:
- **Specific:** Target exact behaviors, not vague impressions
- **Timely:** During the process, not only at the end
- **Task-oriented:** Comment on the WORK, never on the student as a person
- **Elaborative:** Include the WHY, not just the WHAT
- **Manageable:** Maximum 3 priority gaps per round (avoid cognitive overload)
- **Non-evaluative in tone:** Frame as information for improvement, not judgment

### Operational Protocol for Critic Agents

Every feedback response in student mode MUST follow this structure:

```
### Feed Up
"Your learning objective in this phase is: [observable verb + content].
Success criteria:
1. [Specific criterion]
2. [Specific criterion]
3. [Specific criterion]"

### Feed Back

**Strengths (always first):**
- [Genuine strength]: [WHY this is good — what principle it demonstrates]
- [Genuine strength]: [WHY this is good]

**Priority Gaps (maximum 3):**

1. **[Gap title]**
   - What you did: [exact quote or description from student's work]
   - The problem: [what's wrong]
   - Why it matters: [consequence for the research if uncorrected]
   - If uncorrected: [what happens to validity/credibility/results]

2. **[Gap title]**
   [Same structure]

3. **[Gap title]**
   [Same structure]

**Additional gaps (for later):**
[List remaining gaps briefly — student addresses these after mastering
the priority 3]

### Feed Forward

For each priority gap:
1. **Action:** [Specific, concrete step the student should take]
   - If Principiante: [Include worked example showing correct approach]
   - If Intermedio: [Point to specific resource — chapter, paper, section]
   - If Avanzado: [Direction only — "consider X approach"]
```

### Language Adaptation by Level

| Level | Technical Vocabulary | Explanations | Examples |
|---|---|---|---|
| Principiante | Avoid jargon. When unavoidable, define inline: "parallel trends (the assumption that treatment and control groups would have followed the same trajectory without the intervention)" | Full explanations of every concept | Include worked example for every gap |
| Intermedio | Use jargon with brief parenthetical: "parallel trends (same trajectory assumption)" | Explain non-obvious concepts | Reference resources, not full examples |
| Avanzado | Free jargon | Only explain if concept is unusual for the field | Direction only |

### Anti-Patterns (What NOT to Do)

- "Your work needs improvement" — vague, not specific (Shute: specificity)
- "This is wrong" without WHY — evaluative, not elaborative
- Listing 8 problems at once — overwhelming (Shute: manageable)
- "Good job!" without specifying WHAT was good — empty praise
- Commenting on student intelligence or effort — task-oriented only
- Giving feedback only at the end — timely means DURING the process

---

## Layer 2: Self-Regulation (Nicol & Macfarlane-Dick, 2006)

### Theoretical Foundation

Seven principles of good feedback that foster self-regulated learning:

| # | Principle | Purpose |
|---|---|---|
| P1 | Clarify what good performance is | Student knows the target BEFORE working |
| P2 | Facilitate self-assessment | Student monitors own progress against criteria |
| P3 | Deliver high-quality information | Feedback is specific, timely, actionable |
| P4 | Encourage dialogue | Student can question, discuss, disagree |
| P5 | Encourage positive motivation | Build confidence through genuine strengths |
| P6 | Provide opportunities to close the gap | Concrete actions, not just identification of problems |
| P7 | Use feedback to improve teaching | Inform the teacher about what's working and what's not |

### Operational Protocol

#### P1: Clarify Criteria (Worker agents, before student works)

```
Before you begin, here are the criteria your work will be evaluated against:

1. [Criterion from the critic's rubric, in student-friendly language]
2. [Criterion]
3. [Criterion]

These criteria come from [source: academic standards / journal requirements /
methodological best practices]. Understanding them before you start will help
you produce better work on the first attempt.
```

#### P2: Self-Assessment (Worker agents, before sending to critic)

```
Before I send your work for review, evaluate it yourself:

1. [Domain-specific question about criterion 1] — Do you meet it? Why?
2. [Domain-specific question about criterion 2] — Do you meet it? Why?
3. [Domain-specific question about criterion 3] — Do you meet it? Why?

What part of your work are you least confident about?
```

The critic RECEIVES the student's self-assessment and:
- Compares self-assessment to own evaluation
- Where they MATCH: "You correctly identified that [X] — good self-awareness"
- Where they DIFFER: "You rated [X] as adequate, but [specific evidence shows gap]. This difference is a learning opportunity — here's why..."

#### P4: Encourage Dialogue (All agents, after feedback)

```
Before you start revising:
- Is there any part of this feedback you don't understand?
- Is there anything you disagree with? (Disagreement is valuable —
  explain your reasoning and we can discuss)
- Do you need more detail on any of the suggested actions?
```

NEVER skip this step. Student silence is not agreement — it may be confusion.

#### P7: Inform Teacher (tutor-pedagogico only)

Generate reports for `/tools progress --teacher` that include:
- Self-assessment accuracy (how well student predicts own gaps)
- Dialogue patterns (does student ask questions or stay silent?)
- Gap closure rate (does feedback lead to improvement?)
- Recurring gaps (same issue appearing across phases)

---

## Layer 3: Disciplinary Scaffolding (Collins, Brown & Newman, 1989 + Kuhlthau et al., 2007)

### Theoretical Foundation

**Cognitive Apprenticeship** (Collins et al., 1989) adapts traditional apprenticeship
to cognitive skills. Six teaching methods, of which we use four:

| Method | Description | When |
|---|---|---|
| **Modeling** | Expert demonstrates complete process, making thinking visible | Principiante — student has never done this |
| **Coaching** | Expert observes student attempting task, offers guidance | Intermedio — student attempts with support |
| **Scaffolding** | Expert provides structure that student fills in | Intermedio — student has partial competence |
| **Fading** | Expert gradually withdraws support | Avanzado — student demonstrates competence |

Two additional methods (articulation, reflection) are embedded in ICAP checkpoints.

**Guided Inquiry** (Kuhlthau, Maniotes & Caspari, 2007) structures the inquiry
process through 6 phases that map to the clo-author pipeline:

| Guided Inquiry Phase | clo-author Phase | Guiding Question |
|---|---|---|
| Open | /discover interview | What do you know? What intrigues you? |
| Immerse | /discover lit | What patterns emerge from the literature? |
| Explore | /discover data + /strategize | What data would answer your question? Why? |
| Identify | /strategize | What is your central argument? What evidence supports it? |
| Gather | /analyze | Do results support your argument? What surprises you? |
| Create | /write + /talk | How would you explain your findings to a non-expert? |

### Operational Protocol for Worker Agents

#### MODELING (Principiante)

```
1. BEFORE asking the student to work:
   a. Explain WHAT this phase is and WHY it matters for research
   b. Show a COMPLETE worked example using a DIFFERENT topic
      (never the student's own topic — they must transfer, not copy)
   c. Narrate EVERY decision in the example:
      "I chose [X] because [reason]. I did NOT choose [Y] because [reason]."
   d. Make thinking VISIBLE — explain the reasoning, not just the steps

2. THEN use Guided Inquiry to help the student discover:
   a. Ask open-ended questions that lead to understanding:
      "What terms would you use to search for your topic? Why those?"
   b. Do NOT give answers directly — guide toward discovery
   c. If student is stuck after 2 attempts, provide a hint, not the answer
   d. If stuck after hint, model ONE step with student's topic, then
      ask them to continue

3. NEVER write the complete artifact for the student
   The student must produce the work; you guide the process
```

#### COACHING (Intermedio)

```
1. Provide STRUCTURE (template, checklist, outline) for the task
2. Student EXECUTES within the structure
3. Coach DURING execution with probing questions:
   "Why did you choose [X]? What alternatives did you consider?"
   "What assumption are you making here? Is it testable?"
4. Intervene ONLY when student deviates significantly from good practice
5. Celebrate good decisions: "That was a strong choice because [reason]"
```

#### SCAFFOLDING (Intermedio, more structured)

```
1. Provide a PARTIAL solution that the student completes:
   - Template with [COMPLETE THIS] sections
   - Skeleton code with key functions defined but body empty
   - Outline with topic sentences written, paragraphs to fill
2. Student COMPLETES and JUSTIFIES each decision
3. Review completions, focus on justifications
```

#### FADING (Avanzado)

```
1. Give the instruction without additional structure:
   "Design your identification strategy. Specify assumptions,
   threats, and robustness checks."
2. Student executes AUTONOMOUSLY
3. Review at the END with standard feedback
4. Intervene ONLY if there is a serious conceptual error
```

### Fading Transition Criteria

| Transition | ALL criteria must be met |
|---|---|
| Principiante --> Intermedio | Artifact score >= 75 AND comprehension checkpoint >= 2/3 AND ICAP level >= Active AND 2/3 ECD evidences demonstrated |
| Intermedio --> Avanzado | Artifact score >= 85 AND comprehension 3/3 AND ICAP >= Constructive AND 3/3 ECD evidences AND 2 consecutive improving phases |

---

## Layer 4: Evidence-Based Assessment (Mislevy, Steinberg & Almond, 2003)

### Theoretical Foundation

Evidence-Centered Design (ECD) separates three concerns:
1. **Competency Model:** What can the student do? (latent traits)
2. **Evidence Model:** What observable behaviors demonstrate competency?
3. **Task Model:** What tasks elicit those behaviors?

This separation prevents the common error of equating "artifact quality" with
"student learning." A student can produce a good artifact by copying; ECD
checks whether the student DEMONSTRATES the underlying competency.

### Operational Protocol

See `tpack-competency-model.md` for the complete competency-evidence-task mapping.

**For critic agents:**

After producing the standard artifact score, evaluate EACH evidence:

```
## ECD Assessment

| Evidence | Demonstrated? | Detail |
|---|---|---|
| E[x].1: [description] | YES / PARTIAL / NO | [what specifically was observed or missing] |
| E[x].2: [description] | YES / PARTIAL / NO | [detail] |
| E[x].3: [description] | YES / PARTIAL / NO | [detail] |

**Competency C[x] status:**
- All YES: DEMONSTRATED
- Any PARTIAL: DEVELOPING — [specify what's missing]
- Any NO: NOT DEMONSTRATED — [specify what's missing]
```

**Key principle:** An artifact can score 85/100 but if a critical evidence
is NOT demonstrated, the competency is NOT achieved. Scores measure product
quality; ECD measures learning.

Register results in `quality_reports/student-profile.md`.

---

## Layer 5: Interaction Design (Chi & Wylie, 2014)

### Theoretical Foundation

ICAP framework classifies learning activities by cognitive engagement:

| Level | Student Behavior | Cognitive Process | Learning Outcome |
|---|---|---|---|
| **Passive** | Receives without responding | Storage | Minimal — may not even store |
| **Active** | Manipulates, repeats, copies | Activation of existing knowledge | Low — rehearsal without integration |
| **Constructive** | Generates new output beyond input | Integration of new + existing knowledge | High — creates new understanding |
| **Interactive** | Co-constructs with another agent | Joint integration + negotiation | Maximum — deepest processing |

The ICAP hypothesis: Interactive > Constructive > Active > Passive for learning.

### Operational Protocol

#### Minimum ICAP Level by Student Level

| Student Level | Minimum ICAP | What This Means |
|---|---|---|
| Principiante | **Active** | Student must DO something with the feedback — correct AND explain |
| Intermedio | **Constructive** | Student must GENERATE beyond the feedback — justify, anticipate, propose |
| Avanzado | **Interactive** | Student must CO-CONSTRUCT — debate, defend, negotiate meaning |

#### Enforcement Mechanisms

**Active (Principiante):**
```
After delivering feedback:
"Make the corrections and explain in 2-3 sentences:
what did you change and why was the change necessary?"

If student only corrects without explaining:
"I see you corrected [X]. Can you explain WHY it was necessary?
What problem did it cause in your research?"
```

**Constructive (Intermedio):**
```
Before correcting, respond to these questions:
1. Why do you think [this] is a problem in your work?
2. What would happen to your conclusions if you didn't fix it?
3. Is there a different way to address this issue?

You MUST respond before proceeding with corrections.
```

**Interactive (Avanzado):**
```
"I disagree with your choice of [X]. My argument is: [genuine
counterargument based on methodology/theory]. Can you defend
your decision or propose an alternative?"

If student accepts without defending:
"You accepted my objection very quickly. Are you sure? What
evidence supports your original decision? Push back if you
think I'm wrong — that's how academic discourse works."
```

#### What Agents Must NOT Do

- Proceed automatically after feedback without student response (kills ICAP)
- Accept a one-word response ("ok", "done") as meeting Active threshold
- Skip the ICAP interaction because "the student already fixed it"
- Lower the ICAP threshold because "we're running out of time"

#### Maximum Attempts

If student cannot reach minimum ICAP level after 2 attempts:
1. Register as "needs reinforcement" in student-profile.md
2. Provide the explanation the student couldn't generate
3. Continue to next step (do NOT block indefinitely)
4. Flag for tutor-pedagogico to design a reinforcement activity

---

## Cross-Layer Integration

The 5 layers are not independent — they reinforce each other:

| Integration | How |
|---|---|
| L1 + L2 | Feed Up = P1 (clarify criteria). Self-assessment (P2) happens before Feed Back. |
| L1 + L3 | Feed Forward adapts to scaffolding level (example for Modeling, resource for Coaching, direction for Fading) |
| L1 + L4 | Feed Back evaluates both artifact quality AND ECD evidences |
| L2 + L5 | Self-assessment (P2) IS an ICAP-Active interaction at minimum |
| L3 + L5 | Modeling phase uses Guided Inquiry questions = ICAP-Active. Coaching uses probing questions = ICAP-Constructive. |
| L4 + L3 | ECD evidence assessment informs fading decisions |
```

- [ ] **Step 2: Verify the file was created correctly**

Run: `wc -l clo-author/.claude/references/tpack-pedagogical-framework.md`
Expected: approximately 280-310 lines.

- [ ] **Step 3: Commit**

```bash
cd clo-author
git add .claude/references/tpack-pedagogical-framework.md
git commit -m "feat(tpack): add pedagogical framework reference — 5 layers operationalized

Hattie+Shute feedback, Nicol self-regulation, Cognitive Apprenticeship
scaffolding, ECD assessment, ICAP interaction design. Loaded on demand
by agents in student mode.

Co-Authored-By: Claude Opus 4.6 (1M context) <noreply@anthropic.com>"
```

---

### Task 2: Create tpack-competency-model.md

**Files:**
- Create: `clo-author/.claude/references/tpack-competency-model.md`

- [ ] **Step 1: Write the ECD competency model**

```markdown
# TPACK Competency Model — Evidence-Centered Design

This file defines the competency-evidence-task model for evaluating student
learning across the research pipeline. Based on Evidence-Centered Design
(Mislevy, Steinberg & Almond, 2003).

**When to load:** Agents in student mode evaluating competency demonstration.
tutor-pedagogico uses this for diagnostic and fading decisions.

---

## Design Principle

```
COMPETENCY (what we want to measure — latent, not directly observable)
    --> EVIDENCE (observable behavior that demonstrates the competency)
        --> TASK (what the student does to produce the evidence)
```

Artifact quality (score) and competency demonstration are INDEPENDENT.
A student can produce a high-scoring artifact without demonstrating
the competency (e.g., by following instructions mechanically).
A student can demonstrate competency on a lower-scoring artifact
(e.g., good reasoning with imperfect execution).

---

## Competency C1: Formulates Researchable Problems

**TPACK Dimension:** CK (Content Knowledge)
**Diagnostic Dimension:** D1
**Pipeline Phase:** /discover interview
**Agent Pair:** (tutor-pedagogico conducts; no separate worker for formulation)

### Evidences

| Evidence | Observable Indicator | Level Required |
|---|---|---|
| E1.1: Delimited question | Question specifies population, variable(s), and context. Not a topic — a question. | Principiante: with guidance. Intermedio: independently. Avanzado: with theoretical grounding. |
| E1.2: Justified relevance | Explains WHY this question matters, citing literature or empirical evidence of the problem. | Principiante: can state importance. Intermedio: cites evidence. Avanzado: positions within field debates. |
| E1.3: Feasible scope | Question is answerable with available methods and data within realistic constraints. | Principiante: acknowledges constraints. Intermedio: adjusts scope to constraints. Avanzado: identifies trade-offs explicitly. |

### Assessment Criteria

| Level | E1.1 Looks Like | E1.2 Looks Like | E1.3 Looks Like |
|---|---|---|---|
| NOT demonstrated | "I want to study AI in education" (topic, not question) | "It's important because AI is trending" (no evidence) | Scope impossible given constraints (entire country, 6 months) |
| PARTIAL | "How does AI affect learning?" (question but undelimited) | "Studies show AI can help (Smith, 2020)" (one citation, no depth) | Feasible but constraints not explicitly discussed |
| DEMONSTRATED | "How does an AI tutoring ecosystem based on AI-TPACK affect research competencies in graduate students at [institution]?" | "Graduate programs face increasing student-advisor ratios (De Kleijn et al., 2012), creating a supervision gap that affects thesis quality (Pyhaltto et al., 2015)" | "15-20 students, 1 semester, mixed methods — consistent with DBR pilot standards (McKenney & Reeves, 2012)" |

---

## Competency C2: Evaluates Literature Critically

**TPACK Dimension:** TCK (Technology + Content)
**Diagnostic Dimension:** D2
**Pipeline Phase:** /discover lit
**Agent Pair:** librarian + librarian-critic

### Evidences

| Evidence | Observable Indicator | Level Required |
|---|---|---|
| E2.1: Identifies research gaps | Points to specific questions not yet answered, populations not studied, methods not applied — with evidence. | Principiante: identifies gaps with guidance. Intermedio: identifies independently. Avanzado: distinguishes genuine gaps from search limitations. |
| E2.2: Distinguishes source quality | Differentiates peer-reviewed from grey literature, seminal from peripheral, high-impact from predatory. | Principiante: knows peer-review exists. Intermedio: applies quality criteria. Avanzado: evaluates methodological rigor within sources. |
| E2.3: Synthesizes, not summarizes | Organizes literature by themes/arguments/debates, not chronologically or by author. Identifies patterns and contradictions. | Principiante: can group by topic. Intermedio: identifies themes and contradictions. Avanzado: constructs narrative positioning own research. |

### Assessment Criteria

| Level | E2.1 | E2.2 | E2.3 |
|---|---|---|---|
| NOT demonstrated | "There are few studies on this topic" (assertion without evidence) | Cites blog posts and Wikipedia alongside journals | Lists papers chronologically: "Smith (2018) found X. Jones (2019) found Y." |
| PARTIAL | "No studies have examined [X] in [context]" (specific but not verified against literature) | Uses peer-reviewed sources but doesn't evaluate methodology | Groups by topic but doesn't connect themes or identify contradictions |
| DEMONSTRATED | "While [X] has been studied in [contexts A, B] (refs), no study has examined [specific gap] in [specific context], despite evidence that [why this context matters]" | Evaluates sources: "While Smith (2020) reports [X], the sample (N=12) limits generalizability" | "Three perspectives emerge: [theme 1] (refs), [theme 2] (refs), and a tension between them regarding [specific point]" |

---

## Competency C3: Designs Empirical Strategy

**TPACK Dimension:** PCK (Pedagogy + Content) / AI-TPACK for full intersection
**Diagnostic Dimension:** D3
**Pipeline Phase:** /strategize
**Agent Pair:** strategist + strategist-critic

### Evidences

| Evidence | Observable Indicator | Level Required |
|---|---|---|
| E3.1: Specifies and defends assumptions | States each assumption required by the method AND provides argument for why it's credible in this context. | Principiante: can name assumptions with help. Intermedio: states and argues. Avanzado: provides empirical evidence for plausibility. |
| E3.2: Anticipates objections | Identifies what a skeptical reviewer would question and prepares responses. | Principiante: acknowledges limitations exist. Intermedio: lists specific threats. Avanzado: proposes tests for each threat. |
| E3.3: Proposes robustness checks | Designs alternative specifications that test sensitivity of results to methodological choices. | Principiante: understands what robustness means. Intermedio: proposes relevant checks. Avanzado: justifies each check and predicts expected results. |

### Assessment Criteria

| Level | E3.1 | E3.2 | E3.3 |
|---|---|---|---|
| NOT demonstrated | Cannot name the assumptions of chosen method | "There may be some limitations" (vague) | No robustness checks proposed |
| PARTIAL | "DiD assumes parallel trends" (names but doesn't defend) | "Selection bias is a concern" (names threat but no response) | "We could try different controls" (vague) |
| DEMONSTRATED | "Parallel trends requires that [treatment/control] would have followed the same trajectory absent treatment. This is credible because [specific evidence]: pre-treatment trends are parallel for [N] years (Figure X)" | "A reviewer might argue that [specific confounder] drives our results. We address this by [specific test/control]. If [confounder] were driving results, we would expect [pattern] — we test this in Table X" | "Robustness: (1) add [controls] — expect stable point estimate if identification is valid; (2) placebo test at [fake date] — expect null; (3) [alternative estimator] — expect similar magnitude" |

---

## Competency C4: Implements Analysis

**TPACK Dimension:** TPK (Technology + Pedagogy)
**Diagnostic Dimension:** D4
**Pipeline Phase:** /analyze
**Agent Pair:** coder + coder-critic (+ data-engineer for pipeline)

### Evidences

| Evidence | Observable Indicator | Level Required |
|---|---|---|
| E4.1: Code-strategy alignment | Code implements EXACTLY what the strategy memo specifies — same estimator, fixed effects, clustering, sample restrictions. | Principiante: implements with guidance. Intermedio: implements independently. Avanzado: makes justified implementation decisions. |
| E4.2: Results pass sanity checks | Sign is expected, magnitude is plausible, dynamics make sense, results are consistent across specifications. | Principiante: can check with checklist. Intermedio: identifies anomalies. Avanzado: explains anomalies with theory. |
| E4.3: Can explain the code | Student can describe what each section of the script does, WHY it does it, and how it connects to the methodology. | Principiante: can describe steps. Intermedio: can explain WHY. Avanzado: can justify implementation choices. |

---

## Competency C5: Writes Academically

**TPACK Dimension:** PCK (Pedagogy + Content)
**Diagnostic Dimension:** D5
**Pipeline Phase:** /write
**Agent Pair:** writer + writer-critic

### Evidences

| Evidence | Observable Indicator | Level Required |
|---|---|---|
| E5.1: Clear contribution | Contribution is explicit within first 2 pages, stating what's new and why it matters. | Principiante: states topic. Intermedio: states contribution. Avanzado: positions contribution within field debates. |
| E5.2: Evidence-backed claims | Every causal or evaluative claim has corresponding evidence (data, citation, logical argument). | Principiante: makes claims with some evidence. Intermedio: most claims backed. Avanzado: no unbacked claims, clear evidence hierarchy. |
| E5.3: Professional academic voice | No hedging, no AI-generated language patterns, appropriate register, consistent notation. | Principiante: writes clearly but informally. Intermedio: academic register with occasional hedging. Avanzado: clean professional voice. |

---

## Competency C6: Communicates Findings

**TPACK Dimension:** TPK (Technology + Pedagogy)
**Diagnostic Dimension:** D6
**Pipeline Phase:** /talk + /review
**Agent Pair:** storyteller + storyteller-critic (+ editor for peer review)

### Evidences

| Evidence | Observable Indicator | Level Required |
|---|---|---|
| E6.1: Coherent narrative | Presentation follows logical arc: hook --> problem --> method --> results --> implication. Audience can follow without reading the paper. | Principiante: presents information. Intermedio: constructs narrative. Avanzado: engages audience. |
| E6.2: Effective visualizations | Figures and tables are self-explanatory, properly labeled, and support the argument. | Principiante: includes relevant figures. Intermedio: figures are clear and labeled. Avanzado: figures tell the story independently. |
| E6.3: Defends under questioning | Can respond to critical questions about methodology, data, and interpretation without reading notes. | Principiante: answers basic questions. Intermedio: handles methodology questions. Avanzado: engages in substantive debate. |

---

## Cross-Competency Dependencies

```
C1 (Problem) --> C2 (Literature) --> C3 (Strategy) --> C4 (Analysis)
                                                            |
                                                            v
                                          C5 (Writing) <----+
                                                            |
                                                            v
                                          C6 (Communication)
```

A student cannot meaningfully demonstrate C3 without at least PARTIAL
demonstration of C1 and C2. The orchestrator should check prerequisite
competencies before advancing phases.

---

## Using This Model

**Critic agents:** After scoring the artifact, evaluate each evidence for
the competency associated with your phase. Record in student-profile.md.

**tutor-pedagogico:** Use evidence status to make fading decisions.
All evidences DEMONSTRATED = competency achieved = eligible for level-up.

**tutor-pedagogico-critic:** Verify that critics are evaluating evidences,
not just scoring artifacts.

**/tools progress:** Report competency status alongside phase scores.
```

- [ ] **Step 2: Verify the file was created correctly**

Run: `wc -l clo-author/.claude/references/tpack-competency-model.md`
Expected: approximately 180-200 lines.

- [ ] **Step 3: Commit**

```bash
cd clo-author
git add .claude/references/tpack-competency-model.md
git commit -m "feat(tpack): add ECD competency model — 6 competencies with evidence mapping

Defines competencies C1-C6, their observable evidences, assessment criteria
by level, and cross-competency dependencies. Based on Evidence-Centered
Design (Mislevy et al., 2003).

Co-Authored-By: Claude Opus 4.6 (1M context) <noreply@anthropic.com>"
```

---

### Task 3: Create tpack-diagnostic-rubric.md

**Files:**
- Create: `clo-author/.claude/references/tpack-diagnostic-rubric.md`

- [ ] **Step 1: Write the diagnostic rubric**

```markdown
# TPACK Diagnostic Rubric — Initial Student Assessment

Scientific rubric for the initial diagnostic interview conducted by
tutor-pedagogico. Based on Evidence-Centered Design (Mislevy et al., 2003),
competency indicators from Meerah & Arsad (2010), and academic literacy
frameworks from Carlino (2013).

**When to load:** tutor-pedagogico at session start when no student-profile.md
exists or when re-diagnosis is requested.

---

## Diagnostic Method

**Type:** Semi-structured adaptive interview using Guided Inquiry
(Kuhlthau, Maniotes & Caspari, 2007).

**Duration:** 6-8 questions, adaptive — each response determines the depth
of the next question.

**Principle:** The diagnostic is itself a learning moment. The tutor does
not just classify — it helps the student articulate their starting point.

---

## Six Diagnostic Dimensions

### D1: Problem Formulation (CK)

**What it measures:** Can the student articulate a researchable question
with clear contribution?

**Question sequence:**

```
Q1: "Describe your research topic in 2-3 sentences. What specific
question do you want to answer?"

Classify response:

IF vague topic without question ("I want to study AI in education"):
  --> Level: Principiante
  --> Follow-up: "What specific aspect of AI in education interests
      you? Is there a problem you've observed that you want to solve?"

IF question exists but undelimited ("How does AI affect learning?"):
  --> Level: Intermedio
  --> Follow-up: "Good question. Now let's sharpen it: WHO are you
      studying? WHERE? WHAT specific outcome are you measuring?"

IF delimited question with population and context:
  --> Level: Avanzado
  --> Follow-up: "Strong formulation. What makes YOUR study different
      from existing work on this topic?"
```

**Observable indicators by level:**

| Level | Indicator |
|---|---|
| Principiante | States a topic or area of interest. Cannot formulate a specific question without guidance. Uses everyday language, not research vocabulary. |
| Intermedio | Formulates a question but it's too broad, lacks population/context, or is not empirically testable. Uses some research vocabulary. |
| Avanzado | Formulates a delimited, testable question with clear population, context, and variables. Positions it relative to existing work. |

---

### D2: Literature Mastery (TCK)

**What it measures:** Can the student search, evaluate, and synthesize
academic sources?

**Question sequence:**

```
Q2: "Have you done any literature search on your topic? Which databases
did you use? How many relevant articles have you found?"

Classify response:

IF no search or only Google/Wikipedia:
  --> Level: Principiante
  --> Follow-up: "Have you heard of databases like Scopus, Web of
      Science, or Google Scholar? What do you think makes an academic
      source different from a web article?"

IF Google Scholar with some articles but no systematic approach:
  --> Level: Intermedio
  --> Follow-up: "Good start. How did you decide which articles to
      include? What criteria did you use for relevance and quality?"

IF systematic search in multiple databases with quality criteria:
  --> Level: Avanzado
  --> Follow-up: "What patterns have you found in the literature?
      What gaps or contradictions have you identified?"
```

**Observable indicators by level:**

| Level | Indicator |
|---|---|
| Principiante | Has not searched or only used Google. Cannot distinguish peer-reviewed from non-academic sources. Does not know academic databases. |
| Intermedio | Has used Google Scholar or one database. Found some articles but selection is unsystematic. Can identify peer-reviewed sources but doesn't evaluate methodology. |
| Avanzado | Systematic search across multiple databases (Scopus, WoS, field-specific). Applies quality criteria. Can synthesize themes and identify gaps. |

---

### D3: Methodological Design (PCK)

**What it measures:** Does the student understand research methods and
their assumptions?

**Question sequence:**

```
Q3: "How are you planning to answer your research question?
What method or approach would you use?"

Classify response:

IF cannot articulate a method or confuses methods with tools
("I'll use a survey" without connecting to research question):
  --> Level: Principiante
  --> Follow-up: "When we choose a research method, we need to think
      about what kind of evidence would answer our question. Is your
      question about describing something, explaining a relationship,
      or testing whether something works?"

IF names a method but cannot explain its assumptions or justify choice:
  --> Level: Intermedio
  --> Follow-up: "Good choice. Why [method] and not [alternative]?
      What does [method] assume about your data or context?"

IF names method, explains assumptions, and justifies choice:
  --> Level: Avanzado
  --> Follow-up: "What would a skeptic say is the biggest weakness
      of your approach? How would you respond?"
```

**Observable indicators by level:**

| Level | Indicator |
|---|---|
| Principiante | Cannot name a method. Confuses tools (survey, interview) with methods (experimental, quasi-experimental, ethnographic). Does not understand the concept of assumptions. |
| Intermedio | Names an appropriate method. Understands basic differences between quantitative/qualitative/mixed. Cannot articulate assumptions or defend choice against alternatives. |
| Avanzado | Names method, explains its assumptions in context, justifies over alternatives, and identifies threats to validity. |

---

### D4: Analytical Competence (TPK)

**What it measures:** Can the student implement, interpret, and verify
analysis using computational tools?

**Question sequence:**

```
Q4: "Have you used any software for data analysis? (R, Python, Stata,
SPSS, Excel, etc.) What have you done with it?"

Classify response:

IF no experience or only Excel for basic calculations:
  --> Level: Principiante
  --> Follow-up: "That's fine — we'll learn together. Have you ever
      written any code, even simple scripts? What's your comfort
      level with learning a programming language?"

IF basic experience with one tool (SPSS point-and-click, basic R):
  --> Level: Intermedio
  --> Follow-up: "When you run an analysis, how do you know if the
      results make sense? What checks do you do?"

IF comfortable writing scripts, can interpret output, checks results:
  --> Level: Avanzado
  --> Follow-up: "If someone else ran your code with the same data,
      would they get exactly the same results? How do you ensure that?"
```

**Observable indicators by level:**

| Level | Indicator |
|---|---|
| Principiante | No coding experience or only spreadsheets. Cannot write scripts. Does not understand reproducibility. |
| Intermedio | Basic experience with one tool. Can run pre-written scripts. Limited ability to interpret output or check for errors. |
| Avanzado | Comfortable writing scripts from scratch. Interprets output critically. Understands reproducibility (seeds, versioning, relative paths). |

---

### D5: Academic Writing (PCK)

**What it measures:** Can the student construct evidence-based arguments
in academic register?

**Question sequence:**

```
Q5: "Have you written academic papers or reports before? What was the
longest piece of academic writing you've produced?"

Classify response:

IF only class essays or no academic writing:
  --> Level: Principiante
  --> Follow-up: "What do you think makes academic writing different
      from a blog post or an essay? What have you found most
      difficult about writing for an academic audience?"

IF has written reports/thesis chapters but struggles with structure:
  --> Level: Intermedio
  --> Follow-up: "When you write a section, how do you decide what
      goes first? How do you connect your claims to evidence?"

IF has published or produced polished academic manuscripts:
  --> Level: Avanzado
  --> Follow-up: "How do you handle reviewer feedback on your writing?
      What's your revision process?"
```

**Observable indicators by level:**

| Level | Indicator |
|---|---|
| Principiante | Only informal or essay-style writing. No experience with academic structure (IMRaD or equivalent). Uses hedging heavily or writes too informally. |
| Intermedio | Has written academic reports. Understands basic structure but struggles with contribution framing, evidence-claim alignment, or consistent notation. |
| Avanzado | Has produced polished academic manuscripts. Clear structure, evidence-backed claims, professional voice. Familiar with revision and peer feedback. |

---

### D6: Scientific Communication (TPK)

**What it measures:** Can the student present and defend findings to a
critical audience?

**Question sequence:**

```
Q6: "Have you presented research in a seminar, conference, or class?
How did it go? Were there tough questions?"

Classify response:

IF never presented research:
  --> Level: Principiante
  --> Follow-up: "Have you ever presented anything (class project,
      work report)? What makes you most nervous about presenting
      to an academic audience?"

IF has presented but struggled with questions or structure:
  --> Level: Intermedio
  --> Follow-up: "When someone asks a tough question about your
      methodology, how do you typically respond? Do you find it
      harder to present methods or results?"

IF has presented confidently and handled critical questions:
  --> Level: Avanzado
  --> Follow-up: "How do you prepare for hostile questions?
      Do you anticipate objections in advance?"
```

**Observable indicators by level:**

| Level | Indicator |
|---|---|
| Principiante | No experience presenting research. Anxious about academic audiences. Cannot structure a presentation narrative. |
| Intermedio | Has presented but struggles with methodology questions, time management, or narrative arc. Can present results but not defend them. |
| Avanzado | Presents confidently. Handles critical questions. Prepares for objections. Adapts to audience level. |

---

## Profile Generation Protocol

After completing the diagnostic, tutor-pedagogico generates:

```markdown
# Student TPACK Profile
**Generated:** [date]
**Updated:** [date]
**Overall Level:** [mode of 6 dimensions]

## Competency Map

| Dimension | Level | Evidence | TPACK | Scaffolding Mode |
|---|---|---|---|---|
| D1: Problem Formulation | [level] | [key quote from diagnostic] | CK | [Modeling/Coaching/Fading] |
| D2: Literature Mastery | [level] | [key quote] | TCK | [mode] |
| D3: Methodological Design | [level] | [key quote] | PCK | [mode] |
| D4: Analytical Competence | [level] | [key quote] | TPK | [mode] |
| D5: Academic Writing | [level] | [key quote] | PCK | [mode] |
| D6: Scientific Communication | [level] | [key quote] | TPK | [mode] |

## Scaffolding Strategy
- Phases requiring MODELING: [list]
- Phases requiring COACHING: [list]
- Phases requiring FADING: [list]

## Fading Criteria
[From tpack-pedagogical-framework.md Layer 3]
```

**Present to student:** "Based on our conversation, this is your research
profile. Does it reflect where you are? If not, tell me what feels wrong
— I want this to be accurate, not flattering."

---

## Re-Diagnosis

Trigger re-diagnosis when:
- Student requests it
- tutor-pedagogico detects significant discrepancy between profile and performance
  (e.g., profile says Intermedio but student consistently fails Principiante-level tasks)
- Teacher requests it via /tools progress --teacher
- After a long break (> 30 days since last session)
```

- [ ] **Step 2: Verify file created correctly**

Run: `wc -l clo-author/.claude/references/tpack-diagnostic-rubric.md`
Expected: approximately 200-220 lines.

- [ ] **Step 3: Commit**

```bash
cd clo-author
git add .claude/references/tpack-diagnostic-rubric.md
git commit -m "feat(tpack): add diagnostic rubric — 6 dimensions with adaptive interview protocol

Scientific rubric based on ECD (Mislevy et al., 2003), research competency
indicators (Meerah & Arsad, 2010), and academic literacy (Carlino, 2013).
Semi-structured adaptive interview with observable indicators by level.

Co-Authored-By: Claude Opus 4.6 (1M context) <noreply@anthropic.com>"
```

---

### Task 4: Create tutor-pedagogico.md agent

**Files:**
- Create: `clo-author/.claude/agents/tutor-pedagogico.md`

- [ ] **Step 1: Write the tutor-pedagogico agent definition**

```markdown
# tutor-pedagogico — Pedagogical Supervisor Agent

You are the **tutor-pedagogico**, the third pedagogical actor in the AI-TPACK
triad (student-IA-teacher). You are not a tool that the student uses — you
are an actor with your own pedagogical functions that mediates and enriches
the formative relationship without replacing the teacher's expert judgment.

**TPACK Dimension:** AI-TPACK (full intersection)
**Paired Critic:** tutor-pedagogico-critic
**Activation:** Only when `mode: student` in CLAUDE.md

---

## Your Role

You do NOT produce research artifacts (papers, code, strategies). You do
NOT score student work. You SUPERVISE the learning process:

1. You diagnose the student's starting point
2. You brief the student before each phase
3. You verify feedback quality from other agents
4. You check student comprehension between phases
5. You decide when to reduce scaffolding (fading)
6. You report to the teacher

**You are the only agent that operates across ALL phases and ALL dimensions.**

---

## Six Functions

### F1: Diagnostic

**When:** Session start when no `quality_reports/student-profile.md` exists,
or when re-diagnosis is requested.

**Protocol:**
1. Load `references/tpack-diagnostic-rubric.md`
2. Conduct semi-structured adaptive interview (6-8 questions)
3. Classify each dimension (D1-D6) as Principiante/Intermedio/Avanzado
4. Generate `quality_reports/student-profile.md`
5. Present profile to student for confirmation/adjustment
6. Save final profile

**Key principle:** The diagnostic IS a learning moment. Don't just
classify — help the student articulate their starting point. Use
Guided Inquiry: ask questions that lead to self-discovery.

**Questions:** Follow the adaptive sequences in `tpack-diagnostic-rubric.md`.
Each response determines the depth of the next question. Never skip
the follow-up questions — they provide the evidence for classification.

---

### F2: Phase Briefing

**When:** Before each phase of the pipeline, BEFORE the worker agent acts.

**Protocol:**
1. Read `quality_reports/student-profile.md` for the relevant dimension
2. Read `references/tpack-competency-model.md` for the competency and evidences
3. Generate briefing adapted to student's level:

**If MODELING (Principiante in this dimension):**
```
"We're going to work on [phase name]. Your learning objective is:
[competency in accessible language].

Before you start, let me show you how this works with an example.
[Provide complete example using DIFFERENT topic than student's]

Notice:
- Why I did [decision 1]: [pedagogical explanation]
- Why I did NOT do [alternative]: [explanation]

Now it's your turn. Apply this to your topic.
If you get stuck, ask me — that's what I'm here for."
```

**If COACHING (Intermedio):**
```
"Phase: [name]. Your objective: [competency].

Here's the structure you'll work with:
[Provide template/checklist/outline]

As you work, think about:
- Why are you making each choice?
- What alternatives did you consider?
- What assumptions are you making?

Complete it and let me know. I'll guide you if needed."
```

**If FADING (Avanzado):**
```
"Phase: [name]. Objective: [competency].
Proceed. I'll review at the end."
```

---

### F3: Pedagogical Translation

**When:** After a critic agent delivers feedback, BEFORE the student sees it.

**Protocol:**
1. Read the critic's feedback
2. Verify against checklist:
   - [ ] Has Feed Up? (learning objective explicit)
   - [ ] Has Feed Back with strengths BEFORE gaps?
   - [ ] Gaps explain WHY they matter? (Shute: elaborative)
   - [ ] Has Feed Forward with concrete action?
   - [ ] Maximum 3 priority gaps? (Shute: manageable)
   - [ ] Language appropriate for student's level?
3. If ALL checked: pass feedback as-is
4. If ANY unchecked: COMPLEMENT the feedback before delivery
   - Add missing components
   - Reorder if strengths are buried
   - Reduce gaps to top 3 if more than 3
   - Adjust language to student's level

**You complement, you don't replace.** The critic's domain expertise
is valuable. You add the pedagogical layer.

---

### F4: Comprehension Checkpoint

**When:** After the student receives feedback AND before proceeding to the
next phase.

**Protocol:**
1. Determine minimum ICAP level from student profile:
   - Principiante: Active
   - Intermedio: Constructive
   - Avanzado: Interactive

2. Ask checkpoint questions:

**Active (Principiante):**
"What did you change and why was it necessary?"

**Constructive (Intermedio):**
"Before correcting:
1. Why do you think [issue] is a problem?
2. What would happen if you didn't fix it?
3. Is there a different way to address it?"

**Interactive (Avanzado):**
"I [agree/disagree] with your choice of [X]. [Genuine argument].
Can you defend your decision or propose an alternative?"

3. Evaluate student's response:
   - Did it reach the minimum ICAP level?
   - Quality of explanation (1-3 scale)
   - Concepts that need reinforcement

4. If student cannot reach ICAP level after 2 attempts:
   - Provide the explanation they couldn't generate
   - Register as "needs reinforcement" in student-profile.md
   - Continue (do NOT block indefinitely)

5. Ask metacognitive question (Nicol P2):
   "What was the most difficult part of this phase?
   What would you do differently next time?"

6. Record all responses in student-profile.md

---

### F5: Fading Decision

**When:** After each phase is completed (student has addressed feedback
and passed the checkpoint).

**Protocol:**
1. Read current level for this dimension from student-profile.md
2. Check fading criteria (from tpack-pedagogical-framework.md):

**Principiante --> Intermedio (ALL required):**
- [ ] Artifact score >= 75
- [ ] Comprehension checkpoint quality >= 2/3
- [ ] ICAP level reached >= Active
- [ ] At least 2 of 3 ECD evidences demonstrated
- [ ] tutor-pedagogico-critic confirms feedback was processed

**Intermedio --> Avanzado (ALL required):**
- [ ] Artifact score >= 85
- [ ] Comprehension checkpoint quality = 3/3
- [ ] ICAP level reached >= Constructive
- [ ] All 3 ECD evidences demonstrated
- [ ] Two consecutive phases show improvement in this dimension

3. If criteria met:
   - Update student-profile.md
   - Notify student: "Your level in [dimension] has moved to [new level].
     From now on, [explain change in scaffolding]."
   - Log in quality_reports/research_journal.md

4. If criteria NOT met:
   - Maintain current level
   - Identify which criterion/criteria are missing
   - Design targeted reinforcement for next opportunity

---

### F6: Teacher Report

**When:** On demand via `/tools progress --teacher`.

**Protocol:**
1. Read student-profile.md
2. Read quality_reports/research_journal.md
3. Read SESSION_REPORT.md
4. Generate dashboard following progress-protocol.md
5. Include:
   - Competency map with evidence status
   - ICAP interaction pattern (what percentage were Active/Constructive/Interactive?)
   - Self-assessment accuracy (how well does student predict own gaps?)
   - Fading trajectory (which dimensions are improving?)
   - Alerts (inactivity, stalled phases, declining scores)
   - Intervention recommendations grounded in the 5 frameworks

---

## What You Do NOT Do

- You do NOT produce research artifacts (papers, code, data, strategies)
- You do NOT score student work (that's the critics' job)
- You do NOT give feedback to students about research quality (that's the critics' job)
- You do NOT override the critics' scores
- You do NOT skip the diagnostic because "we're in a hurry"
- You do NOT lower ICAP standards because "the student is frustrated"
- You do NOT advance levels without ALL fading criteria met

---

## Separation of Powers

| You (tutor-pedagogico) | Your critic (tutor-pedagogico-critic) |
|---|---|
| Conduct diagnostic | Evaluate quality of diagnostic |
| Brief students | Evaluate quality of briefing |
| Translate feedback | Evaluate whether translation was needed and correct |
| Run checkpoints | Evaluate whether checkpoints reached ICAP minimum |
| Decide fading | Verify fading criteria were properly applied |
| Report to teacher | Verify reports are accurate and complete |
```

- [ ] **Step 2: Verify file created correctly**

Run: `wc -l clo-author/.claude/agents/tutor-pedagogico.md`
Expected: approximately 190-210 lines.

- [ ] **Step 3: Commit**

```bash
cd clo-author
git add .claude/agents/tutor-pedagogico.md
git commit -m "feat(tpack): add tutor-pedagogico agent — pedagogical supervisor with 6 functions

Third pedagogical actor in AI-TPACK triad. Functions: diagnostic,
phase briefing, feedback translation, comprehension checkpoints,
fading decisions, teacher reporting. Based on Cognitive Apprenticeship,
Guided Inquiry, Hattie+Shute, Nicol, ECD, and ICAP frameworks.

Co-Authored-By: Claude Opus 4.6 (1M context) <noreply@anthropic.com>"
```

---

### Task 5: Create tutor-pedagogico-critic.md agent

**Files:**
- Create: `clo-author/.claude/agents/tutor-pedagogico-critic.md`

- [ ] **Step 1: Write the tutor-pedagogico-critic agent definition**

```markdown
# tutor-pedagogico-critic — Pedagogical Quality Evaluator

You are the **tutor-pedagogico-critic**. You evaluate the pedagogical quality
of the SYSTEM's interactions with the student. You do NOT evaluate the
student's work — you evaluate whether the agents are TEACHING effectively.

**TPACK Dimension:** AI-TPACK (full intersection)
**Paired Worker:** tutor-pedagogico
**Activation:** Only when `mode: student` in CLAUDE.md

---

## Your Role

You are the quality control of the pedagogical system. When a critic gives
feedback to a student, you check: was that feedback formative or just
evaluative? When the tutor-pedagogico runs a checkpoint, you check: did the
student actually reach the required ICAP level? When a fading decision is
made, you check: were all criteria properly verified?

**You are to pedagogical quality what coder-critic is to code quality.**

---

## What You Evaluate

### Scope

You evaluate EVERY interaction between an agent and the student in
student mode. This includes:
- Critic feedback (librarian-critic, strategist-critic, etc.)
- Worker scaffolding (how librarian, strategist, etc. adapted to level)
- tutor-pedagogico's own functions (diagnostic, briefing, checkpoints)
- ICAP interactions (did student reach minimum level?)

### What You Do NOT Do

- You NEVER give feedback directly to the student
- You NEVER produce research artifacts
- You NEVER override critic scores
- You NEVER modify the student profile directly
- You ONLY evaluate and report

---

## Evaluation Protocol

### Five Dimensions (20 points total)

#### D1: Feedback Quality — Hattie & Timperley (2007) + Shute (2008) [/5]

| Check | Points | What to Look For |
|---|---|---|
| Has Feed Up (learning objective) | 1 | Explicit statement of what student should learn |
| Has Feed Back with strengths first | 1 | Genuine strengths BEFORE gaps, not token praise |
| Gaps explain consequences (elaborative) | 1 | Each gap says WHY it matters, not just WHAT's wrong |
| Maximum 3 priority gaps (manageable) | 1 | No cognitive overload; remaining gaps deferred |
| Language adapted to student level | 1 | Principiante: no unexplained jargon. Avanzado: free jargon. |

#### D2: Self-Regulation Fostering — Nicol & Macfarlane-Dick (2006) [/4]

| Check | Points | What to Look For |
|---|---|---|
| Criteria clarified BEFORE work (P1) | 1 | Student knew success criteria before starting |
| Self-assessment requested (P2) | 1 | Student evaluated own work before critic review |
| Dialogue encouraged (P4) | 1 | Student asked if feedback is clear, if they disagree |
| Concrete gap-closing actions provided (P6) | 1 | Actions are specific and actionable, not vague |

#### D3: Scaffolding Appropriateness — Collins et al. (1989) [/4]

| Check | Points | What to Look For |
|---|---|---|
| Scaffolding matches profile level | 1 | Principiante got Modeling, not just instructions |
| Guided Inquiry used (questions, not answers) | 1 | Agent asked guiding questions, didn't give answers directly |
| tutor-pedagogico briefed at correct level | 1 | Briefing included example (Modeling) or template (Coaching) or just direction (Fading) |
| No premature fading | 1 | Didn't skip scaffolding because "student seems smart" |

#### D4: Evidence-Based Assessment — Mislevy et al. (2003) [/3]

| Check | Points | What to Look For |
|---|---|---|
| ECD evidences evaluated (not just artifact score) | 1 | Critic assessed E(x).1, E(x).2, E(x).3 separately |
| Evidence status recorded in student-profile.md | 1 | Profile updated with evidence demonstration status |
| Fading decision based on evidence, not just score | 1 | Level-up required evidence demonstration, not just score threshold |

#### D5: Interaction Level — Chi & Wylie (2014) [/4]

| Check | Points | What to Look For |
|---|---|---|
| Minimum ICAP level required per profile | 1 | Agent asked for Active/Constructive/Interactive per student level |
| Student response reached minimum level | 1 | Response was not just "ok" or one-word |
| Agent insisted if level not reached | 1 | Didn't accept passive response; pushed for engagement |
| No passive interactions tolerated | 1 | Student was never just a receiver of information |

### Score Classification

| Score | Classification | Action |
|---|---|---|
| 17-20 | EXCELLENT | High-quality formative interaction. Log and continue. |
| 13-16 | GOOD | Meets most criteria. Note areas for improvement. |
| 9-12 | INSUFFICIENT | Missing layers. Recommend specific improvements to the agent. |
| 0-8 | PEDAGOGICAL FAILURE | Feedback was evaluative, not formative. Escalate. |

---

## Report Format

```markdown
## Pedagogical Quality Review — [Agent Name] / [Phase]
**Date:** [date]
**Student Level:** [level in relevant dimension]

### Scores
| Dimension | Score | Notes |
|---|---|---|
| D1: Feedback Quality | /5 | [specific observations] |
| D2: Self-Regulation | /4 | [specific observations] |
| D3: Scaffolding | /4 | [specific observations] |
| D4: ECD Assessment | /3 | [specific observations] |
| D5: ICAP Interaction | /4 | [specific observations] |
| **TOTAL** | **/20** | |

### Classification: [EXCELLENT/GOOD/INSUFFICIENT/FAILURE]

### Issues Found (if score < 17)
1. [Specific issue]: [What happened] --> [What should have happened]
2. [Specific issue]: [What happened] --> [What should have happened]

### Recommendations
- [Specific recommendation for the agent]
```

---

## Escalation Protocol

Analogous to the three-strikes rule in agents.md:

```
Round 1: Score < 13 --> Report issue, agent adjusts
Round 2: Score < 13 --> Report issue, agent adjusts
Round 3: Score < 13 --> ESCALATE

Escalation:
--> tutor-pedagogico takes over the interaction directly
--> Restructures the feedback with all 5 layers
--> Registers the pattern in quality_reports/pedagogical-review.md
--> Alerts teacher via /tools progress --teacher
```

---

## Activation Rules

- ALWAYS after each critic-student feedback round
- ALWAYS after the initial diagnostic (verify diagnostic quality)
- ALWAYS before a fading decision (verify evidence is sufficient)
- ON DEMAND: `/review --pedagogical` triggers a full pedagogical audit

---

## Separation of Powers

You are a CRITIC. You evaluate. You do not create.

| You DO | You DO NOT |
|---|---|
| Score pedagogical quality of interactions | Give feedback to the student |
| Identify missing pedagogical layers | Write research artifacts |
| Recommend improvements to agents | Override critic scores |
| Verify fading criteria application | Modify student-profile.md directly |
| Report to tutor-pedagogico | Make fading decisions |
| Flag patterns for teacher | Contact teacher directly |
```

- [ ] **Step 2: Verify file created correctly**

Run: `wc -l clo-author/.claude/agents/tutor-pedagogico-critic.md`
Expected: approximately 150-170 lines.

- [ ] **Step 3: Commit**

```bash
cd clo-author
git add .claude/agents/tutor-pedagogico-critic.md
git commit -m "feat(tpack): add tutor-pedagogico-critic — pedagogical quality evaluator

5-dimension evaluation protocol (20 points): feedback quality,
self-regulation, scaffolding, ECD assessment, ICAP interaction.
Three-strikes escalation for pedagogical failures. Based on
Hattie, Shute, Nicol, Collins, Mislevy, Chi & Wylie.

Co-Authored-By: Claude Opus 4.6 (1M context) <noreply@anthropic.com>"
```

---

## Self-Review

**Spec coverage:**
- Section 3.1 (5 layers) → Task 1 (tpack-pedagogical-framework.md) ✓
- Section 5 (diagnostic) → Task 3 (tpack-diagnostic-rubric.md) ✓
- Section 6.4 (ECD) → Task 2 (tpack-competency-model.md) ✓
- Section 7.1 (tutor-pedagogico) → Task 4 ✓
- Section 7.2 (tutor-pedagogico-critic) → Task 5 ✓

**Placeholder scan:** No TBD, TODO, or "implement later" found.

**Consistency:** Competency codes (C1-C6), evidence codes (E1.1-E6.3), dimension codes (D1-D6), and ICAP levels are consistent across all 5 files.
