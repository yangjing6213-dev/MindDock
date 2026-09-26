# Weekly Maintenance Prompt

Read this reference only when configuring, repairing, or auditing the weekly Native task. Replace `<VAULT_ROOT>` with the resolved absolute vault path.

Default schedule: local Sunday 22:30.

```text
Run one local weekly maintenance pass for <VAULT_ROOT>.

Scope:
- Process only indexes, project entrypoints, and derived summaries inside <VAULT_ROOT>.
- Do not scan other projects, session databases, complete chat history, or external accounts.

Rules:
1. Repair broken links in 00-index.md and project indexes when the correct target is unambiguous.
2. Record superseded decisions only in indexes or derived summaries, preserving the original decision file and linking to its replacement.
3. Merge only fully duplicate derived summaries. Never merge or delete raw daily records or original candidates.
4. List conflicts, uncertain states, stale candidates, and items requiring human confirmation.
5. Do not delete, overwrite, or silently reinterpret history. When uncertain, leave the item unchanged.
6. Report only actionable changes or blockers. Stay quiet when nothing actionable changed.
```

Do not weaken these boundaries when translating the prompt into an automation tool's input format.
