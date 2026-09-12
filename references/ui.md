## UI and Human Review Workflow

For any UI work, make rendered user experience a first-class acceptance gate. Keep iterating until the "human in you" would be satisfied with what a real user sees and does, not merely until tests pass or components compile.

Use whatever can inspect the actual interface: Browser/in-app browser, Playwright, screenshots, accessibility snapshots, responsive viewports, keyboard navigation, hover/focus/tap checks, console/network inspection, and manual visual review. Inspect the UI after meaningful changes and again after fixes. Treat screenshots as evidence to critique, not a checkbox.

When subagents are available and the harness permits them, select one to three personas that best match the actual users and risk. Use every persona only when the user explicitly requests exhaustive persona coverage. Give reviewers the current requirements and rendered UI artifact or running target, but not your conclusions. Available personas:

- Karen, non-technical user: notices confusion, friction, unclear labels, missing affordances, and brittle happy paths.
- John, technical coder: notices implementation tells, broken states, edge cases, and developer-facing workflow issues.
- Bobby, competent manager: checks task completion, business usefulness, prioritization, and operational clarity.
- Sven, manager who failed upward: impatient, literal, status-driven, and likely to misunderstand ambiguous UI, labels, or state.
- UX expert: checks interaction design, accessibility, information architecture, responsive behavior, focus handling, and error states.
- Marketing expert: checks positioning, clarity of value, tone, trust cues, conversion paths, and copy consistency.

Classify persona findings through the scope governor, apply admitted findings, and re-run the relevant visual checks. If subagents cannot be used, perform the same selected persona passes yourself and disclose that limitation when it materially affects confidence.

During UI inspection, verify:

- Responsive behavior and mobile ergonomics where applicable, including tap targets, touch-specific affordances, hover-only controls, click flows, and keyboard flows.
- Layering and portal behavior: dropdowns, comboboxes, tooltips, popovers, menus, toasts, and modals must not render behind overlays, native dialogs, top-layer hosts, or higher-z elements.
- Edge-of-viewport behavior: hover/focus menus and floating elements near boundaries should flip, shift, stay visible, and remain reachable.
- Text layout: non-breaking words, long names, URLs, counters, translations, and dynamic data must not overlap, clip, or force unintended page-level overflow.
- State coverage: loading, empty, error, disabled, pending, success, destructive confirmation, slow network, offline where relevant, and repeated-submit states.
- Accessibility: semantic labels, focus order, keyboard reachability, contrast, reduced motion, visible state, and screen-reader-friendly names/status.
