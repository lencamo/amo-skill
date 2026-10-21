---
name: amo-detail
description: Use when the user wants an existing discussed proposal expanded into how the agent plans to implement it and how workflows, frontend behavior, backend processing, and data will change afterward. Not for initial solution design, challenging the chosen approach, coding, or code review.
metadata:
  version: '0.4.0'
---

# Amo Detail

Expand an existing discussed proposal into concrete implementation intentions and resulting behavior. The proposal is the primary source; code is optional supporting evidence.

## Shared Output Marker

Prefix the first output line inline with `🔎 [amo-detail]`. Do not put the marker in a separate paragraph.

## Use When

- A proposal exists, supplied by the user or formed through `amo-feature`, `amo-improve`, `amo-fix`, `amo-refactor`, or `amo-best`.
- The user wants to understand how the agent plans to carry out the proposal and what will change afterward.
- The user asks for concrete workflow, frontend, backend, storage, or scheduled-task details beyond a proposal summary.

## Do Not Use

- No approach exists yet; use `amo-feature`, `amo-improve`, `amo-fix`, or `amo-refactor`.
- The user wants to challenge the proposal; use `amo-best`.
- The user wants code implementation or review of implemented code.

## Workflow

1. Establish the proposal, goal, scope, and settled decisions from the discussion.
2. Trace the resulting flow from user action or system trigger to outcome, identifying affected features and modules.
3. Expand frontend implementation: page changes, which existing components and APIs will be reused or adjusted and how, data sources, state ownership, request handling, and resulting display, interaction, and state transitions.
4. Expand backend implementation: entry points and inputs, which existing processing logic will be reused or adjusted and how, business rules, data reads and writes, storage changes (tables and fields), results and consumers. For scheduled tasks, explain triggers or timing, work, and outcomes.
5. Check that frontend requests, backend inputs, responses, and UI updates connect; identify open questions affecting implementation.
6. Describe actions beyond routine deployment (scheduled tasks, backfills, migrations, etc.), their targets, and required timing or dependencies. State when none apply; list uncertainties as open questions.

## Key Rules

- Use the discussed proposal as the primary source and follow settled decisions; inspect code only as needed for verification.
- For each major change, explain what will be done, how it will work, and resulting behavior; summaries or name lists alone are insufficient.
- Distinguish settled decisions, planned details, and open questions. Do not invent current behavior or defer routine implementation details to the user.
- Stay within the proposal; do not add features or architecture, or change states beyond its scope. Mark irrelevant areas as not involved.
- Explain without implementing; provide execution order beyond deployment and verification plans only when requested.

## Output

Use the user's language for output labels and content.

```text
🔎 [amo-detail] Scenario: proposal implementation details
Proposal:
End-to-end flow:
Frontend implementation:
Backend implementation:
Impact scope:
Deployment actions:
Open questions:
```
