## Parent PRD

#1

## What to build

Implement ingestion adapter interface and one concrete provider that can fetch bookmark-like records (mock/dev provider for tracer-bullet verification) with explicit auth/config errors surfaced in UI. This covers the ingestion flexibility and explicit error handling requirements from the parent PRD.

## Acceptance criteria

- [ ] Adapter contract exists and is exercised through sync flow.
- [ ] Provider returns bookmark records from configurable source.
- [ ] Missing/invalid config yields actionable error in UI.

## Blocked by

- Blocked by #<issue-01-number>

## User stories addressed

- User story 1
- User story 3
- User story 19
- User story 20
