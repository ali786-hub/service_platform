# Workflow: Fix Defect

This workflow describes the systematic methodology for diagnosing, reproducing, fixing, and verifying software defects in `service_platform`.

---

## Core Rule: Reproduce Before Modifying
Never attempt a fix without first reproducing the failure or writing a test that demonstrates the defect.

---

## Process Steps

### Step 1: Defect Triage & Understanding
1. Review the defect report, error logs, and stack traces.
2. Determine the affected subsystem (`apps/`, `services/`, or `packages/`).
3. Identify the expected behavior versus the actual behavior.

### Step 2: Reproduction & Minimal Failing Test
1. Create a reproducible scenario or write an automated unit/integration test that asserts expected behavior and currently fails.
2. Confirm the failure reproduces consistently.

### Step 3: Root Cause Analysis
1. Inspect the code path leading to the defect.
2. Distinguish the root cause from downstream symptoms.
3. Check for similar vulnerabilities or bug patterns elsewhere in the codebase.

### Step 4: Minimal & Targeted Fix
1. Apply the most concise and direct fix addressing the root cause.
2. Avoid unnecessary refactoring or scope creep in the same patch.
3. Ensure no regression is introduced to existing functionality.

### Step 5: Regression & Suite Verification
1. Run the failing test from Step 2 and confirm it now passes.
2. Run the full test suite for the affected module and dependent packages.
3. Run linting and static analysis checks.

### Step 6: Documentation
1. Document the root cause, fix rationale, and verified tests using `.agents/templates/work-report.md`.
