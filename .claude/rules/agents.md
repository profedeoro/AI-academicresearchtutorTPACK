# Agents: Pairs, Separation of Powers, and Escalation

---

## 1. Adversarial Pairing

**Every worker agent has a paired critic. The Orchestrator never dispatches a creator without scheduling its critic.**

### Worker-Critic Pairs

| Worker (Creator) | Critic (Reviewer) | What's Reviewed |
|-----------------|-------------------|-----------------|
| librarian | librarian-critic | Literature coverage, gaps, recency |
| explorer | explorer-critic | Data feasibility, quality, identification fit |
| data-engineer | coder-critic | Data pipeline quality, reproducibility, transformation correctness |
| strategist | strategist-critic | Identification validity, assumptions, robustness |
| coder | coder-critic | Code quality, reproducibility, code-strategy alignment |
| writer | writer-critic | Manuscript polish, LaTeX quality, hedging |
| storyteller | storyteller-critic | Talk structure, audience calibration, visual quality |

### Peer Review (Special Case)

Peer Review uses a different structure — the Orchestrator dispatches two independent referees:

1. Orchestrator assigns the paper to domain-referee and methods-referee (blind, independent)
2. Both referees produce scored reports
3. Orchestrator synthesizes a decision: Accept / Minor Revisions / Major Revisions / Reject

### Enforcement

- The Orchestrator checks: if a creator artifact exists without a critic score, it is **not approved**
- No artifact advances to the next phase without its critic's score >= 80
- Critics produce scores; creators produce artifacts — never the reverse

---

## 2. Separation of Powers

**Critics never create. Creators never self-score.**

### Critics Never Create

A critic's job is to evaluate, not to produce artifacts. If a critic produces code, text, or data during its review, something is wrong.

**What critics DO:**
- Score artifacts against a rubric
- List issues with severity and deductions
- Suggest fixes (as recommendations, not implementations)

**What critics DON'T DO:**
- Write code to fix the issues they found
- Rewrite paper sections
- Produce alternative implementations

**Why:** A critic who fixes their own findings has incentive to find only fixable issues. Separation keeps criticism honest.

### Creators Can't Self-Score

A creator cannot evaluate the quality of its own work. The score always comes from the paired critic.

| Agent | Creates | Scored By |
|-------|---------|-----------|
| librarian | Annotated bibliography | librarian-critic |
| explorer | Data assessment | explorer-critic |
| data-engineer | Data pipeline and cleaned datasets | coder-critic |
| strategist | Strategy memo | strategist-critic |
| coder | R/Python/Julia scripts | coder-critic |
| writer | Paper manuscript | writer-critic |
| storyteller | Beamer talk | storyteller-critic |

### Enforcement

The Orchestrator flags violations:
- If a critic invocation produces a file in `scripts/`, `paper/`, or `paper/talks/` → flag
- If a creator reports its own score → discard, dispatch critic

---

## 3. Three Strikes Escalation

**If a worker-critic pair fails to converge after 3 rounds, the Orchestrator escalates.**

### The Protocol

```
Round 1: Critic reviews → Worker fixes
Round 2: Critic reviews → Worker fixes
Round 3: Critic reviews → Worker fixes
         Still failing?
              ↓
         ESCALATION
```

### Escalation Routing

| Pair | Escalation Target | What Happens |
|------|-------------------|--------------|
| coder + coder-critic | strategist-critic | Re-evaluates whether the strategy memo is implementable |
| data-engineer + coder-critic | strategist-critic | Re-evaluates whether the data specification is tractable |
| writer + writer-critic | Orchestrator | Structural rewrite, not just polish |
| strategist + strategist-critic | User | Fundamental design question — needs human judgment |
| librarian + librarian-critic | User | Scope disagreement — user decides breadth vs depth |
| explorer + explorer-critic | User | Data feasibility deadlock — user decides resource trade-offs |
| storyteller + storyteller-critic | User | Talk scope/format disagreement |
| tutor-pedagogico + tutor-pedagogico-critic | User | Pedagogical quality disagreement |

### Rules

- **Max 3 rounds per pair per invocation** — no infinite loops
- **Escalation is logged** in the research journal with strike count
- **User escalation requires a clear question** — not "they disagree," but "strategist-critic requires X, which contradicts Y. Which takes priority?"
- **Post-escalation:** The worker starts fresh from the escalation target's decision, not from its previous attempt

---

## 4. Pedagogical Escalation (Student Mode Only)

**Active only when `mode: student` in CLAUDE.md.**

### Pedagogical Quality Enforcement

The tutor-pedagogico-critic evaluates the pedagogical quality of every agent-student interaction on a 20-point scale (5 dimensions). If an agent consistently delivers evaluative instead of formative feedback, the system escalates.

### Three-Strikes Protocol (Pedagogical)

```
Round 1: Pedagogical score < 13 → tutor-pedagogico-critic reports → agent adjusts
Round 2: Pedagogical score < 13 → tutor-pedagogico-critic reports → agent adjusts
Round 3: Pedagogical score < 13 → ESCALATE
         ↓
    tutor-pedagogico takes over the interaction directly
    → Restructures feedback with all 5 pedagogical layers
    → Registers pattern in quality_reports/pedagogical-review.md
    → Alerts teacher via /tools progress --teacher
```

### What Gets Evaluated

| Dimension | Points | Framework |
|-----------|--------|-----------|
| Feedback quality (Feed Up/Back/Forward) | /5 | Hattie & Timperley (2007) + Shute (2008) |
| Self-regulation fostering | /4 | Nicol & Macfarlane-Dick (2006) |
| Scaffolding appropriateness | /4 | Collins, Brown & Newman (1989) |
| Evidence-based assessment | /3 | Mislevy, Steinberg & Almond (2003) |
| Interaction level (ICAP) | /4 | Chi & Wylie (2014) |

### Classification

| Score | Classification | Action |
|-------|---------------|--------|
| 17-20 | EXCELLENT | Log and continue |
| 13-16 | GOOD | Note improvements needed |
| 9-12 | INSUFFICIENT | Recommend specific improvements |
| 0-8 | PEDAGOGICAL FAILURE | Escalate immediately |
