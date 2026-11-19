# Orca and Local Claude Review

Read this only when using Orca workers or the built-in local Claude `/code-review`; the runtime is optional unless requested by the user or required by the project.

## Assignment

- Read the orchestration skill and its version-matched runtime guide before using Orca. Use a fresh independent reviewer session, honoring the selected reviewer and configured model. For direct review, have the worker apply amo-review itself without launching another reviewer.
- When selecting local `/code-review`, use the built-in command, not the legacy GitHub plugin, cloud Code Review, ultrareview, or OCR delegate. Select effort from concrete risk: `low` for bounded low-risk work, `medium` for routine features, `high` for sensitive or complex behavior, and `max` only for a specific deeper-analysis need. Explain the choice briefly; honor explicit effort and do not run levels in sequence.
- For a contiguous committed range, pass `/code-review <effort> <base-sha>..<target-sha>` with the baseline resolved to the appropriate merge base. Preserve explicit commit selections and included workspace changes rather than substituting another scope.
- Require the worker and any built-in subprocess to remain read-only without tests/builds or fixes. After the built-in result returns, the wrapper may resolve a decisive evidence ambiguity but must not repeat the scoped review or write a second long report. Return the result and material gaps promptly.

## Completion and Cleanup

- Follow the runtime's completion protocol, including ending the coordinator turn when required. A background launch or task handle is not a completed review: wait for actual findings before reporting completion. Return results through the runtime without asking the user to copy them.
- Preserve output and reconcile owned test/build handles if any were started. On resource pressure, stop review-owned verification before further diagnosis. On cancellation, stop the assigned worker and owned subprocesses through the runtime's ownership/cancellation protocol; confirm exit before claiming they stopped. Unknown ownership or exit remains a reported gap. Preserve unrelated sessions, user takeovers, keep-open terminals, and needed development/acceptance services. Do not restart cancelled work without user instruction.
- Follow the current runtime guide for automatic or explicit release of proven dedicated terminals; pending release is not confirmed release. Terminal release, temporary-worktree cleanup, and log retention are separate; do not require deleting a workspace or logs to release a terminal.
- Keep cleanup state separate from review results. A release failure does not invalidate completed findings or warrant another review. Follow supported recovery only for the failed operation. Retry a failed worker on the same task only after its predecessor is confirmed stopped, honoring retry limits rather than creating another task to bypass them.
