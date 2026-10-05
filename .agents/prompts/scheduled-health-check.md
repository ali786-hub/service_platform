# Prompt: Scheduled Health Check

Run this prompt periodically to evaluate the overall health, build status, and integrity of `service_platform`.

---

## Agent Task Prompt

```text
Perform an automated health and sanity audit on the repository:

1. Verification Checks:
   a. Check git status to ensure the working tree is clean and no unintended files are tracked.
   b. Run the repository linter and type-checker across all workspaces/packages.
   c. Execute the automated test suite across apps/, services/, and packages/.
   d. Check for broken links or outdated references in documentation.

2. Diagnostic Analysis:
   - Identify any test failures, warnings, or deprecation notices.
   - Inspect build outputs to detect unusually large bundle sizes or compilation anomalies.

3. Reporting:
   - Generate a concise health summary report.
   - If issues are detected, detail reproduction steps and suggested remediation paths.
   - Do NOT modify codebase files during this health check unless explicitly instructed to fix failures.
```
