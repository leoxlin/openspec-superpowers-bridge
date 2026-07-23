# CLAUDE.md

> Contextual guidance for Claude Code when working in this repository. Write in English.
>
> For what this repository is, why it exists, and which bridges it contains, see [README.md](./README.md).
> This file focuses on the **conventions and red flags** Claude needs to know when working in this repository.

---

## Structure Conventions

```
openspec-schemas/                     ← this repository
├── README.md                         ← English, rendered by default on GitHub
├── CLAUDE.md                         ← the file you are reading
├── LICENSE                           ← MIT
├── .gitignore
├── .github/workflows/
│   ├── validate-schemas.yml          ← CI runs openspec schema validate for each bridge
│   └── version-check.yml             ← checks upstream OpenSpec / Superpowers weekly and opens an issue when behind
├── docs/
│   ├── roadmap.md                    ← public roadmap
│   └── superpowers/
│       ├── specs/                    ← design specs (brainstorming output)
│       └── plans/                    ← implementation plans (writing-plans output)
└── superpowers-bridge/               ← first bridge, a self-contained schema bundle
    ├── README.md                     ← complete bridge documentation (including install and integration runbook)
    ├── schema.yaml                   ← schema definition read by OpenSpec
    └── templates/                    ← artifact templates
        ├── brainstorm.md
        ├── proposal.md
        ├── design.md
        ├── spec.md
        ├── tasks.md
        ├── plan.md
        ├── verify.md
        └── retrospective.md
```

To add a bridge in the future, create a `<new-bridge>/` subdirectory at the repository root with the same structure as `superpowers-bridge/`. Add one line to `matrix.bridge` in `.github/workflows/validate-schemas.yml`.

## Naming Conventions

- **Repository / directory / schema name**: lowercase + hyphens + correct singular or plural form
  - repository: `openspec-schemas` (plural, because it can contain multiple bridges)
  - bridge directory / schema name: `superpowers-bridge` (singular)
  - Do not use PascalCase. Although OpenSpec's own repository uses `OpenSpec`, its CLI and npm package are lowercase, so functional names follow that convention.
## Language Strategy

| File type | Language |
|---------|------|
| Entry-point `README.md` | English canonical |
| `CLAUDE.md` (this file) | English |
| `docs/roadmap.md` | English canonical |
| `superpowers-bridge/README.md` | English canonical |
| `schema.yaml`, `templates/*.md` | English (machine-readable and accessible to international readers) |
| Commit messages | English |
| Code comments | English |

## Schema Modification Workflow

1. Edit `<bridge>/schema.yaml` or `<bridge>/templates/*.md`.
2. Validate locally:
   ```bash
   mkdir -p /tmp/test-project/openspec/schemas
   cp -R <bridge>/ /tmp/test-project/openspec/schemas/
   cd /tmp/test-project
   openspec schema validate <bridge-name>
   openspec schemas
   ```
3. If timing mismatches or error behavior change, **also update the "Six design touchpoints worth remembering" section in `superpowers-bridge/README.md`**, especially the verify/retrospective timing-mismatch subsection.
4. Write commit messages in English and follow Conventional Commits (`feat:`, `fix:`, `refactor:`, `chore:`, `docs:`, `ci:`).
5. Push to trigger CI.

## Responses to the Three alfred-openspec Concerns

The PR #970 review raised three concerns, each addressed concretely in schema v1. Claude must remember them before changing any schema behavior in this repository:

| Concern | Response |
|------|------|
| #3 Proactively committing to the user's Git repository | **Removed entirely.** Step 0 became a skill PRECHECK that validates skills without modifying Git. |
| #1 Tight coupling to Superpowers without capability detection | **Layer 1**: begin every skill-invoking instruction with a PRECHECK and STOP when the skill is unavailable. **Layer 2**: add evidence-based PRECHECKs to verify / retrospective (`git log` and `grep` inspect observable state). |
| #2 Verify timing mismatch (and the same issue for retrospective) | Known limitation documented in bridge README design touchpoint #6. The complete fix requires the OpenSpec engine to introduce a `post_apply` phase. The Layer 2 evidence-based PRECHECK is the current mitigation. |

**Red flags when modifying the schema** — **do not** do the following, because they would undo the responses to PR #970:

- ❌ Add instructions to proactively run `git add` or `git commit`.
- ❌ Remove a PRECHECK without replacing it with a stronger alternative.
- ❌ Remove verify / retrospective as artifacts without updating the limitation in the README design-touchpoint section.
- ❌ Change the schema name without synchronizing all bridge documentation and the bridge index in the top-level README.

## Related Links

- Design spec: [`docs/superpowers/specs/2026-05-02-openspec-schemas-monorepo-design.md`](./docs/superpowers/specs/2026-05-02-openspec-schemas-monorepo-design.md)
- Implementation plan: [`docs/superpowers/plans/2026-05-02-phase-1-implementation.md`](./docs/superpowers/plans/2026-05-02-phase-1-implementation.md)
- PR #970 review: <https://github.com/Fission-AI/OpenSpec/pull/970>
- Existing spec-kit Superpowers bridge references:
  - [RbBtSn0w/spec-kit-extensions/superpowers-bridge](https://github.com/RbBtSn0w/spec-kit-extensions/tree/main/superpowers-bridge)
  - [WangX0111/superspec](https://github.com/WangX0111/superspec)
