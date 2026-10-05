# Prompt: Weekend Maintenance Runbook

Use this prompt to execute autonomous repository maintenance, housekeeping, dependency hygiene, and technical debt sweeps.

---

## Agent Task Prompt

```text
Perform weekend housekeeping and maintenance routines on service_platform:

1. Dependency & Security Audit:
   - Run dependency vulnerability scanner (e.g. npm audit, pip-audit).
   - Check for outdated dependencies with minor/patch updates available.
   - Review licenses to ensure compliance with .agents/policies/dependency-policy.md.

2. Codebase Hygiene:
   - Identify dead code, unused imports, or orphaned asset files.
   - Check for obsolete TODO/FIXME comments or dangling mock data.
   - Verify formatting and adherence to project style rules.

3. Test Health & Coverage Sweep:
   - Run all test suites and flag tests that exhibit flakiness or slow runtimes (> 5s).
   - Identify any recently added code paths missing test assertions.

4. Deliverables:
   - Compile a maintenance summary report using .agents/templates/work-report.md.
   - Propose non-breaking fixes or chore pull requests for human review.
```
