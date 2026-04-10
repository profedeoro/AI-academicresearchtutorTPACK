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

- "Your work needs improvement" -- vague, not specific (Shute: specificity)
- "This is wrong" without WHY -- evaluative, not elaborative
- Listing 8 problems at once -- overwhelming (Shute: manageable)
- "Good job!" without specifying WHAT was good -- empty praise
- Commenting on student intelligence or effort -- task-oriented only
- Giving feedback only at the end -- timely means DURING the process

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
- Where they MATCH: "You correctly identified that [X] -- good self-awareness"
- Where they DIFFER: "You rated [X] as adequate, but [specific evidence shows gap]. This difference is a learning opportunity -- here's why..."

#### P4: Encourage Dialogue (All agents, after feedback)

```
Before you start revising:
- Is there any part of this feedback you don't understand?
- Is there anything you disagree with? (Disagreement is valuable —
  explain your reasoning and we can discuss)
- Do you need more detail on any of the suggested actions?
```

NEVER skip this step. Student silence is not agreement -- it may be confusion.

#### P7: Inform Teacher (tutor-pedagogico only)

Generate reports for `/tools progress --teacher` that include:
- Self-assessment accuracy (how well student predicts own gaps)
- Dialogue patterns (does student ask questions or stay silent?)
- Gap closure rate (does feedback lead to improvement?)
- Recurring gaps (same issue appearing across phases)

---

## Layer 3: Disciplinary Scaffolding (Collins, Brown & Newman, 1989 + Kuhlthau et al., 2007)

### Theoretical Foundation

**Cognitive Apprenticeship** (Collins et al., 1989) adapts traditional apprenticeship to cognitive skills. Six teaching methods, of which we use four:

| Method | Description | When |
|---|---|---|
| **Modeling** | Expert demonstrates complete process, making thinking visible | Principiante -- student has never done this |
| **Coaching** | Expert observes student attempting task, offers guidance | Intermedio -- student attempts with support |
| **Scaffolding** | Expert provides structure that student fills in | Intermedio -- student has partial competence |
| **Fading** | Expert gradually withdraws support | Avanzado -- student demonstrates competence |

Two additional methods (articulation, reflection) are embedded in ICAP checkpoints.

**Guided Inquiry** (Kuhlthau, Maniotes & Caspari, 2007) structures the inquiry process through 6 phases that map to the clo-author pipeline:

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

1. BEFORE asking the student to work:
   a. Explain WHAT this phase is and WHY it matters for research
   b. Show a COMPLETE worked example using a DIFFERENT topic (never the student's own topic -- they must transfer, not copy)
   c. Narrate EVERY decision in the example: "I chose [X] because [reason]. I did NOT choose [Y] because [reason]."
   d. Make thinking VISIBLE -- explain the reasoning, not just the steps

2. THEN use Guided Inquiry to help the student discover:
   a. Ask open-ended questions that lead to understanding: "What terms would you use to search for your topic? Why those?"
   b. Do NOT give answers directly -- guide toward discovery
   c. If student is stuck after 2 attempts, provide a hint, not the answer
   d. If stuck after hint, model ONE step with student's topic, then ask them to continue

3. NEVER write the complete artifact for the student. The student must produce the work; you guide the process.

#### COACHING (Intermedio)

1. Provide STRUCTURE (template, checklist, outline) for the task
2. Student EXECUTES within the structure
3. Coach DURING execution with probing questions: "Why did you choose [X]? What alternatives did you consider?" "What assumption are you making here? Is it testable?"
4. Intervene ONLY when student deviates significantly from good practice
5. Celebrate good decisions: "That was a strong choice because [reason]"

#### SCAFFOLDING (Intermedio, more structured)

1. Provide a PARTIAL solution that the student completes: template with [COMPLETE THIS] sections, skeleton code with key functions defined but body empty, outline with topic sentences written and paragraphs to fill
2. Student COMPLETES and JUSTIFIES each decision
3. Review completions, focus on justifications

#### FADING (Avanzado)

1. Give the instruction without additional structure: "Design your identification strategy. Specify assumptions, threats, and robustness checks."
2. Student executes AUTONOMOUSLY
3. Review at the END with standard feedback
4. Intervene ONLY if there is a serious conceptual error

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

This separation prevents the common error of equating "artifact quality" with "student learning." A student can produce a good artifact by copying; ECD checks whether the student DEMONSTRATES the underlying competency.

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
- Any PARTIAL: DEVELOPING -- [specify what's missing]
- Any NO: NOT DEMONSTRATED -- [specify what's missing]
```

**Key principle:** An artifact can score 85/100 but if a critical evidence is NOT demonstrated, the competency is NOT achieved. Scores measure product quality; ECD measures learning.

Register results in `quality_reports/student-profile.md`.

---

## Layer 5: Interaction Design (Chi & Wylie, 2014)

### Theoretical Foundation

ICAP framework classifies learning activities by cognitive engagement:

| Level | Student Behavior | Cognitive Process | Learning Outcome |
|---|---|---|---|
| **Passive** | Receives without responding | Storage | Minimal -- may not even store |
| **Active** | Manipulates, repeats, copies | Activation of existing knowledge | Low -- rehearsal without integration |
| **Constructive** | Generates new output beyond input | Integration of new + existing knowledge | High -- creates new understanding |
| **Interactive** | Co-constructs with another agent | Joint integration + negotiation | Maximum -- deepest processing |

The ICAP hypothesis: Interactive > Constructive > Active > Passive for learning.

### Minimum ICAP Level by Student Level

| Student Level | Minimum ICAP | What This Means |
|---|---|---|
| Principiante | **Active** | Student must DO something with the feedback -- correct AND explain |
| Intermedio | **Constructive** | Student must GENERATE beyond the feedback -- justify, anticipate, propose |
| Avanzado | **Interactive** | Student must CO-CONSTRUCT -- debate, defend, negotiate meaning |

### Enforcement Mechanisms

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
think I'm wrong -- that's how academic discourse works."
```

### What Agents Must NOT Do

- Proceed automatically after feedback without student response (kills ICAP)
- Accept a one-word response ("ok", "done") as meeting Active threshold
- Skip the ICAP interaction because "the student already fixed it"
- Lower the ICAP threshold because "we're running out of time"

### Maximum Attempts

If student cannot reach minimum ICAP level after 2 attempts:
1. Register as "needs reinforcement" in student-profile.md
2. Provide the explanation the student couldn't generate
3. Continue to next step (do NOT block indefinitely)
4. Flag for tutor-pedagogico to design a reinforcement activity

---

## Cross-Layer Integration

The 5 layers are not independent -- they reinforce each other:

| Integration | How |
|---|---|
| L1 + L2 | Feed Up = P1 (clarify criteria). Self-assessment (P2) happens before Feed Back. |
| L1 + L3 | Feed Forward adapts to scaffolding level (example for Modeling, resource for Coaching, direction for Fading) |
| L1 + L4 | Feed Back evaluates both artifact quality AND ECD evidences |
| L2 + L5 | Self-assessment (P2) IS an ICAP-Active interaction at minimum |
| L3 + L5 | Modeling phase uses Guided Inquiry questions = ICAP-Active. Coaching uses probing questions = ICAP-Constructive. |
| L4 + L3 | ECD evidence assessment informs fading decisions |
