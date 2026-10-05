# Agent Guidelines & Repository Governance - Service Platform

## 1. Repository Purpose

This repository contains the **Local Verified Services Marketplace**.

The intended product vision will eventually support both:
- A mobile-first responsive website
- Native or cross-platform mobile applications

The currently approved delivery sequence is **web-first, not web-only** (per [NFR-001](file:///c:/FYP/service_platform/docs/Local_Services_Marketplace_SRS_v0.2_Gold.md#L798-L803)). Native or cross-platform mobile applications must **not** be presented or built as part of the first implementation (V1_Initial) unless the governing requirements are formally amended by the founder.

---

## 2. Document Authority Order

When interpreting requirements, design constraints, and implementation choices, all agents and contributors must strictly adhere to the following hierarchy of authority:

1. **Founder decisions explicitly recorded through an approved amendment**
2. **Gold SRS v0.2** ([`docs/Local_Services_Marketplace_SRS_v0.2_Gold.md`](file:///c:/FYP/service_platform/docs/Local_Services_Marketplace_SRS_v0.2_Gold.md))
3. **Approved Domain Model v0.1** ([`docs/Local_Services_Marketplace_Domain_Model_v0.1.md`](file:///c:/FYP/service_platform/docs/Local_Services_Marketplace_Domain_Model_v0.1.md))
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

- **Gold SRS v0.2** ([`docs/Local_Services_Marketplace_SRS_v0.2_Gold.md`](file:///c:/FYP/service_platform/docs/Local_Services_Marketplace_SRS_v0.2_Gold.md)):  
  **Approved** and authoritative requirements baseline.
- **Domain Model v0.1** ([`docs/Local_Services_Marketplace_Domain_Model_v0.1.md`](file:///c:/FYP/service_platform/docs/Local_Services_Marketplace_Domain_Model_v0.1.md)):  
  **Approved** domain baseline, although its signature table still requires administrative cleanup.
- **Architecture and Data Design v0.1** ([`docs/Local_Services_Marketplace_Architecture_and_Data_Design_v0.1.md`](file:///c:/FYP/service_platform/docs/Local_Services_Marketplace_Architecture_and_Data_Design_v0.1.md)):  
  **Candidate** awaiting founder approval.
- **V1 Product and Policy Baseline v0.1** ([`docs/Local_Services_Marketplace_V1_Product_and_Policy_Baseline_v0.1.md`](file:///c:/FYP/service_platform/docs/Local_Services_Marketplace_V1_Product_and_Policy_Baseline_v0.1.md)):  
  **Corrected coordinated candidate** awaiting joint approval.
- **Logical Data Model v0.1** ([`docs/Local_Services_Marketplace_Logical_Data_Model_v0.1.md`](file:///c:/FYP/service_platform/docs/Local_Services_Marketplace_Logical_Data_Model_v0.1.md)):  
  **Corrected coordinated candidate** awaiting joint approval.
- **DATABASE_DESIGN_V1.md** ([`docs/DATABASE_DESIGN_V1.md`](file:///c:/FYP/service_platform/docs/DATABASE_DESIGN_V1.md)):  
  **Draft for founder review**. It is **not** an approved schema and must **not** be used to generate database migrations until formally approved.
- **Validation Evidence and Review Bundles** ([`docs/VALIDATION_PRIMARY_EVIDENCE.txt`](file:///c:/FYP/service_platform/docs/VALIDATION_PRIMARY_EVIDENCE.txt), [`docs/VALIDATION_REVIEW_BUNDLE.txt`](file:///c:/FYP/service_platform/docs/VALIDATION_REVIEW_BUNDLE.txt)):  
  **Historical evidence and review material**. They document experimental findings and historical state; they are **not** current product requirements.

---

## 4. Architecture Direction

The repository is organized to support a **cloud-portable modular monolith** for V1:

- **Modular Monolith for V1**: V1 uses a single primary backend application with internally enforced modules unless the founder formally approves an architecture amendment.
- **Role of `services/`**: The `services/` directory is the location for backend application code and internally modular business capabilities (logical modules and bounded contexts), **not** independently deployed microservices.
- **Bounded Contexts**: Logical subdomains and bounded contexts (Marketplace, Fulfilment, Provider, Reputation, Trust & Safety, Taxonomy, Markets, Identity, Communication) reside inside one backend application sharing one authoritative relational database.
- **Infrastructure Constraints**: No agent may introduce microservices, Kafka, Kubernetes, event streaming clusters, or multi-region active-active distributed infrastructure without an explicit, approved architecture decision.

### Repository Layout

```text
service_platform/
├── AGENTS.md        # Authoritative agent governance rules and repository instructions
├── README.md        # Project overview and orientation
├── .agents/         # Agent operations framework, workflows, policies, and templates
├── .github/         # CI/CD workflows and repository automation
├── apps/            # Frontend applications (starting with the web-first responsive client)
├── services/        # Backend application code and internally modular business capabilities
├── packages/        # Shared internal libraries, types, and schemas
├── tooling/         # Development configs, linters, and local build tooling
└── docs/            # Governing specifications, requirements, architecture, and design records
```

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
9. **No Migrations From Unapproved Designs**: Never generate or execute database migrations from an unapproved database design (such as [`docs/DATABASE_DESIGN_V1.md`](file:///c:/FYP/service_platform/docs/DATABASE_DESIGN_V1.md) while it remains in Draft status).
10. **Preserve Historical Evidence**: Never delete or alter historical validation evidence (such as [`docs/VALIDATION_PRIMARY_EVIDENCE.txt`](file:///c:/FYP/service_platform/docs/VALIDATION_PRIMARY_EVIDENCE.txt) or [`docs/VALIDATION_REVIEW_BUNDLE.txt`](file:///c:/FYP/service_platform/docs/VALIDATION_REVIEW_BUNDLE.txt)) because it is flawed, inconvenient, or superseded.
