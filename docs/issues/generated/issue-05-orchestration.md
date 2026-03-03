## Parent PRD

#1

## What to build

Orchestrate fetch→normalize→write with per-item error isolation and end-of-run summary counts for success/failure/skips shown in UI. This realizes the best-effort sync contract and user-facing visibility from the parent PRD.

## Acceptance criteria

- [ ] Failure on one item does not abort entire run.
- [ ] Run summary reports totals and failures.
- [ ] UI presents latest run outcome clearly.

## Blocked by

- Blocked by #<issue-04-number>

## User stories addressed

- User story 9
- User story 10
- User story 11
- User story 12
