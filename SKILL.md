---
name: be-thorough
description: For requested rigor or full-clip work, verify requirements and complete a bounded independent review.
---

# Be Thorough

“Done” requires evidence against the user's requested outcome. Thoroughness means deeper verification within scope, not a wider assignment. Complete admitted work or report the exact blocker and remaining requirements. Explicit user exceptions still govern the task.

## Scope and completion

Before substantial edits, record the outcome, acceptance criteria, non-goals, and expected footprint. Reuse the current task contract and review receipts when another skill already established them.

Classify findings as mission blockers, patch regressions, mandatory safety issues, follow-ups, or non-findings. Only the first three can expand current work. Report useful unrelated improvements without implementing them.

Reassess if a hotfix approaches five files or 150 non-generated lines, exceeds roughly twice its estimate, or adds an unplanned schema, durable queue/state, scheduler, state machine, protocol, recovery mechanism, or generic framework. Preserve the attempt and find the smallest coherent design. These are tripwires, not hard limits; ask before genuinely broadening the authorized mission.

Choose the detailed workflow for the actual deliverable:
- Code changes: read [coding review](references/coding.md).
- Multi-part requirements, PRDs, audits, or comprehensive requests: read [requirement completeness](references/requirements.md). Keep a ledger mapping each requirement to done, blocked, or intentionally out of scope with evidence.
- UI work: read [rendered UI review](references/ui.md), including relevant state, accessibility, viewport, and persona checks.

Do not load unrelated workflows. A matching verification or review already completed for the current change can satisfy this skill; do not repeat it just because another skill requests the same gate.

## Evidence and independent review

Use checks that match the risk: focused code checks, rendered UI inspection, parsed/rendered artifacts, or the actual runtime interface. Fix failures caused by the requested change and re-run the check that exposed them. A successful command alone does not prove the user journey works.

Use one independent reviewer by default when available, on the highest available model. Give it the requirements and current evidence without your intended conclusion. Add reviewers only for a demonstrated high-stakes boundary or explicit request. Require concrete evidence, classify each finding, and resolve admitted issues. After fixes, re-check affected work and run one targeted re-review, followed by a final main-thread pass. Do not restart broad review unless the mission changed.

If delegation is unavailable, perform an explicit main-thread review and disclose that limit. A separate agent is useful scrutiny, not proof against shared model blind spots.

## Canary execution

The stronger model that started the task plans the canary and assesses its evidence. Delegate execution to a weaker model. Give it a compact brief with the exact release, owned fixtures, allowed actions, required checks, stop conditions, and cleanup. Do not fork the full task history. This selects the canary operator model; it does not change the system's live model or expand permission for production actions.

In the Codex app, use Luna in a separate, sidebar-visible task created with `create_thread`. Put it in the **Canary** section, creating that section only if missing, and link the task from the parent. Reuse the task for related retries. Do not run the canary in a hidden subagent or the stronger parent. If Luna or the required sidebar controls are unavailable, report the blocker instead of silently substituting.

In another harness with different models, use an available model weaker than the initiating model. Run it in a separate task or agent that follows the stronger model's brief. If the harness cannot delegate to a weaker model, report that limitation.

Keep one canary owner and watcher. Return final evidence or an actionable blocker once; avoid routine acknowledgements, relayed status updates, and duplicate checks after handoff. The stronger model resolves failures and decides whether the evidence meets the task's acceptance criteria.

## Reporting gate

Finish only when relevant verification has passed or its limits are explicit, no admitted finding remains, any ledger required by the selected workflow is complete, and changed files are intentional. A blocked requirement must identify the exact missing input or external condition; complete the independent work that remains possible.

For UI, rendered behavior must pass the applicable review. For user-visible writing, prefer direct, specific language and readable structure; revise filler and dense prose. Use humanizer only when a substantial editorial pass is warranted. An internal writing score is not evidence of user comprehension.

Report the result, why it changed, validation, and remaining limits. Companion skills are optional; discover or recommend one only when a concrete missing capability affects the task.
