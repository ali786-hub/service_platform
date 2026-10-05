# Agent Guidelines & Workflow - Service Platform

## Core Directives
1. **Strict Step-by-Step Execution**: Follow user instructions sequentially, one by one. Do not jump ahead without explicit confirmation.
2. **Clarity & Transparency**: Clearly report completed actions, files modified, and wait for feedback or the next command.
3. **High Quality & Standards**: Adhere to clean code practices, maintain clear documentation, and ensure maintainability.
4. **Verification**: Validate code changes and configurations before proceeding.

## Project Structure
```text
service_platform/
├── AGENTS.md        # Agent guidelines and project instructions
├── README.md        # Project overview and getting started guide
├── .agents/         # Antigravity agent configuration, rules, and skills
├── .github/         # CI/CD workflows, issue templates, and automation
├── apps/            # Frontend applications and user interfaces
├── services/        # Backend microservices and business logic
├── packages/        # Shared libraries, utilities, and common schemas
├── tooling/         # Build tools, configuration, and scripts
└── docs/            # Architecture specifications, diagrams, and guides
```

## Module Descriptions
- **`apps/`**: Client-facing and administrative applications (e.g. web portals, dashboards).
- **`services/`**: Independent backend services handling core business domains, APIs, and background processing.
- **`packages/`**: Reusable internal packages shared across apps and services (e.g. models, validation, types, auth helpers).
- **`tooling/`**: Shared development configs, linting, Docker setups, and local dev scripts.
- **`docs/`**: Project documentation, architectural decision records (ADRs), and setup instructions.
- **`.agents/`**: Antigravity agents, skills, and rule definitions.
