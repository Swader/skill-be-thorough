---
name: be-thorough
description: Enforce high-rigor completion workflows for coding and specification-driven tasks. Use when the user says to be thorough, invokes $be-thorough, asks for exhaustive/rigorous implementation, requests no shortcuts, or gives a comprehensive prompt, PRD, audit report, design document, checklist, issue list, or similar source of truth that must be fully satisfied before finalizing.
---

# Be Thorough

## Core Rule

Treat "done" as a verified state, not a feeling. Before finalizing, prove that the implementation or deliverable satisfies the source request and has survived independent review.

Keep working until all actionable findings are resolved, all required scope is complete, or a real blocker prevents progress. If blocked, report the blocker with the evidence gathered and the exact remaining work.

## Coding Workflow

After every coding pass, run an independent code-audit loop before doing more unrelated work or finalizing.

A coding pass is any coherent set of implementation edits: adding a feature slice, fixing a bug, refactoring a module, changing tests, or applying audit fixes. Small mechanical formatting-only edits do not require a separate audit unless they could affect behavior.

Use this loop:

1. Run the relevant local verification first when it is cheap and available: focused tests, type checks, linters, build, smoke tests, or runtime checks.
2. Start one or more code-audit subagents using the highest available model and strongest feasible reasoning. Give them the current task, the original requirements, the relevant changed files or diff, and instructions to return only concrete findings with file/line evidence, severity, and suggested fixes.
3. Apply every valid finding. If a finding is invalid or intentionally deferred, write down the technical reason and evidence; do not silently ignore it.
4. Re-run the relevant local verification after fixes.
5. Repeat subagent audits until they return no valid actionable findings.
6. Run a main-thread code audit yourself from a reviewer stance against the current working tree. Look for bugs, regressions, missing tests, edge cases, security boundaries, performance risks, and integration mismatches.
7. Apply any valid main-thread findings and verify them.
8. Run subagent audits again after main-thread fixes.
9. Continue the cycle until both the subagent audit pass and the main-thread audit pass are clean.

Do not produce the final response while any valid audit finding remains unresolved.

## Requirement Completeness Workflow

When the task is based on a source of truth such as a PRD, design doc, audit report, issue, checklist, long prompt, or multi-part request, perform a final completeness check before reporting completion.

Use this loop:

1. Preserve or reconstruct the starting source of truth from the user prompt, linked documents, local files, issue text, PRD, audit report, or acceptance criteria.
2. Before finalizing, run a subagent on the highest available model to re-read that source of truth and compare it with what was actually done. Ask for a binary result: `done` or `not done yet`, plus a concise list of missing or mismatched requirements.
3. If the subagent says `not done yet`, resume implementation and complete the outstanding parts.
4. Re-run local verification and the coding audit loop for any new coding pass.
5. Run the completeness subagent again.
6. Repeat until the completeness check returns `done`, or until a real blocker prevents completion.

Do not treat partial compliance, "close enough", or unverified assumptions as complete. If a requirement is impossible, obsolete, contradictory, or intentionally out of scope, document the reason and get as close to the requested outcome as the available tools and constraints allow.

## Subagent Expectations

Use subagents as independent reviewers, not rubber stamps.

- Use the highest available model for audit and completeness subagents.
- Keep prompts scoped and evidence-oriented. Include the original requirements and current artifacts, but do not include your intended answer or ask them to confirm your conclusion.
- Prefer multiple specialized audit subagents for broad or risky code changes, such as one for correctness, one for security/data integrity, and one for tests/runtime behavior.
- Require concrete, actionable output. Findings need evidence; vague concerns must become a reproducible check, code reference, or explicit non-finding.
- If subagents are unavailable in the current harness, perform an explicit independent main-thread audit pass instead, state that limitation in the final response, and do not pretend that a subagent audit occurred.

## Verification Discipline

Use the verification surface that matches the risk:

- For code: run focused tests or checks that exercise the changed behavior; broaden to full suites when the change touches shared contracts, cross-module behavior, security, persistence, public APIs, or user-facing workflows.
- For frontend work: inspect rendered UI with browser automation or screenshots when feasible, especially for layout, interaction, responsive behavior, and visual regressions.
- For documents, specs, data, and generated artifacts: render, parse, diff, or inspect the actual output, not only the source files.
- For operations or deployments: verify the real runtime interface, not just that a command exited successfully.

Record failures as work items, fix them, and re-run the same check that exposed the issue.

## Final Response Gate

Finalize only when all are true:

- Local verification appropriate to the task has passed or any inability to run it is clearly explained.
- Subagent code audits are clean, or subagents are unavailable and the fallback audit limitation is disclosed.
- Main-thread code audit is clean.
- Requirement completeness check is `done` for document-driven or comprehensive tasks.
- The working tree contains only intentional changes for the task.

In the final response, summarize what changed, what verification ran, and any residual risks or blocked items. Keep the report concise, but do not omit unresolved blockers.
