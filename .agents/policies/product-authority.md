# Policy: Product Authority & Decision Boundaries

This policy establishes the decision-making boundaries for autonomous agents, delineating what operations may be performed independently versus those requiring explicit human sign-off.

---

## Authority Matrix

| Action / Decision Category | Autonomy Level | Approval Required |
| :--- | :--- | :--- |
| **Bug fixes within existing specs** | Autonomous | No (Proceed with test verification) |
| **Writing & expanding test coverage** | Autonomous | No |
| **Refactoring within existing API contracts** | Autonomous | No (Must pass existing test suites) |
| **Creating internal helper packages** | Autonomous | No |
| **Adding new public API routes** | Guided | Yes (Confirm route signature with user) |
| **Database schema alterations** | Strict Human Sign-Off | Yes (Mandatory approval required) |
| **Adding new third-party dependencies** | Strict Human Sign-Off | Yes (Check dependency policy first) |
| **Modifying security/auth boundaries** | Strict Human Sign-Off | Yes (Mandatory security review) |
| **Deleting existing features or data** | Strict Human Sign-Off | Yes (Explicit confirmation required) |

---

## Escalation Protocol
When an agent encounters a decision requiring human sign-off:
1. Halt execution before making destructive or unauthorized changes.
2. Formulate a concise summary of the proposed change, the rationale, and potential trade-offs.
3. Present the proposal to the user and await explicit confirmation before proceeding.
