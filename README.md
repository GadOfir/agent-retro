# Agent Retro

**End-of-session learning for AI agents.** After a long session, the agent self-reports what went wrong. Triage by model, harness, and task step. Patterns emerge. The lifecycle improves.

## Quick start

```bash
git clone https://github.com/GadOfir/agent-retro.git
# Drop the skill into your Claude Code skills directory
cp SKILL.md .claude/skills/agent-retro/
```

Then tell your agent:

> **"Run a retrospective on this session."**

The agent self-reports: which step broke, which model was running, which harness was driving it. You triage by model × harness × step. Patterns emerge across sessions.

## What you get

| File | Purpose |
|---|---|
| `index.html` | GitHub Pages landing page |
| `SKILL.md` | The retro skill — agent reads this and fills out what went wrong |
| `NOTES.md` | Accumulated learning log (created on first use) |
| `SMELLS.md` | Confusing code log (created on first use) |

## How it works

1. **Agent finishes a long session** — hours of coding, testing, deploying. Some steps smooth, some rough.
2. **Agent self-reports** — you run the retro skill. The agent fills out what broke: which step, which model, which harness.
3. **You triage** — sort entries across three dimensions: model, harness, task step. Hotspots become visible.
4. **Improve the lifecycle** — route the right model to the right step. Adjust harness config. Next session starts from what the last one learned.

## The triage dimensions

| Dimension | Question | Value |
|---|---|---|
| **Model** | Which AI was running? | "Claude 4 struggles on test generation, GPT-4o invents APIs" |
| **Harness** | Which tool was driving it? | "Same model — Codex got it right, Claude Code missed" |
| **Step** | What was it trying to do? | "Testing stage, refactor stage, deploy stage — each has its own failure pattern" |

The 5 built-in classes (CX-CANDIDATE, VERIFICATION-GAP, AGENT-NOTE, OPERATOR-NOTE, CODE-SMELL) tell you what kind of fix each entry needs. The triage tells you where to aim it.

## Customize me

This skill is a framework. To adapt it to your project:

1. **Map your models and harnesses** — Replace the model/harness examples with the ones you actually use.
2. **Define your step types** — Your project has its own task stages. Add them to the triage.
3. **Adjust the classification** — The 5 classes cover most patterns, but add more if your domain has specific failure modes.

## Troubleshooting

| Problem | Likely cause | Fix |
|---|---|---|
| Retro feels shallow | Agent wasn't given the retro skill to self-report | Make sure SKILL.md is in `.claude/skills/` |
| Pattern not visible yet | Only one session captured | Accumulate 5+ retros. Patterns need volume. |
| Triage feels random | Not logging model/harness consistently | Standardize: every entry gets model + harness + step |
| Same issue keeps recurring | AGENT-NOTE wasn't deduped | NOTES.md auto-dedupes on second occurrence |

## Part of the Kingdom of God

One of the skills in the [Kingdom of God](https://gadofir.github.io/kingdom-of-god/) — a persona-matrix skill router (God → King → Workers). Agent Retro is the learning stage — end-of-session self-report, triaged by model × harness × step.

| Skill | Stage | Link |
|---|---|---|
| Kingdom of God | Router | https://gadofir.github.io/kingdom-of-god/ |
| GodsPlan | Planning | https://gadofir.github.io/godsplan/ |
| CONTRACTX | Contracts | https://gadofir.github.io/contractx-starter/ |
| Shit Hit The Fan | Triage | https://gadofir.github.io/shit-hit-the-fan/ |
| Agent Retro | Learning | https://gadofir.github.io/agent-retro/ |
| TechDebt | Drift | https://gadofir.github.io/techdebt/ |
| LOS | Memory (optional) | https://gadofir.github.io/LOS-starter/ |

Advisory wiring only — if CONTRACTX / TechDebt are installed the retro files into them;
if not, it records findings in your own docs. Works standalone.

### Plug-in skills feed the retro

External skills can plug in to sharpen the retro. Reference them by link (always
latest) and wire them to this stage. Example:
[improve-codebase-architecture](https://github.com/mattpocock/skills/tree/main/skills/engineering/improve-codebase-architecture)
— during the retro the agent references what a good architecture looks like and
checks whether its changes drifted the structure or missed a seam.

## License

MIT
