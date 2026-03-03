## Create child issues for PRD #1

Use these commands in order to create issues and fill real dependencies as issue numbers are returned.

### 1. Create slice 1

```bash
gh issue create --repo mm-parthy/my-bookmarks \
  --title "[Slice 1][AFK] Bootstrap app with one-click dry-run sync" \
  --body-file docs/issues/generated/issue-01-bootstrap.md
```

### 2. Create slice 2 (replace blocker placeholder)

1) Replace `#<issue-01-number>` in `docs/issues/generated/issue-02-ingestion-adapter.md`.

```bash
gh issue create --repo mm-parthy/my-bookmarks \
  --title "[Slice 2][AFK] Source ingestion adapter (MVP contract + mock provider)" \
  --body-file docs/issues/generated/issue-02-ingestion-adapter.md
```

### 3. Create slice 3 (replace blocker placeholder)

1) Replace `#<issue-02-number>` in `docs/issues/generated/issue-03-normalization.md`.

```bash
gh issue create --repo mm-parthy/my-bookmarks \
  --title "[Slice 3][AFK] Canonical model normalization + deterministic ID mapping" \
  --body-file docs/issues/generated/issue-03-normalization.md
```

### 4. Create slice 4 (replace blocker placeholder)

1) Replace `#<issue-03-number>` in `docs/issues/generated/issue-04-markdown-writer.md`.

```bash
gh issue create --repo mm-parthy/my-bookmarks \
  --title "[Slice 4][AFK] Markdown writer with idempotent upsert to flat folder" \
  --body-file docs/issues/generated/issue-04-markdown-writer.md
```

### 5. Create slice 5 (replace blocker placeholder)

1) Replace `#<issue-04-number>` in `docs/issues/generated/issue-05-orchestration.md`.

```bash
gh issue create --repo mm-parthy/my-bookmarks \
  --title "[Slice 5][AFK] Best-effort sync orchestration with run summary" \
  --body-file docs/issues/generated/issue-05-orchestration.md
```

### 6. Create slice 6 (replace blocker placeholder)

1) Replace `#<issue-05-number>` in `docs/issues/generated/issue-06-checkpointing.md`.

```bash
gh issue create --repo mm-parthy/my-bookmarks \
  --title "[Slice 6][AFK] Incremental checkpointing for on-demand reruns" \
  --body-file docs/issues/generated/issue-06-checkpointing.md
```

### 7. Create slice 7 (replace blocker placeholder)

1) Replace `#<issue-02-number>` in `docs/issues/generated/issue-07-production-adapter-hitl.md`.

```bash
gh issue create --repo mm-parthy/my-bookmarks \
  --title "[Slice 7][HITL] Real X data access decision and production adapter" \
  --body-file docs/issues/generated/issue-07-production-adapter-hitl.md
```

### 8. Create slice 8 (replace blocker placeholder)

1) Replace `#<issue-05-number>` in `docs/issues/generated/issue-08-post-processing-hook.md`.

```bash
gh issue create --repo mm-parthy/my-bookmarks \
  --title "[Slice 8][AFK] Optional post-processing hook for similar-content grouping" \
  --body-file docs/issues/generated/issue-08-post-processing-hook.md
```
