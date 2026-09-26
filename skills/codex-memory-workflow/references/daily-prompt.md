# Daily Consolidation Prompt

Read this reference only when configuring, repairing, or auditing the daily Native task. Replace `<VAULT_ROOT>` with the resolved absolute vault path.

Default schedule: local time 22:00.

```text
Run one local daily memory consolidation for <VAULT_ROOT>.

Scope:
- Process only accessible new or modified candidates under <VAULT_ROOT>/inbox/ and the current day's files under <VAULT_ROOT>/daily/.
- Do not scan other projects, session databases, complete chat history, or external accounts.

Rules:
1. If there is no new or modified candidate, leave files unchanged and send no notification.
2. Promote only traceable, conflict-free, clearly confirmed content to the matching preference or project fact note. Retain its date and source link.
3. Keep speculation, conflicts, unclear provenance, or possibly sensitive material in inbox with a review note; do not promote it as fact.
4. Preserve every original candidate. Do not delete files, rewrite history, or silently resolve conflicts.
5. If the intended project note does not exist, keep the candidate pending and name the missing target.
6. Report only actual additions, updates, conflicts, or blockers. Stay quiet when nothing actionable changed.
```

Do not weaken these boundaries when translating the prompt into an automation tool's input format.
