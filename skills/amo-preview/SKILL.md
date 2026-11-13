---
name: amo-preview
description: Build or revise interactive UI proposal previews that guide users from familiar entry points to proposed changes and demonstrate how they work. Use across web, mobile, and admin interfaces before implementation, not for raster images, production code, or UX audits.
metadata:
  version: '0.2.0'
---

# Amo Preview

Make a discussed UI change discoverable, visible, and operable from the user's starting screen, using the product's existing interface language.

## Use When

- The user wants to find a proposed feature's entry, see its resulting UI, and try key interactions before implementation.
- A delivery workflow needs a concrete preview for a UI decision.
- The user asks to revise an existing proposal preview.

## Do Not Use

- The primary task is to decide a new feature's business design; establish the approach first.
- The user requests a generated illustration, production page implementation, or an audit of an existing experience.
- The user explicitly requests a static-only artifact; honor that format directly.

## Workflow

1. Read the discussed approach, settled decisions, project instructions, and any existing preview. Read [preview-contract.md](references/preview-contract.md) for the route, marking, artifact, and verification requirements.
2. Inspect the relevant running interface under the correct project and identity using available browser, device, or runtime tools. Use design files and code as supporting evidence. If inspection is unavailable, report the gap and use supplied references only as permitted by the task and project rules; do not claim an uninspected style match.
3. Trace the familiar starting screen, necessary entrances and intermediate steps, target changes, and resulting states. Distinguish unchanged navigation from actual modifications. Preserve existing shared behavior and terminology unless their change is agreed; resolve material business uncertainty through the proposal owner.
4. Build a local interactive HTML preview suited to the actual platform and decision, following the contract. Generate the required pages, components, or dialogs from the inspected product and agreed references; do not impose a fixed business example or page count.
5. Apply the contract's entry guidance and change marking throughout the route, including the necessary entrances that remain unchanged.
6. Open the artifact at the agreed starting screen and follow the represented user path through the target changes. Exercise relevant states, mark visibility, and reset; inspect the rendered result and save representative screenshots. Record unavailable checks as gaps.
7. Present the clickable artifact through a supported host renderer or a usable local entry, with a short starting-point/operation guide. For revisions, update the same preview and identify which version any before/after screenshot represents.

## Key Rules

- Implement only the agreed preview scope. Keep it separate from production source changes, releases, and business writes; preview requests do not authorize those operations.
- Use synthetic data and local state for demonstrated actions. Preserve enough shared state to show their consequences across the represented pages; do not wire sample saves or fulfillment actions to live endpoints.
- Keep product content in the product UI and review controls in its surrounding preview frame. Follow the contract for change marking and presentation rather than adding implementation commentary to the business screens.
- Reuse an available visualization renderer according to its own instructions when suitable; keep the preview usable without an assumed host SDK. Distinguish verified behavior, simulated behavior, and unverified style or runtime limitations.

## Output

Use the user's language and requested level of detail. Lead with the answer to the current request. For a complete deliverable, follow the format below, preserving label order and omitting inapplicable sections. For a focused follow-up, answer only that question and any qualification needed to interpret the answer; do not repeat the report or restart workflow routing.

```text
🖼️ [amo-preview] Scenario: UI proposal preview
Preview:
Coverage and changes:
Verification and gaps:
```
