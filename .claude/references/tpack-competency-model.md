# TPACK Competency Model — Evidence-Centered Design

This file defines the competency-evidence-task model for evaluating student
learning across the research pipeline. Based on Evidence-Centered Design
(Mislevy, Steinberg & Almond, 2003).

**When to load:** Agents in student mode evaluating competency demonstration.
tutor-pedagogico uses this for diagnostic and fading decisions.

---

## Design Principle

```
COMPETENCY (what we want to measure -- latent, not directly observable)
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
**Agent Pair:** tutor-pedagogico conducts; no separate worker for formulation

### Evidences

| Evidence | Observable Indicator |
|---|---|
| E1.1: Delimited question | Question specifies population, variable(s), and context. Not a topic -- a question. |
| E1.2: Justified relevance | Explains WHY this question matters, citing literature or empirical evidence of the problem. |
| E1.3: Feasible scope | Question is answerable with available methods and data within realistic constraints. |

### Assessment Criteria

| Level | E1.1 | E1.2 | E1.3 |
|---|---|---|---|
| NOT demonstrated | "I want to study AI in education" (topic, not question) | "It's important because AI is trending" (no evidence) | Scope impossible given constraints |
| PARTIAL | "How does AI affect learning?" (question but undelimited) | "Studies show AI can help (Smith, 2020)" (one citation, no depth) | Feasible but constraints not explicitly discussed |
| DEMONSTRATED | "How does an AI tutoring ecosystem based on AI-TPACK affect research competencies in graduate students at [institution]?" | "Graduate programs face increasing student-advisor ratios (De Kleijn et al., 2012), creating a supervision gap that affects thesis quality (Pyhaltto et al., 2015)" | "15-20 students, 1 semester, mixed methods -- consistent with DBR pilot standards (McKenney & Reeves, 2012)" |

---

## Competency C2: Evaluates Literature Critically

**TPACK Dimension:** TCK (Technology + Content)
**Diagnostic Dimension:** D2
**Pipeline Phase:** /discover lit
**Agent Pair:** librarian + librarian-critic

### Evidences

| Evidence | Observable Indicator |
|---|---|
| E2.1: Identifies research gaps | Points to specific questions not yet answered, populations not studied, methods not applied -- with evidence. |
| E2.2: Distinguishes source quality | Differentiates peer-reviewed from grey literature, seminal from peripheral, high-impact from predatory. |
| E2.3: Synthesizes, not summarizes | Organizes literature by themes/arguments/debates, not chronologically or by author. Identifies patterns and contradictions. |

### Assessment Criteria

| Level | E2.1 | E2.2 | E2.3 |
|---|---|---|---|
| NOT demonstrated | "There are few studies on this topic" (assertion without evidence) | Cites blog posts and Wikipedia alongside journals | Lists papers chronologically: "Smith (2018) found X. Jones (2019) found Y." |
| PARTIAL | "No studies have examined [X] in [context]" (specific but not verified) | Uses peer-reviewed sources but doesn't evaluate methodology | Groups by topic but doesn't connect themes or identify contradictions |
| DEMONSTRATED | "While [X] has been studied in [contexts A, B] (refs), no study has examined [specific gap] in [specific context], despite evidence that [why this context matters]" | Evaluates sources: "While Smith (2020) reports [X], the sample (N=12) limits generalizability" | "Three perspectives emerge: [theme 1] (refs), [theme 2] (refs), and a tension between them regarding [specific point]" |

---

## Competency C3: Designs Empirical Strategy

**TPACK Dimension:** PCK (Pedagogy + Content) / AI-TPACK for full intersection
**Diagnostic Dimension:** D3
**Pipeline Phase:** /strategize
**Agent Pair:** strategist + strategist-critic

### Evidences

| Evidence | Observable Indicator |
|---|---|
| E3.1: Specifies and defends assumptions | States each assumption required by the method AND provides argument for why it's credible in this context. |
| E3.2: Anticipates objections | Identifies what a skeptical reviewer would question and prepares responses. |
| E3.3: Proposes robustness checks | Designs alternative specifications that test sensitivity of results to methodological choices. |

### Assessment Criteria

| Level | E3.1 | E3.2 | E3.3 |
|---|---|---|---|
| NOT demonstrated | Cannot name the assumptions of chosen method | "There may be some limitations" (vague) | No robustness checks proposed |
| PARTIAL | "DiD assumes parallel trends" (names but doesn't defend) | "Selection bias is a concern" (names threat but no response) | "We could try different controls" (vague) |
| DEMONSTRATED | "Parallel trends requires that [treatment/control] would have followed the same trajectory absent treatment. This is credible because [specific evidence]: pre-treatment trends are parallel for [N] years (Figure X)" | "A reviewer might argue that [specific confounder] drives our results. We address this by [specific test/control]. If [confounder] were driving results, we would expect [pattern] -- we test this in Table X" | "Robustness: (1) add [controls] -- expect stable point estimate; (2) placebo test at [fake date] -- expect null; (3) [alternative estimator] -- expect similar magnitude" |

---

## Competency C4: Implements Analysis

**TPACK Dimension:** TPK (Technology + Pedagogy)
**Diagnostic Dimension:** D4
**Pipeline Phase:** /analyze
**Agent Pair:** coder + coder-critic (+ data-engineer for pipeline)

### Evidences

| Evidence | Observable Indicator |
|---|---|
| E4.1: Code-strategy alignment | Code implements EXACTLY what the strategy memo specifies -- same estimator, fixed effects, clustering, sample restrictions. |
| E4.2: Results pass sanity checks | Sign is expected, magnitude is plausible, dynamics make sense, results are consistent across specifications. |
| E4.3: Can explain the code | Student can describe what each section of the script does, WHY it does it, and how it connects to the methodology. |

### Assessment Criteria

| Level | E4.1 | E4.2 | E4.3 |
|---|---|---|---|
| NOT demonstrated | Code uses different estimator or specification than strategy memo | Results have wrong sign or implausible magnitude, student doesn't notice | Cannot explain what key functions do |
| PARTIAL | Code matches strategy but with minor deviations (e.g., wrong clustering level) | Notices anomalies but cannot explain them | Describes steps but not WHY |
| DEMONSTRATED | Code is exact implementation of strategy memo; any deviations are documented and justified | Checks sign, magnitude, dynamics; explains anomalies with theory; compares across specifications | Explains each section's purpose, connection to methodology, and implementation choices |

---

## Competency C5: Writes Academically

**TPACK Dimension:** PCK (Pedagogy + Content)
**Diagnostic Dimension:** D5
**Pipeline Phase:** /write
**Agent Pair:** writer + writer-critic

### Evidences

| Evidence | Observable Indicator |
|---|---|
| E5.1: Clear contribution | Contribution is explicit within first 2 pages, stating what's new and why it matters. |
| E5.2: Evidence-backed claims | Every causal or evaluative claim has corresponding evidence (data, citation, logical argument). |
| E5.3: Professional academic voice | No hedging, no AI-generated language patterns, appropriate register, consistent notation. |

### Assessment Criteria

| Level | E5.1 | E5.2 | E5.3 |
|---|---|---|---|
| NOT demonstrated | Contribution buried or absent; reader doesn't know what's new after 2 pages | Claims without evidence: "AI improves learning" with no citation or data | Heavy hedging ("might possibly suggest"), AI patterns ("delving into"), informal register |
| PARTIAL | Contribution stated but vague: "This paper contributes to the literature" | Most claims backed but some assertions unsupported | Occasional hedging, mostly appropriate register, minor notation inconsistencies |
| DEMONSTRATED | "This paper makes three contributions: First, [specific]. Second, [specific]. Third, [specific]" within first 2 pages | Every claim has citation, data reference, or logical argument; no orphan assertions | Clean professional voice, zero hedging, consistent notation throughout, no AI patterns |

---

## Competency C6: Communicates Findings

**TPACK Dimension:** TPK (Technology + Pedagogy)
**Diagnostic Dimension:** D6
**Pipeline Phase:** /talk + /review
**Agent Pair:** storyteller + storyteller-critic (+ editor for peer review)

### Evidences

| Evidence | Observable Indicator |
|---|---|
| E6.1: Coherent narrative | Presentation follows logical arc: hook --> problem --> method --> results --> implication. Audience can follow without reading the paper. |
| E6.2: Effective visualizations | Figures and tables are self-explanatory, properly labeled, and support the argument. |
| E6.3: Defends under questioning | Can respond to critical questions about methodology, data, and interpretation without reading notes. |

### Assessment Criteria

| Level | E6.1 | E6.2 | E6.3 |
|---|---|---|---|
| NOT demonstrated | Reads slides, no narrative arc, audience lost | Figures copied from paper without adaptation, too small, unlabeled | Cannot answer basic methodology questions |
| PARTIAL | Has structure but transitions are weak; some sections unclear | Figures are clear but don't tell a story independently | Answers basic questions but struggles with methodology challenges |
| DEMONSTRATED | Compelling narrative arc, clear transitions, audience engaged, key takeaway memorable | Figures designed for presentation (large, labeled, self-explanatory), each supports a specific argument | Handles critical questions confidently, defends methodology with evidence, acknowledges limitations honestly |

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
