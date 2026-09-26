# Codex Memory Workflow Skill

A portable Codex Skill for configuring an Obsidian-compatible Markdown memory vault, scoped global routing, and Native scheduled maintenance.

## Install

Copy the entire `codex-memory-workflow` folder into one Skill directory.

Codex user directory:

```text
~/.codex/skills/codex-memory-workflow/
```

Cross-runtime directory:

```text
~/.agents/skills/codex-memory-workflow/
```

PowerShell example, run from the directory containing this folder. It creates the parent directory but stops if the target Skill folder already exists:

```powershell
$skillsDir = Join-Path $env:USERPROFILE '.codex\skills'
$target = Join-Path $skillsDir 'codex-memory-workflow'
New-Item -ItemType Directory -Force -Path $skillsDir | Out-Null
if (Test-Path -LiteralPath $target) { throw "Target already exists: $target" }
Copy-Item -Recurse -LiteralPath '.\codex-memory-workflow' -Destination $target
```

POSIX shell example with the same no-overwrite behavior:

```sh
skills_dir="$HOME/.codex/skills"
target="$skills_dir/codex-memory-workflow"
mkdir -p "$skills_dir"
test ! -e "$target" || { printf 'Target already exists: %s\n' "$target" >&2; exit 1; }
cp -R ./codex-memory-workflow "$target"
```

If the target already exists, audit or update that installation explicitly instead of copying over it.

Restart or reload Codex if the installed Skill is not discovered immediately.

## Use

Explicit invocation:

```text
$codex-memory-workflow Configure this project using the portable defaults.
```

Useful requests:

- Audit my existing Codex memory workflow without changing it.
- Configure the vault at a specific absolute path.
- Repair missing templates but preserve all existing notes.
- Configure different daily and weekly times.

Default configuration:

- Vault: `<current-project-root>/codex-memory`
- Daily maintenance: local 22:00
- Weekly maintenance: local Sunday 22:30

## What configuration can change

Only an explicit install, configure, repair, or migrate request authorizes changes. Depending on the request and available capabilities, Codex may create missing vault files, append one managed global routing block, and create or reuse two project-scoped Native scheduled tasks.

Existing notes are not overwritten. Equivalent global rules and matching scheduled tasks are not duplicated.

## Remove

Removing this Skill folder disables future discovery only. It does not delete a vault, global routing block, or scheduled task. Ask Codex to audit those items and name the exact removal targets before removing them separately.

## Limits

Native scheduled tasks depend on the local Codex environment and machine availability. A valid configuration does not prove that a future scheduled run occurred.
