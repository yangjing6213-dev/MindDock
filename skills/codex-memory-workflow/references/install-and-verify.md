# Install, Configure, and Verify

Read this reference for installation paths, Native task creation, duplicate detection, fallback behavior, verification, or removal.

## Skill installation

Install the complete folder as either:

- `~/.codex/skills/codex-memory-workflow/`
- `~/.agents/skills/codex-memory-workflow/`

`SKILL.md` must remain at the folder root. Installation does not authorize vault, global configuration, or automation changes; the user's current request determines that scope.

## Configuration sequence

1. Classify the request as read-only audit or authorized install/configure/repair/migrate work.
2. Resolve `<PROJECT_ROOT>`, `<VAULT_ROOT>`, effective user-level `AGENTS.md`, local timezone, and requested schedules.
3. Inspect the target vault and equivalent global rule before writing.
4. Create missing vault files from `vault-layout.md`; never replace an existing note.
5. Append the marked global rule only when no equivalent marked or unmarked rule exists.
6. Inspect existing scheduled tasks before creating or updating anything.
7. Verify files, routing, task scope, and final status.

## Native scheduled tasks

Use the Codex app's Native automation capability when available. Both tasks are local, active, and bound to the selected project only.

| Field | Daily | Weekly |
|---|---|---|
| Suggested name | `Codex memory daily consolidation` | `Codex memory weekly maintenance` |
| Default schedule | `FREQ=DAILY;BYHOUR=22;BYMINUTE=0;BYSECOND=0` | `FREQ=WEEKLY;BYDAY=SU;BYHOUR=22;BYMINUTE=30;BYSECOND=0` |
| Timezone | User's local timezone | User's local timezone |
| Prompt source | `daily-prompt.md` | `weekly-prompt.md` |
| Execution | Local selected project | Local selected project |

Duplicate and conflict handling:

- Same name, project, vault path, purpose, and schedule: reuse the existing task and report its real ID; otherwise it is not a match.
- Same name or purpose with a different project, vault path, or schedule: treat it as a conflict; preserve the task and do not create a disguised duplicate.
- Applying or matching the Skill defaults does not authorize changing an existing task. Report the conflict and require a separate explicit request that identifies the exact task and requested change.
- Never edit internal automation files directly when a Native task API is available.

## Manual fallback

If the Native automation API, project ID, or task registry is unavailable:

- Complete and verify the vault and global routing layers that remain accessible.
- Do not create a replacement daemon, operating-system scheduler, or plugin.
- Report overall `PARTIAL`, automation `NOT_RUN`, and task IDs as unavailable.
- Provide the exact names, schedules, local project, resolved vault path, and prompt-source references from the table above so the user can configure them later.

## Verification

Run checks proportional to the requested layers:

- Required vault files exist at the resolved path.
- The index states scoped reading, conflict precedence, and inbox-first promotion.
- Existing notes remain intact; only missing files were created.
- Exactly one equivalent global rule exists, or a conflict is reported.
- Exactly one matching daily task and one matching weekly task exist when automation was requested and available.
- Task project, vault path, schedule, status, and prompt boundaries match the request.
- Package or generated content contains no real credentials, private keys, account data, session database copy instructions, or complete chat dumps.
- Review repository status for unrelated changes.

Status contract:

- `PASS`: every requested layer exists and its applicable checks passed.
- `PARTIAL`: safe layers were completed but another requested layer, commonly Native automation, is unavailable or conflicted.
- `FAIL`: a verification ran and demonstrated an unsatisfied requirement.
- `BLOCKED`: a concrete permission, path, or environment condition prevents meaningful progress.

A configured schedule is not evidence that a future run executed. State that runtime execution remains unverified until an actual run is observed.

## Removal

Removing the Skill folder affects discovery only. Vault files, global routing rules, and Native tasks are separate user data and configuration. Remove any of them only after a new explicit request identifies the exact target; do not couple data deletion to Skill uninstall.
