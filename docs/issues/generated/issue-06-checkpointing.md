## Parent PRD

#1

## What to build

Track sync cursor/checkpoint state to reduce redundant processing while preserving correctness on reruns. This follows the checkpointing implementation decision in the parent PRD.

## Acceptance criteria

- [ ] Checkpoint state persisted between runs.
- [ ] Subsequent syncs process only new/changed records when possible.
- [ ] Manual reset/force-full-sync path is available.

## Blocked by

- Blocked by #<issue-05-number>

## User stories addressed

- User story 11
- User story 12
