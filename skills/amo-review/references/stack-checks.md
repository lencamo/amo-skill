# Stack-Specific Checks

Read the sections selected by SKILL.md. Use each row when its trigger appears in the scoped change; these are investigation prompts, not automatic findings or mandatory test runs.

## Vue / TypeScript

| Changed area | Trace | Check before reporting |
| :--- | :--- | :--- |
| Component props, emits, or models | Compare payload types, event timing, controlled state, and every affected caller's listeners. | An update event and a change event can both be intentional; establish that a consumer loses state or performs an action twice. |
| Filters, pagination, selection, or reused components | Follow state ownership and the required reset/retention behavior across route, account, and dataset changes. | Retained state is a defect only when it violates the intended scope or causes incorrect results or actions. |
| Watchers and request triggers | Trace event handlers, watchers, and route updates to the actual request and resulting UI state. | Check batching, equality guards, and deliberately distinct requests before claiming duplicate execution. |
| Async responses and scope changes | Resolve which response may update the current page or drawer after a new search, navigation, or close. | A request sequence guard may already prevent stale writes; missing cancellation alone does not prove stale data. |
| Timers, listeners, and subscriptions | Trace registration and cleanup through unmount, deactivation, and re-entry, as applicable. | Distinguish framework-managed cleanup from resources created outside the component's managed scope. |
| API values and TypeScript assertions | Follow real response shapes, nullable fields, string/number conversions, and identifiers into comparisons and actions. | A type assertion or any is not a runtime check, but its use alone is not a defect; confirm a reachable incompatible value. |
| HTML, URLs, or client permission checks | Trace untrusted values to rendering/navigation sinks and protected actions to server authorization. | Verify escaping, sanitization, URL validation, or server guards; UI visibility alone neither proves nor enforces authorization. |

## Python

| Changed area | Trace | Check before reporting |
| :--- | :--- | :--- |
| Mutable defaults, class attributes, globals, or closures | Check whether state persists across calls, instances, requests, or loop iterations contrary to intent. | Read-only defaults, deliberate caches, and local state are not unintended sharing. |
| Optional or partial data | Follow empty collections, missing keys, None, and unit/type conversions from actual producers to consumers. | Honor validated upstream constraints; do not invent inputs the boundary excludes. |
| Exception handling or partial work | Follow failure propagation, externally reported success, and any writes already performed. | An enclosing handler may deliberately recover; report lost failures or inconsistent outcomes, not a preferred except style. |
| Files, connections, locks, or generators | Follow release on success, early return, exception, and cancellation. | Framework lifecycles and complete try/finally cleanup can be sufficient without a with statement. |
| Async functions and background tasks | Check blocking operations in the event loop, task lifetime, exception observation, and cancellation cleanup. | Verify the real invocation context and any executor/task supervisor; task creation without a direct await is not automatically wrong. |
| Concurrent updates or repeated operations | Trace shared read-modify-write sequences, transaction boundaries, idempotency, and duplicate side effects. | Establish concurrent or retry invocation and inspect locks, atomic operations, or database constraints. |
| SQL, shell commands, deserialization, or file paths | Trace input trust through construction, validation, and execution. | Check parameterization and effective boundary protection; an API name or trusted constant alone does not prove an exploit. |
| Loops, queries, or large materializations | Relate repeated I/O, N+1 access, or memory growth to the actual path and expected data scale. | Do not report hypothetical performance costs without a meaningful workload or resource impact. |

## Reference

The selection of checks draws on [Open Code Review Delegate](https://github.com/alibaba/open-code-review/blob/main/skills/open-code-review-delegate/SKILL.md) and its resolved language rules; execution uses amo-review without that tool dependency.
