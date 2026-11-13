---
name: amo-workflow
description: Coordinate a complete feature delivery or resume its staged work, from discovery and plan approval through UI, integration, review, fixes, final acceptance, and closeout. Not for standalone questions, small edits, or review-only requests outside an active delivery.
metadata:
  version: '0.6.0'
---

# Amo Workflow

Coordinate delivery stages and their evidence. Use the existing amo skills for the substantive work.

## Use When

- The user requests a complete feature delivery, staged implementation, or continuation of an active delivery.
- A project workflow entry selects this process for the task.

## Do Not Use

- A standalone question, small edit, or isolated design, diagnosis, or review request has no active delivery context.
- The user has chosen a different workflow.

## Workflow

1. Read the applicable project rules and delivery preferences, then [modules.md](references/modules.md) for stage obligations, evidence, and the delivery record. Resolve the actual worktree, branch, running environment, design source, and existing task record before continuing.
2. On a new task, investigate and prepare the plan and any necessary preview before collecting the user's business decisions and execution authorization. Record the agreed scope, acceptance criteria, execution mode, and checkpoints. Reuse decisions already established in the conversation.
3. In continuous mode, advance through applicable stages after plan approval; in UI-first mode, also wait for UI acceptance before business integration. Report progress with artifact links without turning ordinary stage updates into approval requests.
4. Select and read the relevant installed skill by name for each piece of work: feature/improve for proposals, preview for UI proposals with entry guidance and key interactions, best/detail/research when needed, implement for code, review for functional review, check for supplied feedback, fix for unresolved diagnosis, draft for content, and deliver for final acceptance and closeout. Preserve their responsibilities and output contracts. If a required skill is unavailable, state the coverage gap rather than claiming it ran.
5. Repair verified defects within the approved implementation scope and repeat affected checks. Reopen design decisions only when new evidence changes the agreed behavior or scope. Review-only and feedback-verification requests remain read-only unless repair is also authorized.
6. Refresh the delivery record at stage transitions, material decisions, interruptions, and handoff. On resume, compare it with current code, configuration, and environment; recheck only evidence invalidated by changes. Apply local corrections to the affected decision and retain the other confirmed decisions. When a correction conflicts with another decision, explain the changed user-visible outcome and resolve that conflict before dependent work. Answer side questions and then resume the active stage unless the user stops or redirects it.
7. At final acceptance and closeout, read and use amo-deliver without requiring another invocation from the user. Pass the target, current evidence, delivery preferences, authorization, and pending steps; let it coordinate experience, independent final review, repairs, and acceptance. Keep the existing delivery record and record only actual authorized closeout results.

## Key Rules

- Establish authorization from explicit instructions and applicable project rules. Store its source and scope; a record, plan approval, or "continue" does not grant extra Git, external-write, production, or delegation permissions.
- Separate agent verification, user acceptance, commit, and deployment states. Report skipped stages with a reason and unavailable checks as gaps. Request the user's decision on material unresolved gaps at final acceptance; never relabel them as passed.
- Interrupt for a necessary new business decision, scope or permission expansion, or a missing condition the agent cannot supply. Continue independent authorized work while awaiting the answer. If the same blocker persists after a targeted recovery attempt without new evidence, preserve state and report the blocker instead of repeating ineffective retries.
- Run code review against the completed change and relevant callers, not just earlier test results. Treat external review comments as claims to verify, then route confirmed issues to a separate repair step. A newly confirmed defect reopens the affected stage; it does not restart the whole delivery.
- Keep task records and evidence in the project's designated location, using existing documents first. Record artifact paths and environment purpose, not credentials or tokens. Do not add project-specific paths or tool assumptions to this reusable skill.
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
