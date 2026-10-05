# Workflow: Improve Tests

This workflow provides guidance for identifying testing deficiencies, expanding test coverage, and hardening test reliability across `service_platform`.

---

## Objectives
- Elevate confidence in core business logic and critical paths.
- Eliminate flaky, non-deterministic tests.
- Ensure automated coverage for boundary conditions and error scenarios.

---

## Process Steps

### Step 1: Gap Analysis
1. Analyze test coverage reports (branch, line, function coverage).
2. Identify critical uncovered areas in `services/` and `packages/`.
3. Check for absent negative test cases (malformed input, auth failures, service timeouts).

### Step 2: Test Design & Taxonomy
Determine the appropriate testing level:
- **Unit Tests**: Pure functions, domain calculations, entity validation, utility modules. Fast and isolated.
- **Integration Tests**: Service layer interactions, database persistence, external service clients with contract mocks.
- **End-to-End Tests**: Critical end-user workflows across `apps/` and API gateways.

### Step 3: Test Implementation Guidelines
1. **Arrange-Act-Assert (AAA)**: Clearly separate setup, execution, and verification phases.
2. **Determinism**: Avoid dependency on random seeds, real time clocks, or external live network services without proper virtualization/mocking.
3. **Descriptive Names**: Name tests clearly: `should [expected result] when [condition/action]`.
4. **Independent & Isolated**: Each test must be runnable independently without relying on the side effects of prior tests.

### Step 4: Verification & Suite Timing
1. Run the new tests to verify pass status.
2. Run test suite multiple times if concurrency or async logic is tested to verify lack of flakiness.
3. Measure execution duration to ensure the suite remains performant.
