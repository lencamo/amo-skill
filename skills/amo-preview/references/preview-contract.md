# UI Proposal Preview Contract

The preview must let the user answer: where do I enter, what will change, and how do I operate it? Apply these goals to the actual web, mobile, admin, page, component, or dialog scenario.

## Baseline Evidence

Before choosing visual values, inspect the relevant existing screens and retain their entry points, project/identity context, and representative screenshots. Identify navigation, content width, component shape, colors, typography, spacing, and important interaction patterns. Match the project's actual theme; a previous preview's host-dependent light/dark appearance is not a universal palette.

Distinguish inspected product behavior from design references and proposed changes. If there is no existing screen, use the agreed design reference and label the new surface accordingly. Never present a screenshot of an earlier prototype as the original live system.

## Entry Route and Marking

- Start at an agreed, recognizable screen and retain the navigation needed to reach the change. Cover the relevant route through menus, existing buttons, intermediate screens, and dialogs. A deep link, isolated final dialog, or preview-only page switcher cannot replace that route.
- Mark both necessary entrances and actual additions or adjustments with rounded orange dashed outlines. Mark an entrance even when the original control is unchanged. Distinguish their purposes with short preview annotations or a legend: "entry to view the change" versus "changed area"; an entry mark does not claim that its control was modified.
- Show the relevant next entrance on each step and the actual changes when reached. Scope marks to the current route and visible state, including dialogs, rather than highlighting unrelated controls. For a moved or removed element, show its original location or a labeled before/after view so the change remains locatable.
- Enable marks by default and provide one toggle for a clean view. Use an overlay or equivalent treatment that preserves the product's layout, component appearance, focus, and click targets; keep outlines rounded and orange in every represented viewport.

## Artifact

- Deliver interactive HTML by default, with the screens, components, dialogs, and viewport appropriate to the actual platform and decision. Do not require an admin shell, fixed page set, or sample business domain. Generate enough coherent content and visual detail to judge the result; a sparse interaction test harness is insufficient.
- Retain the inspected product context and shared components needed to recognize the feature's location. Extend them with the agreed fields and controls; do not introduce an unrelated interface or rename shared behavior to accommodate one feature.
- Scope CSS and DOM queries to the preview, use local scripts and assets where practical, and avoid requiring a new application framework for a small mockup. Follow the host renderer's packaging rules when embedding and provide the artifact's actual open/run entry.
- Use a coherent synthetic scenario. Derive dependent totals, labels, and states from local data. Reflect a demonstrated save or state change in the other represented pages; allow reset to the starting scenario. Identify which controls are demonstrable and which are out of scope.
- Make labels, buttons, dialogs, and forms usable with keyboard focus and visible validation. In a sandbox that blocks form submissions, use explicit local action handlers with validation and keyboard support. Demonstrate the applicable empty, disabled, confirmation, success, or failure states that affect the proposed decision rather than implementing unrelated navigation.
- Keep credentials, real customer data, and service calls out of the artifact. Sample actions must remain local, including form submission and upload controls. Use already permitted non-sensitive assets; obtaining new remote assets still follows the task's authorization.

## Review Frame and Presentation

Place the short scenario/sample-data notice, route guide, marking controls, and reset in the surrounding preview frame. Add page switching only when useful for reviewing multiple surfaces. Keep normal product copy inside the canvas and render guidance labels as review annotations rather than production content.

Deliver the clickable preview, plus representative screenshots as evidence. Prefer in-conversation embedding when the host supports it; otherwise provide a working local entry and explicitly identify the presentation limitation. Static screenshots alone do not replace the default interactive deliverable. If runtime viewing is unavailable, deliver the artifact with that verification gap instead of claiming it was exercised.

For a revision, retain the same artifact entry where practical, preserve unaffected agreed behavior, and summarize the requested differences. Keep before/after screenshots tied to their actual artifact versions; clearly separate live-system captures from preview captures.

## Verification

Open the artifact at the agreed start and reach the change using the represented product entrances, including an unchanged trigger when applicable. Check that the next step is discoverable, the final UI is visually assessable, and the key operation produces its expected local outcome. Verify mark purpose, shape, color, visibility, and unobstructed clicks along the route.

Check the rendered layout at the intended review size and exercise the applicable edited values, confirmation/cancellation branches, state propagation, clean-view toggle, and reset to the starting screen. Check that the runtime is not sending business requests, form submissions, or navigation to production.

Verify only interactions actually present. Report the inspected baseline, exercised paths, synthetic behavior, and missing coverage accurately. A proposal preview supports a design decision; runtime UI and business acceptance remain later delivery stages.
