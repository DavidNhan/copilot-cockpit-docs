# 11 Runbooks and Troubleshooting

## Purpose

This chapter provides operational runbooks for frequent failure patterns.

## Runbook A: Page Fails to Render Data

Symptoms:

- Empty cards/lists
- Console fetch errors

Actions:

1. Validate JSON path and file availability
2. Verify JSON syntax and required fields
3. Run integrity tests
4. Re-test affected perspective pages

Exit condition:

- Page renders expected core content and tests pass

## Runbook B: Deep Links Broken

Symptoms:

- Hash links do not open expected detail contexts

Actions:

1. Verify anchor/ID naming consistency
2. Check cross-page link conventions
3. Execute navigation regression tests
4. Add targeted test for reproduced breakage

Exit condition:

- Deep link path works from source and direct route

## Runbook C: Governance/Security Reference Drift

Symptoms:

- Mappings outdated or unresolved

Actions:

1. Confirm source references
2. Mark verification status where needed
3. Update mapping data and change notes
4. Request domain review

Exit condition:

- References validated and documented with review date

## Runbook D: Release Regression

Actions:

1. Trigger rollback to last known good state
2. Open incident note in `changelog.md`
3. Reproduce and isolate root cause
4. Ship fix with new regression test
