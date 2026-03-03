## Parent PRD

- GitHub issue: https://github.com/mm-parthy/my-bookmarks/issues/1

## Proposed tracer-bullet vertical slices

### 1) Bootstrap app with one-click dry-run sync
- **Type**: AFK
- **Blocked by**: None - can start immediately
- **User stories covered**: 4, 10, 12, 14, 15
- **What to build**: Deliver a runnable Next.js + shadcn/ui app in Docker with a `Sync now` button that executes a stub sync pipeline and returns status/log output in UI.
- **Acceptance criteria**:
  - [ ] App runs in Docker and local Node.js dev mode.
  - [ ] UI shows `Sync now` action and run status.
  - [ ] Clicking `Sync now` executes end-to-end dry-run path and displays logs.

### 2) Source ingestion adapter (MVP adapter contract + mock provider)
- **Type**: AFK
- **Blocked by**: #1
- **User stories covered**: 1, 3, 19, 20
- **What to build**: Implement ingestion adapter interface and one concrete provider that can fetch bookmark-like records (mock/dev provider for tracer-bullet verification) with explicit auth/config errors surfaced in UI.
- **Acceptance criteria**:
  - [ ] Adapter contract exists and is exercised through sync flow.
  - [ ] Provider returns bookmark records from configurable source.
  - [ ] Missing/invalid config yields actionable error in UI.

### 3) Canonical model normalization + deterministic ID mapping
- **Type**: AFK
- **Blocked by**: #2
- **User stories covered**: 5, 6, 7, 8, 17
- **What to build**: Convert ingestion payloads into canonical bookmark model containing stable source ID, content, links, and required metadata.
- **Acceptance criteria**:
  - [ ] Normalized model includes required metadata fields and source ID.
  - [ ] Link extraction/reference mapping is captured in canonical structure.
  - [ ] Duplicate identifiers map to same canonical entity.

### 4) Markdown writer with idempotent upsert to flat folder
- **Type**: AFK
- **Blocked by**: #3
- **User stories covered**: 2, 5, 6, 7, 8, 11, 16, 17
- **What to build**: Persist canonical records as Markdown files in a flat folder named by source ID with frontmatter + body, supporting repeat-run updates without duplicate files.
- **Acceptance criteria**:
  - [ ] Files are written as `<source-id>.md` in flat output directory.
  - [ ] Frontmatter contains required metadata fields.
  - [ ] Repeat sync updates existing file instead of creating duplicates.

### 5) Best-effort sync orchestration with run summary
- **Type**: AFK
- **Blocked by**: #4
- **User stories covered**: 9, 10, 11, 12
- **What to build**: Orchestrate fetch→normalize→write with per-item error isolation and end-of-run summary counts for success/failure/skips shown in UI.
- **Acceptance criteria**:
  - [ ] Failure on one item does not abort entire run.
  - [ ] Run summary reports totals and failures.
  - [ ] UI presents latest run outcome clearly.

### 6) Incremental checkpointing for on-demand reruns
- **Type**: AFK
- **Blocked by**: #5
- **User stories covered**: 11, 12
- **What to build**: Track sync cursor/checkpoint state to reduce redundant processing while preserving correctness on reruns.
- **Acceptance criteria**:
  - [ ] Checkpoint state persisted between runs.
  - [ ] Subsequent syncs process only new/changed records when possible.
  - [ ] Manual reset/force-full-sync path is available.

### 7) Real X data access decision and production adapter
- **Type**: HITL
- **Blocked by**: #2
- **User stories covered**: 1, 3, 19, 20
- **What to build**: Finalize and implement production ingestion path (official API or extension-assisted), including required setup docs and runtime config.
- **Acceptance criteria**:
  - [ ] Human-approved ingestion strategy documented.
  - [ ] Production adapter runs end-to-end through existing sync pipeline.
  - [ ] Setup/docs allow another developer to execute a real sync.

### 8) Optional post-processing hook for similar-content grouping placeholder
- **Type**: AFK
- **Blocked by**: #5
- **User stories covered**: 18
- **What to build**: Introduce optional post-processing stage interface with a no-op/default implementation and one demonstrative grouping heuristic output.
- **Acceptance criteria**:
  - [ ] Post-processing hook can be toggled on/off.
  - [ ] Default behavior keeps current output unchanged.
  - [ ] Example grouping metadata is emitted when enabled.

## Dependency graph summary

- #1 → #2 → #3 → #4 → #5 → #6
- #2 → #7
- #5 → #8

## Draft GitHub issue bodies (template-filled)

### Issue draft for slice 1

## Parent PRD

#1

## What to build

