# Workflow: Review Code

This workflow defines the quality and security checklist required when reviewing code or validating changes before pull request submission.

---

## Review Dimensions

### 1. Correctness & Logic
- [ ] Does the implementation fulfill all requirements from the task brief?
- [ ] Are edge cases handled (null/undefined values, empty collections, network timeouts)?
- [ ] Are race conditions, concurrency bottlenecks, or state desynchronizations present?

### 2. Architecture & Design Alignment
- [ ] Are code changes placed in the correct directories (`apps/`, `services/`, `packages/`)?
- [ ] Does the code reuse existing utilities rather than reinventing wheels?
- [ ] Is modularity and separation of concerns maintained?

### 3. Security & Boundaries
- [ ] Does the code comply with `.agents/policies/security-boundaries.md`?
- [ ] Are all user inputs and external payloads validated and sanitized?
- [ ] Are credentials, tokens, or environment secrets hardcoded? (MUST BE ZERO)
- [ ] Are authorization and authentication checks enforced on protected endpoints?

### 4. Database & State
- [ ] Does the change comply with `.agents/policies/database-change-policy.md`?
- [ ] Are queries optimized (indexing, avoiding N+1 queries)?
- [ ] Are database transactions used where atomic consistency is necessary?

### 5. Testing & Verification
- [ ] Are new tests added for new logic and bug fixes?
- [ ] Do all unit and integration tests pass without failures or flakiness?
- [ ] Is test coverage maintained or improved?

### 6. Readability & Maintainability
- [ ] Is code cleanly formatted, following project style guidelines?
- [ ] Are variable, function, and file names clear and descriptive?
- [ ] Are complex algorithms or non-obvious design decisions properly commented?
