# Agent Retro

**Post-incident diagnostics for AI agents.** Classify what went wrong, file
CX gaps, and improve your agent system — one session at a time.

## Quick start

```bash
git clone https://github.com/GadOfir/agent-retro.git
# Drop the skill into your Claude Code skills directory
cp SKILL.md .claude/skills/agent-retro/
```

Then tell your agent:

> **"Run a retrospective on the last session."**

The agent reads the skill, reconstructs what happened from evidence, classifies
each issue into one of five classes, and prescribes the fix.

## What you get

| File | Purpose |
|---|---|
| `index.html` | GitHub Pages landing page |
| `SKILL.md` | The retro protocol — classification + workflow |
| `NOTES.md` | Agent-improvement log (created on first use) |
| `SMELLS.md` | Confusing code log (created on first use) |

## The five classes

| Class | What it means | What to do |
|---|---|---|
| **CX-CANDIDATE** | Missing rule would have prevented this | File CX gap + update contract |
| **VERIFICATION-GAP** | Agent claimed success, proof was weak | Flag hand-back, harden testing |
| **AGENT-NOTE** | Bad call despite available info | Append to NOTES.md (deduped) |
| **OPERATOR-NOTE** | Instructions were ambiguous | Report inline, no file |
| **CODE-SMELL** | Codebase was confusing | Append to SMELLS.md (one line) |

## Customize me

This skill is a generic framework. To adapt it to your project:

1. **Replace the classification examples** — The current examples reference
   CONTRACTX conventions. Replace with your project's own failure patterns.
2. **Add your own artifact sources** — If your project has different evidence
   sources (e.g., a bug tracker, CI logs, deployment dashboard), add them to
   the "Reconstruct from evidence" step.
3. **Adjust the severity rules** — Change escalation thresholds or add new
   failure classes that match your domain.

## Troubleshooting

| Problem | Likely cause | Fix |
|---|---|---|
| Retro feels shallow | Only looked at git commits | Add artifact sources: hand-back tables, RESULT.md, session notes |
| Same issue keeps recurring | AGENT-NOTE wasn't deduped | Check NOTES.md — second occurrence auto-escalates |
| Classification feels forced | A real problem doesn't fit any class | File a CX gap for the missing class definition |
| Retro blames the agent | Operator forgot rule 2 | Retro fixes the system, never the agent. Re-read the rules. |

## License

MIT
