# Agent Operations Framework

This directory contains the operational framework, standard workflows, governance policies, prompt templates, and documentation formats used by autonomous agents and developers working on `service_platform`.

## Directory Overview

```text
.agents/
├── README.md                  # Framework overview and usage guidelines
├── workflows/                 # Standard Operating Procedures (SOPs)
│   ├── implement-feature.md   # Feature design, coding, testing, and delivery
│   ├── fix-defect.md          # Bug triage, reproduction, minimal fix, verification
│   ├── review-code.md         # Comprehensive code review checklist
│   ├── improve-tests.md       # Test hardening, edge cases, and hygiene
│   └── update-ui-from-stitch.md # Syncing UI components and tokens from Stitch
├── policies/                  # Guardrails and hard constraints
│   ├── product-authority.md   # Authority matrix (autonomous vs human approval)
│   ├── database-change-policy.md # Migration standards and backward compatibility
│   ├── security-boundaries.md # Secrets handling, sanitization, and access boundaries
│   ├── dependency-policy.md   # Adding, updating, and auditing external libraries
│   └── pull-request-policy.md # Branch naming, commit conventions, and PR standards
├── prompts/                   # Reusable prompt runbooks
│   ├── scheduled-health-check.md # Routine health and build sanity verification
│   ├── weekend-maintenance.md # Housekeeping, dependency audits, cleanup tasks
│   └── bounded-feature-task.md # Scoped prompt for executing single feature slices
└── templates/                 # Standard document templates
    ├── task-brief.md          # Template for scoping tasks and features
    ├── decision-record.md     # Architectural Decision Record (ADR) template
    └── work-report.md         # Completion and verification report template
```

## How to Use This Framework

1. **Before Taking Action**: Read the corresponding policy in `policies/` to ensure full compliance with system constraints.
2. **Executing Tasks**: Follow the exact multi-step process defined in the relevant workflow in `workflows/`.
3. **Recording Work**: Use the standard templates in `templates/` for task briefs, architecture decisions, and summary reports.
4. **Autonomous Routines**: Utilize prompt files in `prompts/` for running scheduled maintenance and isolated tasks.
