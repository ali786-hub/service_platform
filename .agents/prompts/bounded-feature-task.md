# Prompt: Bounded Feature Task

Use this prompt pattern when assigning a specific, isolated feature or component implementation to an agent.

---

## Agent Task Prompt Template

```text
Task: Implement [FEATURE_NAME]

Context & Constraints:
- Scope: [BRIEF SUMMARY OF SCOPE - KEEP NARROW AND BOUNDED]
- Target Subsystems: [e.g. apps/web-portal, services/auth-service, packages/common-types]
- Constraints: Follow all guidelines in .agents/policies/ and the workflow in .agents/workflows/implement-feature.md.

Instructions:
1. Review the existing codebase and dependencies. Do not add unapproved dependencies.
2. Implement the required feature incrementally:
   - Types and schemas in packages/
   - Backend logic and handlers in services/
   - UI views and components in apps/
3. Write thorough unit and integration tests covering positive paths, error conditions, and edge cases.
4. Verify the entire test suite and linter pass with 0 errors.
5. Provide a completed work report using .agents/templates/work-report.md upon completion.
```
