---
name: codex-memory-workflow
description: Use when a user wants to install, configure, repair, audit, or migrate a Codex memory workflow backed by an Obsidian-compatible Markdown vault and Native scheduled tasks, especially when paths, existing notes, global AGENTS.md rules, duplicate automations, or unavailable scheduling capabilities must be handled safely.
---

# Codex Memory Workflow

## Overview

Configure a portable, reviewable external memory layer for Codex. The Markdown vault is a project fact source; it complements rather than replaces Codex Memories.

## Intent Gate

- Analysis, explanation, or audit request: remain read-only.
- Install, configure, repair, or migrate request: make only the requested local changes.
- If the target project root cannot be resolved, ask one path question before writing.

## Portable Defaults

| Setting | Default |
|---|---|
| Vault | `<current-project-root>/codex-memory` |
| Daily task | Local time 22:00 |
| Weekly task | Local Sunday 22:30 |
| New durable information | `inbox/` first |
| Existing files | Preserve; create missing files only |

An explicit user path or schedule overrides these defaults.

## Workflow

1. Read applicable `AGENTS.md`, then inspect only the target vault, equivalent global memory rule, and matching automations.
2. For vault files and the managed global rule, read [references/vault-layout.md](references/vault-layout.md). Never overwrite an existing note. Treat an equivalent unmarked rule as already installed.
3. When daily scheduling is in scope, read [references/daily-prompt.md](references/daily-prompt.md). For weekly scheduling, read [references/weekly-prompt.md](references/weekly-prompt.md).
4. For installation locations, duplicate detection, Native task parameters, fallback, verification, or removal, read [references/install-and-verify.md](references/install-and-verify.md).
5. Verify observable state and report `PASS`, `PARTIAL`, `FAIL`, or `BLOCKED`. Automation configuration is not runtime execution evidence.

## Safety Boundaries

- Do not read or copy session databases, full chat histories, credentials, cookies, certificates, customer data, or unrelated projects.
- Preserve raw candidates and history. Conflicts stay pending until a person resolves them.
- Do not create a replacement daemon, database, plugin, or cloud sync service when Native scheduling is unavailable.
- Never invent project IDs, task IDs, successful writes, or test results.

## Common Mistakes

- Defaulting to the user home directory instead of the current project root.
- Inventing a new schedule instead of using 22:00 and Sunday 22:30.
- Adding a second global rule because the equivalent existing rule lacks markers.
- Calling setup `PASS` when scheduled tasks were not created or verified.

## Example

For “configure this project with defaults,” resolve the project root, use `<project>/codex-memory`, preserve existing files, configure daily 22:00 and Sunday 22:30 local tasks when Native automation is available, and report any unavailable layer as `PARTIAL`.
