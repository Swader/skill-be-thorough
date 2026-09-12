## Requirement Completeness Workflow

When the task is based on a source of truth such as a PRD, design doc, audit report, issue, checklist, long prompt, or multi-part request, perform a final completeness check before reporting completion.
For broad PRD/audit/checklist work, maintain a compact source-of-truth ledger while working. The ledger can be in the final report, a local scratch artifact, or an existing project checklist, but it must map each material requirement to `done`, `blocked`, or `intentionally out of scope` with evidence.

Use this loop:

1. Preserve or reconstruct the starting source of truth from the user prompt, linked documents, local files, issue text, PRD, audit report, or acceptance criteria.
2. Build or update the ledger before the final completeness pass. Include requirement id/short label, current status, evidence path or command, and any remaining blocker.
3. Before finalizing, run one subagent when available to re-read that source of truth and compare it with the ledger and actual work. Ask for a binary result: `done` or `not done yet`, plus a concise list of missing or mismatched requirements. The source-of-truth ledger and non-goals are immutable review boundaries.
4. If the subagent says `not done yet`, resume implementation and complete the outstanding parts.
5. Re-run local verification and the coding audit loop for any new coding pass.
6. Run one targeted completeness re-check after the fixes.
7. If it still returns `not done yet`, identify the exact unmet acceptance criterion or report the blocker; do not broaden into adjacent improvements.

Do not treat partial compliance, "close enough", or unverified assumptions as complete. If a requirement is impossible, obsolete, contradictory, or intentionally out of scope, document the reason and get as close to the requested outcome as the available tools and constraints allow.
If an earlier report says the work is "not done" but the tree may have changed since, verify against the current head and update the ledger before accepting the older status.
