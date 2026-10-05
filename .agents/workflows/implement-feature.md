# Workflow: Implement Feature

This workflow outlines the mandatory sequence for planning, developing, testing, and verifying new features within `service_platform`.

---

## Prerequisites
- Review `.agents/policies/product-authority.md` to confirm the scope is authorized.
- Obtain or create a structured brief using `.agents/templates/task-brief.md`.
- Ensure clean working tree and up-to-date branch.

---

## Process Steps

### Step 1: Requirements & Scope Analysis
1. Define the functional requirements, acceptance criteria, and edge cases.
2. Identify affected components across `apps/`, `services/`, and `packages/`.
3. If an architectural decision or schema change is required, document it using `.agents/templates/decision-record.md` and check `.agents/policies/database-change-policy.md`.

### Step 2: Implementation Design
1. Identify existing patterns, types, and utilities to reuse in `packages/`.
2. Draft interface contracts (API routes, payloads, response schemas, types).
3. Confirm data validation boundaries (Zod/Pydantic/schemas).

### Step 3: Incremental Implementation
1. **Shared / Types First**: Implement or extend types and domain models in `packages/`.
2. **Backend / Core Services**: Build business logic and endpoint handlers in `services/`.
3. **Frontend / UI**: Build components and integration views in `apps/`.
4. Keep edits modular and avoid touching unrelated files.

### Step 4: Testing & Verification
1. Add unit tests for business logic and edge cases.
2. Add integration tests for API endpoints and contracts.
3. Run the project test suite and linter. Ensure zero warnings or errors.

### Step 5: Delivery & Summary
1. Complete a work report using `.agents/templates/work-report.md`.
2. Verify all requirements are satisfied against the original task brief.
