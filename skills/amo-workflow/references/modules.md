# Delivery Modules

Use the applicable rows for the current task. Keep all eight statuses in the delivery record; mark a stage not applicable with its reason instead of inventing work. The rows describe completion evidence, not eight mandatory user approvals.

| Stage | Work | Reviewable result | Completion condition |
| :--- | :--- | :--- | :--- |
| 1. Requirements and current state | Read requirements and design states; inspect actual code and relevant running pages under the correct project, identity, and tenant. Distinguish reusable, changed, new, and unverified capabilities, including their real entry points. | Scope and current-state/change inventory, sources, and unresolved business questions. | Enough evidence to propose the work; remaining unknowns are explicit. |
| 2. Proposal and preview | Explain user, operator, and system flows; identify shared behavior, data contracts, migrations, acceptance criteria, and deployment dependencies. When UI changes need a concrete decision, use amo-preview to prepare an interactive HTML proposal grounded in the inspected interface, with a discoverable entry route, rounded orange dashed entrance/change marks, and local scenario interactions. Consolidate decisions on rules, UI direction, execution mode, checkpoints, and permitted operations. | Plan and necessary clickable preview entry with representative screenshots and coverage limits, with confirmed decisions distinguished from recommendations. | The user has approved the applicable plan and execution boundary; existing explicit approval counts. |
| 3. Real UI | Inspect design annotations, relevant states, and current components. Verify the actual asset upload and readback path within authorization, reuse headers/components where appropriate, and implement native pages in the target stack. Check rendered states against the approved design, accepted preview where applicable, and rules. | Running page entry points, state screenshots, design comparison, and identification of mock versus live data. | Applicable states are checked in the runtime; in UI-first mode the user also accepts them. |
| 4. Business integration | Connect admin configuration, APIs, persistence, and state transitions; replace demonstration responses. Prepare schema changes using the project's migration mechanism and preserve affected existing flows. | Connected implementation, data-source mapping, migrations where needed, and focused verification. | Core paths are ready for end-to-end integration; remaining limits are recorded. |
| 5. Integration and experience | Establish an isolated environment using the actual implementation and reproducible setup. Exercise operator setup, user actions, downstream processing, and relevant failure paths; distinguish real dependencies from substitutes. | A usable environment, access instructions without secrets, experience steps, expected outcomes, and observed results. | The core flow is exercised across its participating interfaces; UI and dependency gaps remain explicit. |
| 6. Review and feedback verification | Use amo-review to inspect implemented changes against requirements, related callers, and high-risk boundaries; use amo-check to verify supplied findings. Carry completed review evidence into closeout rather than scheduling another review solely for a stage change. | Prioritized defects, deferrable advice, verification gaps, and evidence. | Scoped findings are evaluated and handed to repair or acceptance; a clean review is valid. |
| 7. Repair and recheck | Repair approved defects, reproduce relevant triggers, check affected existing behavior, and refresh invalidated evidence. | Fix results and current acceptance evidence. | Required defects are resolved; unresolved or deferred limits are explicitly presented for user decision. |
| 8. Acceptance and closeout | Use amo-deliver to coordinate final experience, independent review through amo-review, feedback rounds, repairs, and user acceptance. Reuse valid completed review and verification evidence; Orca provides session execution and report return. Present completed scope and remaining limits. After acceptance, carry out authorized closeout and explain applicable migration order, prerequisites, deployment, and rollback. | Acceptance record, actual commit/sync results, included/excluded files, and release handoff. | User acceptance and authorized closeout results are recorded; awaiting authorization is not completion. |

## Planning Checkpoint

Recommend continuous execution when the design and rules are sufficiently defined. Use UI-first when requested or when the user needs to judge the page direction before integration. Settle meaningful uncertainty with a concrete preview, not an abstract approval request.

## Delivery Record

Use the existing task specification and issue tracker; add a short delivery section rather than creating parallel tracking documents. Choose a record location from project instructions. If none exists, establish it with the user before persisting outside the agreed workspace; continue useful discovery meanwhile.

Maintain these fields as facts, with evidence links where relevant:

| Field | Content |
| :--- | :--- |
| Goal and boundary | Target behavior, exclusions, acceptance criteria, and unresolved business decisions. |
| Confirmed decisions | Agreed rules and design direction, with the conversation or instruction that established them; distinguish user confirmation from recommendations and assumptions. Retain decision-critical business meanings and current user-visible outcomes so later stages use the same interpretation. |
| Execution agreement | Continuous or UI-first, required checkpoints, and authorization source/scope for implementation and any separate operations. |
| Working context | Actual repository, worktree, branch/revision, environment purpose, persistence, and real versus simulated dependencies. |
| Stage progress | Each of stages 1–8: pending, active, agent-verified, awaiting-user, user-accepted, blocked, or not-applicable; attach artifacts and verification limits. |
| Findings and repairs | Trigger, evidence, action decision, repair status, and affected checks. |
| Review and verification evidence | Reviewer identity and completion state, baseline/target and coverage, verification commands and results/logs, and relevant environment. Reuse this record across implementation, review, and closeout; refresh only evidence invalidated by changes. |
| Background resources, when present | Task-owned background check and review-session handles, purpose, current state, retained development/acceptance services and access points, and unresolved cleanup with its reason and next action. Reconcile these on resume before retrying or releasing resources. Record only resources this task needs to manage; do not inventory all machine processes. |
| Closeout | Intended included/excluded files, temporary configuration, user acceptance, and actual Git/release results. |
| Resume | Next action, outstanding answers/conditions, and last update. |

Do not mark agent-verified stages as user-accepted. Keep related implementation tickets when the project uses them; the delivery section is a summary and links to those tickets.
