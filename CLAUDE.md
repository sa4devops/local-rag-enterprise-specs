# CLAUDE.md — Operational Instructions for Claude Code Sessions

> **Operational tooling instructions for Claude Code sessions.**
> **NON-GOVERNING.**
> **Ranks below all governed sources.**
> **Any conflict is resolved in favor of `AUTHORITY.md` and the applicable governing source.**
> **This file does not override the current Owner execution order, its allowed-file list, or its stop conditions.**
> **It creates no authority rank and adds nothing to the governed Reading Matrix.**
> **It does not replace mandatory Tier-0 or task-specific reading.**

**Scope:** how a Claude Code session *operates* inside this repository. It is not a governing text, not a methodology, and not a substitute for reading the governing sources. Where a rule already exists in a governing source, this file refers to it and does not restate it.

---

## 1. Establish the facts before acting

Before any action, determine **from repository evidence** — not from memory, assumption, or a report:

- the **current baseline** (`origin/main` SHA · working-tree state);
- the **applicable governing sources**, in the order fixed by `AUTHORITY.md`;
- the **current Owner order** and its authority;
- the **authorized scope** and the **allowed files**;
- any **conflicts** between sources or with the order;
- material **risks**.

Mandatory reading is set by `methodology/agent-execution-model.md` §9 (Tier-0 + per-phase + per-task). This file adds nothing to it.

## 2. When to proceed automatically

Proceed without asking **only** when the work is **all** of the following:

- **sufficiently clear**;
- **inside the authorized scope**;
- **reversible and reviewable**;
- **consistent with the governing sources**;
- **free from material security, data-loss, architectural, permission, or authority risk**.

**This rule does not select or grant an automation degree.** Automation levels (`L0`..`L3`), protected-path handling, merge patterns, and merge authorization remain governed **exclusively** by `decisions/adr/ADR-0033-automation-levels-git-merge-policy.md` and the current Owner order. Nothing here authorizes a merge, tag, release, or protected-path action.

## 3. Do not stop for low-impact matters

Do **not** raise a Decision Request for cosmetic differences, optional improvements, harmless implementation choices, or low-impact ambiguity — **provided** the chosen interpretation:

- is **disclosed as an assumption** in the execution report;
- is **reversible within the authorized batch**;
- **does not invent Owner authority**;
- **does not expand scope**;
- **does not conflict with a governing source**.

If any one of these fails, it is not a low-impact matter — apply §4.

## 4. Stop before mutation

Stop **before writing** when:

- the repository, baseline, working tree, authorized scope, or allowed paths **cannot be established**;
- **governing sources conflict**;
- the execution order is **materially incomplete or truncated**;
- missing content concerns **authority, scope, baseline, allowed files, a mandatory acceptance criterion, or an irreversible decision**;
- the action is **destructive, irreversible, security-sensitive**, or affects **permissions, secrets, `main`, tags, releases, protected paths, or governing architecture** without the required authorization;
- proceeding would require **inventing Owner authority**.

Report the evidence and stop. Do not silently re-base the order onto a newer baseline.

## 5. No standing correction mandate

**This file creates no permanent consistency-correction authority.**

A required correction that falls **outside the current explicit authorization** requires:

```text
STOP + Decision Request
```

A **bounded** consistency correction is permitted **only** when the current Owner execution order **expressly grants** that authority and **defines its boundaries**. Absent that grant, disclose the defect and stop — do not fix it.

## 6. Report after execution

Every execution round ends with a report stating:

- **files changed**;
- **tests and checks performed**, with their commands and results;
- **material assumptions**;
- **explicitly authorized consistency corrections**, if any;
- **governing conflicts or deviations**;
- **residual risks**.

Evidence requirements are set by `methodology/agent-execution-model.md` §17 — `claimed ≠ published`.

## 7. Review severity is not governing disposition

Review findings may carry a **severity** label:

| Label | Meaning |
|---|---|
| `BLOCKING` | correction required before acceptance |
| `NON-BLOCKING` | recorded; does not require another correction round unless a governing source says otherwise |
| `OPTIONAL` | improvement only |

**These are severity labels only.** They are **not** a disposition system and **do not replace** the exclusive governing batch disposition required by `methodology/PHASE_EXECUTION_STANDARD.md` §3.3:

```text
COMPLETE
GOVERNED TRANSFER
BLOCKING REMAINDER
```

Every finding must still receive **one** governing disposition under §3.3, with:

```text
UNCLASSIFIED = 0
```

The two sets serve different purposes and are **not aliases** of one another.

## 8. Acceptance

Acceptance depends on:

- **satisfaction of all mandatory requirements**;
- **absence of material harm or unresolved blocking remainder**;
- **required evidence and validation**.

**Acceptance does not depend on an estimated or subjective completion percentage.** Mandatory quantitative governing gates remain binding, including:

```text
EC-3 = 100%
```

## 9. What this file cannot override

This file **cannot override**:

- `AUTHORITY.md`;
- any applicable governing source;
- the **current Owner execution order**;
- the **current allowed-file list**;
- the **current stop conditions**;
- `decisions/adr/ADR-0033-automation-levels-git-merge-policy.md`;
- protected-path requirements.

It creates **no** new architecture, methodology, lifecycle, authority vocabulary, or governance layer.

---

**Related:** `AUTHORITY.md` · `constitution.md` · `methodology/PHASE_EXECUTION_STANDARD.md` (§3.3) · `methodology/agent-execution-model.md` (§9 · §15 · §17 · §18) · `decisions/adr/ADR-0033-automation-levels-git-merge-policy.md` · `decisions/open-decisions.md` (`OD-GOV-CLAUDE-1`) · `handoff/handoff.md` · `INDEX.md`
