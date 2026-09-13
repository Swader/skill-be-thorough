## Coding Workflow

After the implementation is coherent, run a bounded independent code-audit loop before finalizing.

A coding pass is any coherent set of implementation edits: adding a feature slice, fixing a bug, refactoring a module, changing tests, or applying audit fixes. Small mechanical formatting-only edits do not require a separate audit unless they could affect behavior.

Use this loop:

1. Run the relevant local verification first when it is cheap and available: focused tests, type checks, linters, build, smoke tests, or runtime checks.
2. Start one independent code-audit subagent when available. Give it the mission contract, relevant changed files or diff, and instructions to return only concrete findings with file/line evidence, severity, and suggested fixes.
3. Classify every finding through the scope governor. Fix admitted findings; record follow-ups and technical dispositions without silently ignoring them.
4. Re-run the relevant local verification after fixes.
5. If admitted findings changed code, run one targeted re-review limited to those fixes and their immediate causal path.
6. Run one final main-thread code audit against the mission contract. Look for unmet acceptance criteria, patch regressions, and mandatory safety issues.
7. Apply and verify any admitted final findings. Do not restart broad review unless the mission itself changed.

Stop when no admitted finding remains. The goal is not to eliminate every conceivable improvement in the surrounding codebase.
