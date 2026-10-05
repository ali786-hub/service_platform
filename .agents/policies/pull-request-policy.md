# Policy: Pull Request & Contribution Policy

This policy governs the creation, review, and merging of Pull Requests (PRs) in `service_platform`.

---

## 1. Branch Naming Conventions
Follow standardized prefixing for Git branches:
- `feat/<short-description>`: New user-facing features or capabilities.
- `fix/<short-description>`: Defect and bug fixes.
- `refactor/<short-description>`: Structural code changes with no behavior change.
- `chore/<short-description>`: Tooling, dependency updates, and maintenance.
- `docs/<short-description>`: Documentation changes only.

---

## 2. Commit Message Standards
Use Conventional Commits formatting:
```text
<type>(<scope>): <short imperative summary>

[optional body explaining motivation and changes]

[optional footer referencing issue numbers, e.g., Closes #123]
```
Examples:
- `feat(auth): add OAuth2 provider authentication`
- `fix(billing): correct stripe webhook signature verification`

---

## 3. Pull Request Requirements
- **Title**: Clean and descriptive matching the primary commit or feature.
- **Description**: Must detail:
  1. What changed.
  2. Why the change was made.
  3. How it was verified (tests run, screenshots for UI changes).
- **CI Status**: All automated workflows (linting, tests, build) must pass cleanly before any merge.
- **Merge Strategy**: Squash and merge or rebase merge to keep Git history linear and clean.
