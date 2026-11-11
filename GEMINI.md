# Gemini Agent Operational Playbook

@AGENTS.md

## 1. Execution Environment (Google Cloud Vertex AI)
- When running headlessly via `run-gemini-cli`, model inference and telemetry run on Google Cloud Vertex AI:
  - **GCP Project ID:** `prj-d-ral-vtxai-kwr9`
  - **Primary Region:** `europe-west2`
- If a task in this repository explicitly requires calling Vertex AI APIs (`aiplatform.googleapis.com`), default to project `prj-d-ral-vtxai-kwr9` and location `europe-west2` via Application Default Credentials (ADC) — never hardcode API keys.

## 2. Automated Issue-to-PR Runbook (Headless CI Mode)
When triggered on a GitHub Issue to implement a fix or feature, execute these steps in order:
1. **Understand & Validate the Issue**
   - Read the full issue description and comments.
   - Search the codebase to locate the relevant modules and existing tests.
   - If the issue is ambiguous, unsafe, or lacks reproduction details, post a clarifying comment on the issue explaining what is needed and stop without opening a broken PR.
2. **Reproduce & Branch**
   - Fetch the latest target branch (`git fetch origin main`) and create branch `ai/issue-<number>-<slug>` from `origin/main`.
   - For bug reports, add or update a failing test case first to confirm reproduction where practical.
3. **Implement & Verify**
   - Implement the minimal code change needed to resolve the issue while following all rules in `AGENTS.md`.
   - Run the project's linter and test suite. Iterate until all checks pass. If tests still fail after 3 attempts, stop, leave a summary of findings on the issue, and do not push broken code.
4. **Push & Open Draft PR**
   - Stage only the intended source/test files (`git status` check — verify no temporary or credential files are untracked/staged).
   - Commit the changes, push the branch (`git push -u origin ai/issue-<number>-<slug>`), and open a **Draft Pull Request** against `main` via `gh pr create --draft`.