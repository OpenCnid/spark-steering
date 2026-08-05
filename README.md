# spark-steering

> [!IMPORTANT]
> **This repository has moved into [OpenCnid/dovetail](https://github.com/OpenCnid/dovetail).**
>
> `spark-steering` is now one of nine skills in that pack, at
> [`skills/spark-steering/`](https://github.com/OpenCnid/dovetail/tree/main/skills/spark-steering).
> Install the whole pack with a plain clone — there are no submodules:
>
> ```bash
> git clone https://github.com/OpenCnid/dovetail.git
> cd dovetail && bash scripts/install.sh
> ```
>
> The eight skills were separate repositories while each was developed on its
> own. They are used together, so they are now maintained together; keeping them
> apart cost a pin-bumping step before every change and bought nothing a reader
> could see. This repository is archived and read-only. Its history is the record
> of how this skill got here, and `docs/provenance.md` in dovetail names the
> commit its content arrived at.


*Diagnose which capability axis is actually short before reaching for a fix.*

[![license](https://img.shields.io/badge/license-CC_BY_4.0-3b7ddd)](LICENSE.md)
![invocation](https://img.shields.io/badge/invocation-manual_only-d97757)

A Claude Code skill for the moment something is not working and you are about to
install something to fix it.

## The problem

A wrong-axis fix does not merely fail. **It stays installed and charges rent
every turn** — a permanent config change that never touches the actual gap, plus
the cost of carrying it forever.

So the move is to name the axis first. SPARK, after
[arXiv:2508.01581](https://arxiv.org/abs/2508.01581):

| axis | short means |
|---|---|
| **S**kills | the capability is absent |
| **P**ersonalities | the disposition is wrong for the work |
| **A**pproaches | the ordering or method is wrong |
| **R**esources | the tool or connector does not exist |
| **K**nowledge | the information exists and was not retrieved |

## The cheapest lever has no surface

> **Ask first — the un-tool.** Declining to call anything, and instead putting
> the question to the user, is a move with no schema, no install, and no
> recurring cost. It is easy to miss precisely because it has no surface.
>
> Reach for it **before** any lever that installs permanent configuration — it
> resolves ambiguity at the source instead of routing around it.

Other skills in this stack cite that section as the destination for a held
expectation, which is the one thing that must never go into a player prompt.

## Rule out the adjacent axis

A confident diagnosis on the wrong axis is worse than none. The gates that
matter most:

- **S vs R** — "I can't do this," with the tool already in the roster and already
  called, is S (weak result), not R (missing resource).
- **R vs K** — a query returning nothing looks like "the resource doesn't exist"
  when it is a retrieval-formulation gap. Reissue with different terms first.
- **P vs A** — a pause to ask gets "fixed" by reordering steps when the real
  issue is whether the question should have interrupted at all.

## Invocation

This skill is **manual-invoke only** (`disable-model-invocation`). It does not
fire on its own, by design: a diagnostic that volunteers itself becomes a tax on
every turn, which is the failure mode it exists to prevent.

## Install

```bash
git clone https://github.com/OpenCnid/spark-steering.git
mkdir -p ~/.claude/skills
cp -r spark-steering/skills/spark-steering ~/.claude/skills/
```

> **The `mkdir -p` is load-bearing — do not drop it as noise.** If
> `~/.claude/skills/` does not exist yet, which is the state of anyone who has
> never installed a skill, `cp` reads the trailing path as a rename target and
> writes `~/.claude/skills/SKILL.md` with no skill directory at all. Exit code
> 0, no output, no error. The skill never loads and nothing says why — and
> because this one is manual-invoke only, you never see it fail to fire. You
> just find the slash command missing.

On PowerShell:

```powershell
git clone https://github.com/OpenCnid/spark-steering.git
New-Item -ItemType Directory -Force ~/.claude/skills
Copy-Item -Recurse -Force spark-steering/skills/spark-steering ~/.claude/skills/
```

`-Force` on the copy is what makes a re-run an upgrade instead of an "item with
the specified name already exists" failure.

If `CLAUDE_CONFIG_DIR` is set it replaces `~/.claude` as the skills root, so
install into `$CLAUDE_CONFIG_DIR/skills` instead.

Or install it with the rest of the stack:
[OpenCnid/dovetail](https://github.com/OpenCnid/dovetail).

## What is not in this repository

The costed levers and cost classes live in `references/`. The **373-primitive
map of Claude Code surfaces** that backs the axis definitions is kept outside
this repository with the research paper it belongs to, so the `references/`
files cite a corpus a reader here cannot open. That is stated rather than hidden;
the judgment in the body stands on its own.

## License

Prose and skill: [CC BY 4.0](LICENSE.md) © OpenCnid Labs. The SPARK framing is
from arXiv:2508.01581, credited above.
