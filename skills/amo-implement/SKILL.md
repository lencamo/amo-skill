---
name: amo-implement
description: Use when the user asks to implement an already defined proposal and verify the result, balancing code efficiency, concision, readability, and maintainability while keeping changes focused, comments useful, and frontend content free of conversation or implementation notes. Do not use for solution design, proposal explanation, or standalone code review.
metadata:
  version: '0.6.0'
---

# Amo Implement

Implement and verify a defined proposal, balancing code efficiency, concision, readability, and maintainability while preventing comment noise, frontend content pollution, and scope creep.

## Shared Output Marker

For a complete deliverable, prefix its first line inline with `🔨 [amo-implement]`. Do not put the marker in a separate paragraph.

## Use When

- A proposal and its implementation scope are already defined.
- The user asks to implement the proposal and verify the result.

## Do Not Use

- The user wants solution design or proposal review.
- The user wants proposal details; use `amo-detail`.
- The user wants functional correctness review; use `amo-review`.
- The user wants standalone code style review.
- The user wants to verify existing review feedback; use `amo-check`.

## Workflow

1. Identify the existing proposal and implementation scope.
2. Inspect relevant code, project conventions, and existing type contracts.
3. Make the changes needed to complete the proposal.
4. Check requirement completion, preserved behavior, scope, and code quality in the diff; correct issues introduced by this task. Include this requirement check in implementation self-checks rather than scheduling another review for it.
5. Select verification by changed behavior and acceptance criteria. For display-only text, comments, or non-executable prose, check the diff, replacement coverage, and unintended changes; do not default to business tests or a full build. Treat selectors, protocol values, interpolation, and executable instructions by their behavioral impact. For logic changes, run the smallest checks that exercise the changed behavior and important regressions; editing a spec does not require running every test in that file. Honor mandatory project checks and surface conflicts rather than silently waiving them. Use one-shot commands, confirm the runner honors the scope and options, and preserve actual exit status and complete failure output. Retain the tested revision, relevant uncommitted state, command, scope, environment, results, and available logs in the existing record. Mark interrupted checks as unverified; investigate unrelated failures separately without automatically rerunning or expanding the checks.
6. Report actual changes, verification results, and unfinished work. For background checks or development services started by this task, include their runtime handles, purpose, and any need to remain available for user acceptance.

## Key Rules

### Code Expression

- Follow project conventions and reuse existing patterns.
- Meet actual performance needs; remove redundancy without sacrificing clarity or maintainability.
- Prefer direct expressions for simple logic. Extract abstractions for current benefits in reuse, readability, error isolation, or testability; do not judge necessity by call count alone.
- In TypeScript, prefer inference for local variables, internal functions, and return values; avoid redundant annotations and reliably inferable complex return types.
- Use explicit types at public boundaries: DTOs, component props, exported function parameters, request payloads, and response structures. Reuse existing contracts.
- Prefer simple types, existing data structures, and ordinary narrowing. Avoid type indirection without a current benefit in clarity, contracts, or reuse.
- For composables, follow project conventions. Otherwise, destructure display-only ref/computed values as needed and keep state-changing or side-effect functions under the composable namespace so their source stays clear.

### Comments

- Comment only on non-obvious reasons, constraints, or behavior; avoid code repetition, step-by-step narration, decorative separators, vague TODOs, or long implementation explanations.
- Preserve useful business, API-contract, and license comments; limit comment cleanup to code touched by this task.

### Frontend Content

- Show only the requested business content. Do not turn conversation, proposal explanations, development history, technical limitations, or precautionary advice into unsolicited UI elements; keep explanations in the chat.
- Preserve existing UI states and initial values unless the proposal requires changing them.

### Implementation Scope

- Make only changes required by the proposal or necessary to complete it; do not add unrelated features, cleanup, or refactors.
- Do not add abstractions, dependencies, configuration, or defensive branches for hypothetical needs.
- Keep debugging within scope; report unrelated issues separately and obtain approval before expanding the agreed scope.

## Output

Use the user's language and requested level of detail. Lead with the answer to the current request. For a complete deliverable, follow the format below, preserving label order and omitting inapplicable sections. For a focused follow-up, answer only that question and any qualification needed to interpret the answer; do not repeat the report or restart workflow routing.

```text
🔨 [amo-implement] Scenario: proposal implementation
Implementation result:
Main changes:
Verification results:
Unfinished work:
```
