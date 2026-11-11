# Repository Agent Guidelines

## 1. Project Overview & Commands
- **Language / Runtime:** Python 3.11+ (update to match your stack)
- **Install dependencies:** `pip install -e ".[dev]"` Use uv for dependency, linting and test management.
- **Run linter / formatter:** `ruff check . && ruff format --check .`
- **Run test suite:** `pytest -q`

Always run the linter and full test suite locally and confirm they pass before creating any commit.
## 2. Git & Branching Rules
- **Protected branches:** NEVER commit or push directly to `main`, `master`, or `release/*`.
- **Branch naming:** Create a fresh branch from `origin/main` for every issue using the format:
  `ai/issue-<number>-<short-kebab-summary>` (e.g., `ai/issue-42-fix-null-header`).
- **History hygiene:** Never run `git push --force`, `git reset --hard` on shared branches, or rewrite published commits.
- **Commit messages:** Use Conventional Commits (`fix: ...`, `feat: ...`, `test: ...`) and reference the issue (`Refs #<number>`).

## 3. Pull Request Requirements
- Always open Pull Requests as **Draft PRs** targeting `main` so a human reviewer approves before merge.
- Every PR description MUST include:
  1. `Fixes #<issue-number>` (or `Refs #<issue-number>` if partial).
  2. Root-cause summary and overview of changes made.
  3. Exact test commands executed and their pass/fail output.
  4. Any assumptions, edge cases, or follow-up questions for the human reviewer.
  
## 4. Security & Scope Boundaries
- Never read, log, commit, or echo secrets, tokens, `.env` files, private SSH keys, or credential files.
- Do not modify `.github/workflows/`, IAM/Terraform configs, or dependency lockfiles unless the issue explicitly requests it.
- Keep changes minimal and strictly scoped to the reported issue; do not perform unrelated refactoring.