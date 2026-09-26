# MindDock

> A reviewable, backup-friendly, portable memory workflow for AI agents and AI creators.

[中文说明](README.md)

MindDock turns project knowledge, stable preferences, pending candidates, and daily records into ordinary Markdown files. Codex can read the relevant context on demand, while people can open, inspect, and back up the vault directly with Obsidian.

This is not a promise of magical “permanent memory”. It is a bounded workflow: durable information enters `inbox/`, important facts keep their provenance, conflicts stay pending for human review, and Native scheduled maintenance is used only when the local capability is available.

## What it provides

- A project-scoped `codex-memory/` vault rooted at the current project by default.
- Obsidian-compatible Markdown without a database or dedicated plugin.
- An inbox-first path for promoting confirmed facts, preferences, and decisions.
- A global `AGENTS.md` routing block so Codex can load the right project memory.
- Native daily and weekly maintenance, with an honest `PARTIAL` fallback when scheduling is unavailable.
- Idempotent setup that preserves existing notes, equivalent rules, and conflicting tasks.

## Quick start

### 1. Install the Skill

PowerShell:

```powershell
$skillsDir = Join-Path $env:USERPROFILE '.codex\skills'
New-Item -ItemType Directory -Force -Path $skillsDir | Out-Null
Copy-Item -Recurse -LiteralPath '.\skills\codex-memory-workflow' -Destination (Join-Path $skillsDir 'codex-memory-workflow')
```

POSIX shell:

```sh
mkdir -p "$HOME/.codex/skills"
cp -R ./skills/codex-memory-workflow "$HOME/.codex/skills/codex-memory-workflow"
```

If the target folder already exists, audit the current installation before choosing to update it. Do not overwrite it blindly.

### 2. Invoke it

```text
$codex-memory-workflow Configure this project using the portable defaults.
```

Defaults:

- Vault: `<current-project-root>/codex-memory`
- Daily maintenance: local time 22:00
- Weekly maintenance: local Sunday 22:30
- New durable information: `inbox/` first

### 3. Read the Skill references

- [Skill entrypoint](skills/codex-memory-workflow/SKILL.md)
- [Install and verify](skills/codex-memory-workflow/README.md)
- [Vault layout and routing](skills/codex-memory-workflow/references/vault-layout.md)
- [Daily prompt](skills/codex-memory-workflow/references/daily-prompt.md)
- [Weekly prompt](skills/codex-memory-workflow/references/weekly-prompt.md)
- [Native configuration and fallback](skills/codex-memory-workflow/references/install-and-verify.md)

## Safety boundaries

MindDock does not read or copy Codex session databases, complete chat histories, secrets, cookies, certificates, customer-sensitive data, or external account data. It does not create a replacement daemon or pretend that an external vault is Codex native Memories.

A configured schedule is not proof that a future run has executed. Observe and verify the first Native run in your own Codex environment.

## About the author

Enhe is a product designer, solo-company practitioner, and AI Builder exploring how AI can help create more capable and freer personal work systems.

![About the author: Enhe](assets/about-author.png)

Asset notice: `assets/about-author.png` is a portrait and brand asset included with the author's permission for display in this project. It is not covered by the MIT License and may not be reused without permission.

## License

The Skill, Markdown documentation, prompts, and templates in this repository are released under the [MIT License](LICENSE). `assets/about-author.png` is excluded from that license grant.

## Why the name MindDock

MindDock combines “Mind” and “Dock”: a clear place where project knowledge, AI agents, and creator workflows can connect, accumulate, and stay ready for the next task.
