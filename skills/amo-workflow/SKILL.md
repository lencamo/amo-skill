---
name: amo-workflow
description: Coordinate feature delivery or resume active work, choosing a lightweight or staged process by scope and risk. Not for standalone questions or isolated implementation, design, diagnosis, or review requests without delivery coordination.
metadata:
  version: '0.10.0'
---

# Amo Workflow

Coordinate delivery stages and their evidence. Use the existing amo skills for the substantive work.

## Use When

- The user requests delivery coordination, from a lightweight change to staged implementation, or continuation of an active delivery.
- A project workflow entry selects this process for the task.

## Do Not Use

- A standalone question or isolated implementation, design, diagnosis, or review request has no delivery coordination context.
- The user has chosen a different workflow.

## Delivery Mode

Choose the process by changed behavior and consequences, not file count:

- **Lightweight:** requirements and the repair boundary are settled, and the change is presentation-only or a bounded local behavior/contract repair with identifiable direct callers and focused verification. Touching storage or an API alone does not require staged delivery. Combine applicable work using the lightweight path in modules.md; retain risk-appropriate verification and independent review.
- **Staged:** connected business flows, critical permission or money protections, migrations, complex concurrency, or unresolved decisions require separate implementation/verification checkpoints. Use the applicable delivery stages in modules.md.

Honor the user's requested scope and verification limits. New evidence can require additional focused checks or a mode change; explain the concrete impact instead of adding stages automatically. Delivery mode does not grant operation permissions.

## Workflow

1. Read the applicable project rules and delivery preferences, choose the delivery mode above, then read [modules.md](references/modules.md) for the applicable path, evidence, and record. Resolve the actual worktree, branch, running environment, design source, and existing task record before continuing. Honor explicit scope; for whole-branch closeout, resolve the baseline/target and net branch changes, including agreed workspace changes. Identify patch-only checks as partial coverage, distinct from branch review or application audit.
2. Reuse settled requirements, proposals, and authorization; proceed to implementation when they are sufficient. Otherwise investigate and prepare the necessary plan/preview before collecting unresolved business decisions and execution authorization. Record the agreed scope, acceptance criteria, execution mode, and applicable checkpoints without adding a design stage to a defined repair.
3. In continuous mode, advance through applicable stages after plan approval; in UI-first mode, also wait for UI acceptance before business integration. Report progress with artifact links without turning ordinary stage updates into approval requests.
4. Select and read the relevant installed skill by name for each piece of work: feature/improve for proposals, preview for interactive UI proposals with entry guidance and key interactions (honor static-image requests directly without requiring interactive HTML), best/detail/research when needed, implement for code, review for review standards or standalone functional review, check for supplied feedback, fix for unresolved diagnosis, draft for content, and deliver for delivery's independent review and final closeout. Preserve their responsibilities and output contracts. If a required skill is unavailable, state the coverage gap rather than claiming it ran.
5. Repair verified defects within the approved implementation scope and repeat affected checks. Reopen design decisions only when new evidence changes the agreed behavior or scope. Review-only and feedback-verification requests remain read-only unless repair is also authorized.
6. Refresh the delivery record at stage transitions, material decisions, interruptions, and handoff. On resume, compare it with current code, configuration, and environment; recheck only evidence invalidated by changes. Apply local corrections to the affected decision and retain the other confirmed decisions. When a correction conflicts with another decision, explain the changed user-visible outcome and resolve that conflict before dependent work. Answer side questions and then resume the active stage unless the user stops or redirects it.
7. At final acceptance and closeout, read and use amo-deliver without requiring another invocation from the user. Pass the target, current evidence, delivery preferences, authorization, and pending steps; let it coordinate experience, independent final review, repairs, and acceptance. Keep the existing delivery record and record only actual authorized closeout results. Follow the user’s explicit commit/push ordering; user acceptance remains a separate status rather than an extra prerequisite for an already authorized earlier commit.

## Key Rules

- Establish authorization from explicit instructions and applicable project rules. Store its source and scope; a record, plan approval, or "continue" does not grant extra Git, external-write, production, or delegation permissions.
- Separate agent verification, user acceptance, commit, and deployment states. Report skipped stages with a reason and unavailable checks as gaps. Request the user's decision on material unresolved gaps at final acceptance; never relabel them as passed.
- Interrupt for a necessary new business decision, scope or permission expansion, or a missing condition the agent cannot supply. Continue independent authorized work while awaiting the answer. If the same blocker persists after a targeted recovery attempt without new evidence, preserve state and report the blocker instead of repeating ineffective retries.
- Apply amo-review's risk-proportionate standards. Let amo-deliver select whether independent review is needed and its scope/executor; reuse the result across review and closeout, without another pass for a stage transition. Record an exemption as not applicable, not independently passed. Evaluate feedback using amo-check in the coordinating session; a new defect reopens only affected work. Keep the chosen process size separate from review depth: a lightweight data-protection repair still needs its critical failure paths checked.
- Keep task records and evidence in the project's designated location, using existing documents first. Record artifact paths and environment purpose, not credentials or tokens. Keep project-specific paths out of this reusable skill and follow the designated runtime guide for execution details.
- This is an instruction workflow executed by the current agent, not a scheduler. Persist a recoverable next step when execution stops; do not promise unattended execution or automatic wake-up.

## Output

Use the user's language and requested level of detail. Lead with the answer to the current request. For a complete deliverable, follow the format below, preserving label order and omitting inapplicable sections. For a focused follow-up, answer only that question and any qualification needed to interpret the answer; do not repeat the report or restart workflow routing.

Use the active module skill's format for its substantive deliverable and the format below for coordination reports; do not concatenate all module reports. Prefix coordination reports with `🧭 [amo-workflow]`.

```text
🧭 [amo-workflow] Scenario: feature delivery
Current stage:
Results and evidence:
Pending decisions or gaps:
Next action:
```