Deliver a runnable Next.js + shadcn/ui app in Docker with a `Sync now` button that executes a stub sync pipeline and returns status/log output in UI. This tracer bullet validates the end-to-end path and deployment baseline described in the parent PRD Solution and Implementation Decisions sections.

## Acceptance criteria

- [ ] App runs in Docker and local Node.js dev mode.
- [ ] UI shows `Sync now` action and run status.
- [ ] Clicking `Sync now` executes end-to-end dry-run path and displays logs.

## Blocked by

None - can start immediately.

## User stories addressed

- User story 4
- User story 10
- User story 12
- User story 14
- User story 15

---

### Issue draft for slice 2

## Parent PRD

#1

## What to build

Implement ingestion adapter interface and one concrete provider that can fetch bookmark-like records (mock/dev provider for tracer-bullet verification) with explicit auth/config errors surfaced in UI. This covers the ingestion flexibility and explicit error handling requirements from the parent PRD.

## Acceptance criteria

- [ ] Adapter contract exists and is exercised through sync flow.
- [ ] Provider returns bookmark records from configurable source.
- [ ] Missing/invalid config yields actionable error in UI.

## Blocked by

- Blocked by #<slice-1-issue-number>

## User stories addressed

- User story 1
- User story 3
- User story 19
- User story 20

---

### Issue draft for slice 3

## Parent PRD

#1

## What to build

Convert ingestion payloads into canonical bookmark model containing stable source ID, content, links, and required metadata. This implements the normalization decision from the parent PRD and prepares deterministic downstream persistence.

## Acceptance criteria

- [ ] Normalized model includes required metadata fields and source ID.
- [ ] Link extraction/reference mapping is captured in canonical structure.
- [ ] Duplicate identifiers map to same canonical entity.

## Blocked by

- Blocked by #<slice-2-issue-number>

## User stories addressed

- User story 5
- User story 6
- User story 7
- User story 8
- User story 17

---

### Issue draft for slice 4

## Parent PRD

#1

## What to build

Persist canonical records as Markdown files in a flat folder named by source ID with frontmatter + body, supporting repeat-run updates without duplicate files. This is the core output behavior defined by the parent PRD solution.

## Acceptance criteria

- [ ] Files are written as `<source-id>.md` in flat output directory.
- [ ] Frontmatter contains required metadata fields.
- [ ] Repeat sync updates existing file instead of creating duplicates.

## Blocked by

- Blocked by #<slice-3-issue-number>

## User stories addressed

- User story 2
- User story 5
- User story 6
- User story 7
- User story 8
- User story 11
- User story 16
- User story 17

---

### Issue draft for slice 5

## Parent PRD

#1

## What to build

Orchestrate fetch→normalize→write with per-item error isolation and end-of-run summary counts for success/failure/skips shown in UI. This realizes the best-effort sync contract and user-facing visibility from the parent PRD.

## Acceptance criteria

- [ ] Failure on one item does not abort entire run.
- [ ] Run summary reports totals and failures.
- [ ] UI presents latest run outcome clearly.

## Blocked by

- Blocked by #<slice-4-issue-number>

## User stories addressed

- User story 9
- User story 10
- User story 11
- User story 12

---

### Issue draft for slice 6

## Parent PRD

#1

## What to build

Track sync cursor/checkpoint state to reduce redundant processing while preserving correctness on reruns. This follows the checkpointing implementation decision in the parent PRD.

## Acceptance criteria

- [ ] Checkpoint state persisted between runs.
- [ ] Subsequent syncs process only new/changed records when possible.
- [ ] Manual reset/force-full-sync path is available.

## Blocked by

- Blocked by #<slice-5-issue-number>

## User stories addressed

- User story 11
- User story 12

---

### Issue draft for slice 7

## Parent PRD

#1

## What to build

Finalize and implement production ingestion path (official API or extension-assisted), including required setup docs and runtime config. This HITL slice resolves the remaining product decision highlighted in Further Notes.

## Acceptance criteria

- [ ] Human-approved ingestion strategy documented.
- [ ] Production adapter runs end-to-end through existing sync pipeline.
- [ ] Setup/docs allow another developer to execute a real sync.

## Blocked by

- Blocked by #<slice-2-issue-number>

## User stories addressed

- User story 1
- User story 3
- User story 19
- User story 20

---

### Issue draft for slice 8

## Parent PRD

#1

## What to build

Introduce optional post-processing stage interface with a no-op/default implementation and one demonstrative grouping heuristic output. This preserves MVP scope while creating the extension seam called out in the parent PRD.

## Acceptance criteria

- [ ] Post-processing hook can be toggled on/off.
- [ ] Default behavior keeps current output unchanged.
- [ ] Example grouping metadata is emitted when enabled.

## Blocked by

- Blocked by #<slice-5-issue-number>

## User stories addressed

- User story 18
