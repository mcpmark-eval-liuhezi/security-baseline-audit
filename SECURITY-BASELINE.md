# Security Baseline — Dependency Sweep

## Metadata
- **Repository:** `security-baseline-audit`
- **Owner:** `mcpmark-eval-liuhezi`
- **Tracking issue:** #1 ("Security posture baseline")
- **Default branch:** `main`
- **Sweep date:** recorded during the security-audit dry-run setup

## Baseline check results

| # | Check | Result |
|---|-------|--------|
| 1 | Dependabot alerts | **Not accessible** — API returned `403 Resource not accessible by personal access token` when listing `/dependabot/alerts`. The token used for this sweep lacks the `security_events` scope. No alerts could be read, so an empty or populated state could not be confirmed. |
| 2 | Code scanning alerts | **Not accessible** — API returned `403 Resource not accessible by personal access token` when listing `/code-scanning/alerts`. Same missing `security_events` scope. No alerts could be read, so an empty or populated state could not be confirmed. |
| 3 | Secret scanning alerts | **Not accessible** — API returned `403 Resource not accessible by personal access token` when listing `/secret-scanning/alerts`. Same missing `security_events` scope. No alerts could be read, so an empty or populated state could not be confirmed. |

> **Important:** None of the three checks returned a confirmed empty result. Each call failed with a
> permissions error, meaning the true alert count is unknown until re-run with a token that grants
> the `security_events` scope (or by viewing the Security tab in the repository UI as an org admin).

## Remediation sandbox layout
- `main` — default branch, holds the README and this baseline once merged
- `audit/dependency-sweep` — this branch; contains the sweep record and the "Security baseline checklist" draft PR
- `audit/secret-rotation` — reserved for the secret-rotation portion of the dry-run

## Re-running the checks with proper access
To get a true baseline before the demo, either:
1. Re-generate the token with the `security_events` scope (plus `repo`), or
2. Open the repository **Security → Alerts** tabs directly in the browser.

Given the repo was freshly initialized with only a README and no code, no dependencies, and no
commits containing secrets, the expected result of all three checks is empty — but this is an
expectation, not a verified reading.
