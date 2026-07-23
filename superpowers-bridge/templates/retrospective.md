# Retrospective: <change-name>

> Written: <YYYY-MM-DD> (after verify passed)
> Commit range: `<base-sha>..<head-sha>`
> Worktree: <path or "merged to main">

---

## 0. Evidence

> Quantitative baseline data — later Wins / Misses bullets can refer to it directly instead of repeating [evidence: ...] on every line.
> In a cold-writing scenario (the retrospective is written some time after the cycle ends), `git log` + `tasks.md` +
> commit messages alone should be sufficient to reconstruct this section.

- **Commit range**: `<base-sha>..<head-sha>` (<n> commits)
- **Diff size**: <+X / -Y lines across N files>
- **Tasks done**: <x>/<y> (`grep -cE '^\s*- \[x\]' tasks.md` → x; the regex allows subtask indentation)
- **Active hours**: <estimate>
- **Subagent dispatches**: <count or "n/a">
- **New external dependencies**: <list, with license + version, or "none">
- **Bugs encountered post-merge**: <count, one-line each, or "none">
- **OpenSpec validate state at archive**: <pass / fail / not-run>
- **Test coverage signal**: <e.g. jacoco %, pytest count, vitest count, or "n/a">

Commit chain (chronological):

```
<base-sha> <one-line summary>
...
<head-sha> <archive commit one-line>
```

---

## 1. Wins

- [evidence: <commit/file/test>] <description>

## 2. Misses

- 🔴 [blocking | evidence: ...] <description>
- 🟡 [painful  | evidence: ...] <description>
- 📌 [nit      | evidence: ...] <description>

## 3. Plan deviations

| Plan task | What changed | Why |
|-----------|--------------|-----|
| 1.2       | ...          | ... |

## 4. Skill / workflow compliance

| Skill                                            | Used |
|--------------------------------------------------|------|
| superpowers:brainstorming                        |      |
| superpowers:writing-plans                        |      |
| superpowers:using-git-worktrees                  |      |
| superpowers:subagent-driven-development          |      |
| (transitive) superpowers:test-driven-development |      |
| (transitive) superpowers:requesting-code-review  |      |
| superpowers:finishing-a-development-branch       |      |

> **Default expectation**: all ✓. Every skill is part of the schema design;
> skipping one is exceptional. Every ✗ must include a reason and prevention plan
> in the `### Deliberately Skipped Skills` subsection below.

### Deliberately Skipped Skills

> Skipping a skill is a designed escape hatch, not the normal path. Every ✗ must answer the three questions below;
> an empty section (all green) is the expected state.

- **`<skill name>`**
  - **What was skipped**: <whether the entire skill or a particular substep was skipped>
  - **Why this cycle**: <specific cycle conditions — do not use vague reasons such as "not needed," "too small," "no time," "blocked by an external dependency," or "the skill output looked wrong"; provide the actual trigger (a specific commit, log line, or observed behavior)>
  - **How to prevent recurrence**: How will the same conditions be handled without skipping in the next cycle? Choose one:
    - `schema graph fix` — identify the exact section of schema.yaml to change
    - `skill description tightening` — identify the exact skill frontmatter / instruction to change
    - `CLAUDE.md trigger` — specify the interpretation rule to add to the adopter CLAUDE.md.fragment
    - `scope-judgment rule` — specify how the cycle's scope should be interpreted
    - `one-off — schema boundary case, no prevention possible` — explain explicitly why it is a boundary case (vague reservations are not accepted)

> **Relationship to §6 Promote candidates**: if multiple cycles produce the same `How to prevent`
> answer for the same skill, promote that pattern to §6 and directly trigger a schema / skill PR rather than allowing it to become normal.

## 5. Surprises

- <assumption that turned out wrong>

## 6. Promote candidates → long-term learning

Use a `- [ ]` checklist for each candidate:

- Title: severity emoji (🔴/🟡/📌) + a one-sentence learning
- `→ **Promote to** <destination>`(memory / CLAUDE.md / schema / skill / one-off)
- Two-line body (matching the Superpowers feedback-memory body schema):
  - `> **Why**: <reason; often a past incident or strong preference>`
  - `> **How to apply**: <when/where this guidance kicks in>`

An unchecked `- [ ]` means the candidate has not yet been promoted. Carry it into the next cycle's retrospective for reevaluation,
or retain it as an observation across cycles.

> **Carry-forward mechanism**: when writing the next cycle's retrospective, run
> `grep -A 5 '^- \[ \]' openspec/changes/archive/*/retrospective.md` to retrieve
> previous unchecked candidates. Decide individually whether to carry each one into this cycle's §6, promote it immediately,
> or mark it stale and stop tracking it.

Examples:

- [ ] 🔴 **<short rule>** → **Promote to memory** (type: feedback)
  > **Why**: <past incident or strong preference that motivated this rule>
  > **How to apply**: <which file / cycle phase / decision moment this kicks in>

- [ ] 🟡 **<another candidate>** → **Promote to project CLAUDE.md** (`<path/to/CLAUDE.md>` section)
  > **Why**: ...
  > **How to apply**: ...

- [ ] 📌 **<third candidate>** → **One-off** (record only; do not promote)
  > **Why**: <why it doesn't generalize>
