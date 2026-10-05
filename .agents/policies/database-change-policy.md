# Policy: Database Change Policy

This policy governs database migrations, schema definitions, and data mutations within `service_platform`.

---

## Core Rules

### 1. Migrations Only (No Manual Alterations)
- All schema changes must be codified into forward and backward (up/down) versioned migrations.
- Direct ad-hoc execution of DDL against production or staging databases is strictly forbidden.

### 2. Backward Compatibility First (Zero-Downtime)
- Changes must follow the **Expand and Contract** pattern:
  - **Phase 1 (Expand)**: Add new columns/tables with nullable defaults or defaults. Support both old and new code paths.
  - **Phase 2 (Migrate)**: Backfill data and switch application traffic to write to new structures.
  - **Phase 3 (Contract)**: Drop old, unused columns/tables only after all services have transitioned.

### 3. Non-Blocking DDL
- Avoid locking entire tables for extended periods.
- Create indexes concurrently (`CREATE INDEX CONCURRENTLY` in Postgres) or use database-appropriate non-blocking flags.
- Avoid large-table default values that require table-wide rewrites if not supported by the database engine.

### 4. Data Safety & Reversibility
- Destructive operations (`DROP TABLE`, `DROP COLUMN`) require explicit user confirmation and verified rollback scripts.
- Never write destructive migrations in the same deployment step as new feature code.
