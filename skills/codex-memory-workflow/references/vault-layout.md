# Vault Layout and Routing

Read this reference when creating, repairing, migrating, or auditing vault files or the global `AGENTS.md` routing block.

## Resolve paths

- `<PROJECT_ROOT>`: the current project root. Prefer the repository root when the task is inside a repository; otherwise use the current project directory.
- `<VAULT_ROOT>`: an explicit user path, or `<PROJECT_ROOT>/codex-memory` when no path was supplied.
- Resolve an absolute `<VAULT_ROOT>` before editing. Do not guess a drive, username, or home directory.

## Create missing files only

```text
<VAULT_ROOT>/
├── 00-index.md
├── README.md
├── user/preferences.md
├── projects/README.md
├── inbox/README.md
├── daily/README.md
├── archive/README.md
└── templates/decision.md
```

If a target exists, preserve it. If its content conflicts with this model, report the conflict and continue only with unrelated missing files.

## Minimal file templates

### `README.md`

```markdown
# Codex Memory

This Obsidian-compatible Markdown vault stores reviewable project facts, decisions, stable preferences, candidates, daily records, and archives. Start at [00-index.md](00-index.md).

Do not store credentials, private account data, customer-sensitive material, or complete chat dumps.
```

### `00-index.md`

```markdown
# Codex Memory Index

## Read order
1. The user's current request.
2. Applicable global and project `AGENTS.md` files.
3. This index.
4. Notes linked to the current project and task.
5. `daily/` or `archive/` only when traceability requires them.

Do not scan the whole vault for completeness.

## Conflict precedence
Current explicit request > latest explicit project decision > project fact source > global preference > Codex Memories > unconfirmed candidate.

## Entrypoints
- [Stable preferences](user/preferences.md)
- [Projects](projects/README.md)
- [Pending candidates](inbox/README.md)
- [Daily records](daily/README.md)
- [Archive](archive/README.md)

New durable information enters `inbox/` before promotion. Preserve raw records and leave conflicts pending for human review.
```

### Supporting index files

Use one heading and a short scope statement in each file:

- `user/preferences.md`: confirmed stable preferences only, each with date and source.
- `projects/README.md`: links to project-specific overview, status, and decisions.
- `inbox/README.md`: pending candidates are not authoritative and must retain provenance.
- `daily/README.md`: dated activity records are raw history, not automatically canonical facts.
- `archive/README.md`: archived records remain available and are not deletion targets.

### `templates/decision.md`

```markdown
---
status: proposed
date: YYYY-MM-DD
project: project-id
source: source-link-or-description
supersedes:
---

# Decision

## Context

## Decision

## Consequences

## Review notes
```

## Managed global rule

Append this block to the effective user-level `AGENTS.md` only when no equivalent rule exists. Replace `<VAULT_ROOT>` with the resolved absolute path.

```markdown
<!-- codex-memory-workflow:start -->
## Codex memory workflow
- External knowledge entry: `<VAULT_ROOT>/00-index.md`. It complements rather than replaces Codex Memories.
- At task start, read the current request and applicable `AGENTS.md`, then the index and only notes relevant to the current project or task.
- Put new durable facts, preferences, and decisions in `<VAULT_ROOT>/inbox/` before promotion.
- Conflict precedence: current explicit request > latest explicit project decision > project fact source > global preference > Codex Memories > unconfirmed candidate.
- Never store credentials, private account data, customer-sensitive material, session databases, or complete chat dumps.
- Daily and weekly maintenance preserve raw records and do not silently resolve conflicts.
<!-- codex-memory-workflow:end -->
```

Idempotency rules:

- Existing start/end markers: verify the block; change it only when the user requested repair or migration.
- Equivalent unmarked rule containing the same vault path, scoped reading, inbox-first writes, and sensitive-data boundary: treat it as installed and do not append or wrap it.
- Multiple conflicting rules: stop global-rule changes and report `PARTIAL` with the conflicting locations.
