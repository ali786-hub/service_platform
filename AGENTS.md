# Agent Guidelines & Repository Governance - Service Platform

## 1. Repository Purpose

This repository contains the **Local Verified Services Marketplace**.

The intended product vision will eventually support both:
- A mobile-first responsive website
- Native or cross-platform mobile applications

The currently approved delivery sequence is **web-first, not web-only** (per [NFR-001](docs/Local_Services_Marketplace_SRS_v0.2_Gold.md#L798-L803)). Native or cross-platform mobile applications must **not** be presented or built as part of the first implementation (V1_Initial) unless the governing requirements are formally amended by the founder.

---

## 2. Document Authority Order

When interpreting requirements, design constraints, and implementation choices, all agents and contributors must strictly adhere to the following hierarchy of authority:

1. **Founder decisions explicitly recorded through an approved amendment**
2. **Gold SRS v0.2** ([docs/Local_Services_Marketplace_SRS_v0.2_Gold.md](docs/Local_Services_Marketplace_SRS_v0.2_Gold.md))
3. **Approved Domain Model v0.1** ([docs/Local_Services_Marketplace_Domain_Model_v0.1.md](docs/Local_Services_Marketplace_Domain_Model_v0.1.md))
4. **Approved product and policy decisions**
5. **Approved architecture decisions**
6. **Approved logical and physical data designs**
7. **Implementation plans and acceptance criteria**
8. **Historical validation and evidence documents**
9. **Agent-generated summaries and reports**

**Critical Rule:** Later documents and lower-tier artifacts may refine concrete implementation choices, but they **must not** silently override, contradict, or reinterpret higher-authority requirements or decisions.

---

## 3. Current Document Status

The governance and specification documents currently hold the following explicit statuses. Agents must not upgrade any candidate or draft to approved status:

- **Gold SRS v0.2** ([docs/Local_Services_Marketplace_SRS_v0.2_Gold.md](docs/Local_Services_Marketplace_SRS_v0.2_Gold.md)):  
  **Approved** and authoritative requirements baseline.
- **Domain Model v0.1** ([docs/Local_Services_Marketplace_Domain_Model_v0.1.md](docs/Local_Services_Marketplace_Domain_Model_v0.1.md)):  
  **Approved** domain baseline, although its signature table still requires administrative cleanup.
- **Architecture and Data Design v0.1** ([docs/Local_Services_Marketplace_Architecture_and_Data_Design_v0.1.md](docs/Local_Services_Marketplace_Architecture_and_Data_Design_v0.1.md)):  
  **Candidate** awaiting founder approval.
- **V1 Product and Policy Baseline v0.1** ([docs/Local_Services_Marketplace_V1_Product_and_Policy_Baseline_v0.1.md](docs/Local_Services_Marketplace_V1_Product_and_Policy_Baseline_v0.1.md)):  
  **Corrected coordinated candidate** awaiting joint approval.
- **Logical Data Model v0.1** ([docs/Local_Services_Marketplace_Logical_Data_Model_v0.1.md](docs/Local_Services_Marketplace_Logical_Data_Model_v0.1.md)):  
  **Corrected coordinated candidate** awaiting joint approval.
- **DATABASE_DESIGN_V1.md** ([docs/DATABASE_DESIGN_V1.md](docs/DATABASE_DESIGN_V1.md)):  
  **Draft for founder review**. It is **not** an approved schema and must **not** be used to generate database migrations until formally approved.
- **Validation Evidence and Review Bundles** ([docs/VALIDATION_PRIMARY_EVIDENCE.txt](docs/VALIDATION_PRIMARY_EVIDENCE.txt), [docs/VALIDATION_REVIEW_BUNDLE.txt](docs/VALIDATION_REVIEW_BUNDLE.txt)):  
  **Historical evidence and review material**. They document experimental findings and historical state; they are **not** current product requirements.

---

## 4. Architecture Direction

The repository is organized to support a **cloud-portable modular monolith** for V1:

- **Modular Monolith for V1**: V1 uses a single primary backend application with internally enforced modules unless the founder formally approves an architecture amendment.
- **Role of `services/`**: The `services/` directory is the location for backend application code and internally modular business capabilities (logical modules and bounded contexts), **not** independently deployed microservices.
- **Bounded Contexts**: Logical subdomains and bounded contexts (Marketplace, Fulfilment, Provider, Reputation, Trust & Safety, Taxonomy, Markets, Identity, Communication) reside inside one backend application sharing one authoritative relational database.
- **Infrastructure Constraints**: No agent may introduce microservices, Kafka, Kubernetes, event streaming clusters, or multi-region active-active distributed infrastructure without an explicit, approved architecture decision.

---

## 5. Agent Operating Rules

All agents operating in this repository must strictly adhere to the following non-negotiable rules:

1. **Strict Step-by-Step Execution**: Work sequentially, one instruction at a time. Never jump ahead without explicit user confirmation.
2. **Perform Only Assigned Tasks**: Perform only the explicitly assigned task. Do not make unprompted changes across the codebase.
3. **Never Invent Requirements**: Never invent product requirements, business rules, features, or domain policies not explicitly documented in authoritative baselines.
4. **Never Resolve OPEN Requirements Autonomously**: Never resolve an OPEN requirement (such as items in the Open Requirements Register) without explicit founder approval.
5. **Never Silently Choose Between Conflicting Documents**: If documents or instructions conflict, stop immediately. Do not make unilateral assumptions.
6. **Conflict Reporting Protocol**: When sources conflict, stop and report:
   - The conflicting statements
   - Their file paths
   - Their respective authority levels (per Section 2)
   - The explicit decision required from the founder
7. **No Governing Document Edits During Implementation**: Never modify governing documents (`docs/` specifications, SRS, architecture, or policy files) during an implementation task.
8. **No Database Changes During Frontend Tasks**: Never modify the database design, schema, or queries during frontend work.
9. **No Migrations From Unapproved Designs**: Never generate or execute database migrations from an unapproved database design (such as [docs/DATABASE_DESIGN_V1.md](docs/DATABASE_DESIGN_V1.md) while it remains in Draft status).
10. **Preserve Historical Evidence**: Never delete or alter historical validation evidence (such as [docs/VALIDATION_PRIMARY_EVIDENCE.txt](docs/VALIDATION_PRIMARY_EVIDENCE.txt) or [docs/VALIDATION_REVIEW_BUNDLE.txt](docs/VALIDATION_REVIEW_BUNDLE.txt)) because it is flawed, inconvenient, or superseded.
11. **Never Push Directly to Main**: Never push directly to main unless the founder explicitly requests it.
12. **Never Commit Unless Explicitly Requested**: Never commit unless explicitly requested by the founder.
13. **Keep Changes Bounded and Reviewable**: Keep each change bounded, minimal, and reviewable.
14. **Task-Relevant Validation Only**: Run only validation relevant to the assigned task.
15. **Report Every Changed File**: Explicitly list every file modified, created, or deleted.
16. **Report Validation Performed**: Document the exact validation commands executed and their results.
17. **Report Unresolved Concerns**: Surface any ambiguities, assumptions, or unresolved concerns immediately.
18. **Stop After Assigned Task**: Stop immediately after completing the assigned task; do not continue to speculative next steps without confirmation.

---

## 6. Web and Mobile Delivery Sequence

- **Web-First Implementation**: The currently approved first implementation is a mobile-first responsive web application.
- **Web-First Does Not Mean Web-Only**: The intended product may later provide Android and iOS applications.
- **Client-Independent Backend**: Backend APIs and authoritative business behavior should remain client-independent where practical.
- **No Authority Duplication in Clients**: Mobile clients must not duplicate authoritative marketplace rules that belong on the backend.
- **Amendment Required for Mobile Priority**: Changing the approved delivery sequence requires a recorded founder amendment.

---

## 7. Repository Directory Responsibilities

- **`apps/`**: Client applications, beginning with the responsive web client. Future mobile clients may also live here after approval.
- **`services/`**: The single backend application and its internally modular business capabilities. The name does not imply microservices.
- **`packages/`**: Genuinely shared libraries, schemas, and tooling. Do not use it as a dumping ground for domain logic.
- **`tooling/`**: Reproducible development, formatting, linting, testing, and build configuration.
- **`docs/`**: Governing, candidate, draft, and historical documents, whose authority is determined by documented status.
- **`.agents/`**: Supporting workflows, policies, prompts, and templates.
- **`.github/`**: Repository automation, CI, and collaboration configuration.

---

## 8. Agent Instruction Precedence

- **Canonical Entry Point**: `AGENTS.md` is the canonical repository entry point for Antigravity, Jules, and other coding agents.
- **Support Role of `.agents/`**: `.agents/` supports `AGENTS.md` but cannot override it.
- **Prompts Cannot Override Specs**: Prompts cannot silently override governing documents.
- **Explicit Founder Exceptions**: A task-specific founder instruction may authorize a bounded exception, but the exception must be explicit and reported.
- **Stop on Ambiguity or Contradiction**: If an instruction appears unsafe, contradictory, or broader than requested, stop and report it immediately.

---

## 9. Required Completion Report

Every agent must provide a structured completion report detailing:

1. **Task performed**
2. **Files changed**
3. **Files deliberately not changed**
4. **Validation commands executed**
5. **Validation results**
6. **Assumptions made**
7. **Conflicts or unresolved concerns**
8. **Commit and push status**
