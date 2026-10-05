# Policy: Security Boundaries & Secret Management

This policy defines mandatory security standards and guardrails to prevent vulnerabilities and data leakage across `service_platform`.

---

## 1. Secrets & Credentials Management
- **Zero Hardcoded Secrets**: Under no circumstances should API keys, passwords, database credentials, JWT secrets, or tokens be hardcoded in files or committed to Git.
- **Environment Variables**: Access all secrets exclusively through validated environment variables or secret vaults.
- **`.env` File Isolation**: Ensure `.env`, `.env.local`, and related sensitive files are listed in `.gitignore` and never committed.
- **Log Hygiene**: Never log sensitive payload attributes (passwords, tokens, PII, credit card numbers).

---

## 2. Input Validation & Defense-in-Depth
- **Strict Boundary Validation**: Every incoming request must be validated using runtime schema validators (e.g., Zod, Pydantic, JSON Schema) before processing.
- **Parameterized Queries**: Never concatenate raw strings into SQL queries. Always use parameterized queries or trusted ORM/query builder abstractions to prevent SQL injection.
- **Output Sanitization**: Prevent XSS by escaping or sanitizing dynamic user content rendered on the frontend.

---

## 3. Authentication & Authorization
- **Least Privilege Access**: Services and APIs must operate with minimal necessary permissions.
- **Explicit Access Controls**: Protected endpoints must explicitly declare and check authentication state and role-based permissions (RBAC) prior to executing business logic.
- **Safe Session Management**: Use secure, HTTP-only, SameSite cookies or signed tokens with short expiration lifespans.
