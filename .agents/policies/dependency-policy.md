# Policy: Dependency Management

This policy defines criteria for vetting, adding, updating, and auditing external third-party dependencies within `service_platform`.

---

## 1. Adding New Dependencies
- **Preference for Existing / Standard Libraries**: Always verify whether the required functionality can be achieved cleanly with language built-ins or packages already installed in the monorepo.
- **Vetting Criteria**:
  - Maintained: Active maintenance within the last 6 months.
  - License: Permissive open source license (MIT, Apache 2.0, BSD, ISC). Avoid viral copyleft licenses (GPL, AGPL) without explicit business sign-off.
  - Security History: No unpatched critical CVEs.
  - Size & Impact: Minimal bundle footprint, tree-shakeable for frontend libraries.
- **Approval**: Agents must ask for explicit confirmation before adding a new package to `package.json` or `pyproject.toml`.

---

## 2. Lockfiles & Reproducibility
- Monorepo package managers must commit exact lockfiles (`pnpm-lock.yaml`, `package-lock.json`, `poetry.lock`).
- Never run arbitrary upgrade commands (`npm update *`) across all packages without dedicated testing and regression passes.

---

## 3. Auditing & Vulnerability Management
- Regularly execute security audit commands (`npm audit`, `pip-audit`).
- Vulnerabilities categorized as High or Critical must be patched or mitigated immediately.
