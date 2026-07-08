---
name: agent-retro
description: >
  Operator-run retrospective on the agent's last session. NOT for product gaps.
  Run when you think the agent needs to learn from what just happened.
argument-hint: "[last-session | last-task | specific topic]"
---

# Agent Retrospective

Operator-run. You invoke this when the agent shipped something but the journey
was painful. This skill diagnoses WHY and records the fix so the NEXT session
is better.

These are NOT product gaps. They are agent runtime issues.

## Workflow

### 1. Reconstruct from primary evidence — NOT narrative memory

The richest evidence is NOT commits. Sweep ALL of these:

- Git log (last 3-5 commits, reverts, fix-on-fix patterns)
- Hand-back tables (operator-facing summaries — what claims were made?)
- RESULT.md / evidence docs (what was actually observed vs claimed?)
- CX gaps filed mid-session (what did the agent already catch?)
- Dead-approaches register (what was tried + reverted?)

Every "what went wrong" claim MUST be re-derived from an artifact, never
from memory. A retro built on git log alone re-creates the fabricated-timeline
risk — the commits look clean but the session was not.

### 2. Classify each issue — FIVE classes

| Class | Definition | Action |
|---|---|---|
| **CX-CANDIDATE** | Missing/vague/undiscoverable rule. A contract rule or CX gap would have prevented this. | File CX gap + update contract. |
| **VERIFICATION-GAP** | The agent claimed success but proof was below claim level. A fix shipped without evidence it actually worked. For every claim, check: proof >= claim? Gates need ENGAGE proofs. | File CX against the testing protocol. Flag the specific hand-back that overstated. |
| **AGENT-NOTE** | Bad call despite available info — wrong assumption, ignored contract, over-engineered. | Append to NOTES.md. Before appending: grep NOTES.md for the same pattern. Second occurrence auto-escalates to CX-CANDIDATE (repeated mistake = missing rule). |
| **OPERATOR-NOTE** | Ambiguous instructions or agent didn't ask clarifying questions. | Report inline. Do not file. |
| **CODE-SMELL** | Codebase itself is confusing — misleading names, dead code that looks alive. NOT dirty runtime state. | Append to SMELLS.md. Do not fix. |

### 3. Output — mandatory sections

(To be filled during the retro.)

### 4. Apply

- CX-CANDIDATE + VERIFICATION-GAP: file CX gap + update contract. Same-commit.
- AGENT-NOTE: append to NOTES.md. Format: "YYYY-MM-DD — <pattern> — <pointer to contract/file>". Dedupe on append (grep first). Second occurrence of same pattern -> escalate to CX-CANDIDATE.
- Dead approach: append to the dead-approaches register in the retro commit. That is the file that prevents retries — NOTES.md is where lessons go to be forgotten.
- Dirty runtime state / config drift found during retro -> tech-debt ledger + CX per its guard rule. NOT SMELLS.md.
- CODE-SMELL: append to SMELLS.md. One line + date + file:line pointer. Dedupe. No essays.
- OPERATOR-NOTE: report inline. Do not file.

## Rules

1. **Observe, don't fix.** Retro is diagnosis, not repair. CX gaps filed but never fixed in the same session (unless operator says fix it).
2. **No blame.** The agent didn't fail — the system failed to guide it. Retro fixes the system.
3. **One CX per root cause.** Don't file 3 gaps for 3 symptoms of the same missing rule.
4. **AGENT-NOTEs are specific.** "Read contracts first" is useless. Say "contract X.md line Y says Z; agent applied it to the wrong tier."
5. **Recurrence escalates.** Second occurrence of the same AGENT-NOTE pattern = CX-CANDIDATE. A repeated agent mistake is a missing rule, not bad luck.
6. **Proof >= claim.** Every hand-back claim checked against actual evidence.
7. **Primary evidence only.** Every wrong-turn claim re-derived from an artifact (commit, hand-back, RESULT.md, CX gap, dead-approaches register). Never from narrative memory.

## Files

- NOTES.md — agent-improvement log. One line per entry. Deduped. Second occurrence -> CX.
- SMELLS.md — confusing code. One line + date + pointer. Deduped. No essays. Dirty runtime state -> tech-debt, NOT here.
- Created on first use next to this SKILL.md.
