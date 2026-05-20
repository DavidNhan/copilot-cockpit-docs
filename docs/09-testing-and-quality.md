# 09 Testing and Quality

## Purpose

This chapter defines quality assurance from test execution to rubric-based documentation acceptance.

## Quality Layers

1. Automated perspective tests
2. Data integrity tests
3. Manual visual verification for high-risk UI flows
4. Documentation quality scoring (rubric)

## Mandatory Quality Gates

- Relevant test suites pass for every change
- Cross-perspective navigation remains valid
- Integrity checks pass for catalog changes
- Documentation score remains >= 90%

## Rubric Coupling

Quality score is evaluated across:

- Completeness
- Correctness
- Traceability
- Maintainability
- Verifiability

Reference files:

- `quality/rubric.md`
- `quality/scorecard.md`
- `quality/iteration-log.md`

## Review Process

1. Draft and self-review
2. Domain review (architecture/security/operations)
3. Fix and re-score
4. Verify against hard exit criteria

## Acceptance Criteria

1. Score >= 90%
2. No criterion below 4/5
3. Completeness and correctness >= 4.5/5
