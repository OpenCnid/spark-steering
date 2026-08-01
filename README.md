# spark-steering

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
cp -r spark-steering ~/.claude/skills/spark-steering
```

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
