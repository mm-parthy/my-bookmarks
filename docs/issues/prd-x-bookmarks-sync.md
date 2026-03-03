## Problem Statement

I save content in X bookmarks, but those bookmarks are hard to search and difficult to reliably rediscover later in the X app experience.

I want a lightweight, local-first workflow that lets me sync bookmarked posts from X into a centralized local store so I can search and browse them outside of X.

## Solution

Build a mini tool that performs one-way, on-demand sync from X bookmarks into local Markdown files.

The tool will include a small web UI (Next.js + shadcn/ui) with a “Sync now” button. On each sync run, the system will fetch bookmark items from X (via the chosen ingestion approach), normalize them, and write/update Markdown files using bookmark/post IDs as filenames in a flat folder.

Each Markdown file will contain:
- Frontmatter metadata (post ID, author, created date, sync timestamps, source URLs, etc.)
- Post content body
- Referenced links captured in structured metadata and readable body formatting

This is best-effort sync (not strict archival guarantees), optimized for quick MVP delivery and future extensibility.

## User Stories

1. As a person who saves many X bookmarks, I want to sync my bookmarks into local files, so that I am not locked into the X app for discovery.
2. As a person with many saved posts, I want local Markdown output, so that I can use my preferred editor/search workflows.
3. As a user, I want one-way sync from X to local, so that I can avoid accidental write-back behavior.
4. As a user, I want a clear “Sync now” button, so that I can manually control when sync runs.
5. As a user, I want each post saved with a stable ID-based filename, so that deduplication is straightforward.
6. As a user, I want key metadata in frontmatter, so that local tooling can index and filter bookmarks.
7. As a user, I want post content preserved in the Markdown body, so that I can read context without opening X.
8. As a user, I want referenced links captured, so that linked resources are searchable and reviewable.
9. As a user, I want sync to be best-effort and resilient, so that one bad item doesn’t fail the whole run.
10. As a user, I want sync logs and basic status in the UI, so that I can tell what happened after a run.
11. As a user, I want re-running sync to update existing files safely, so that my local store stays current.
12. As a user, I want sensible defaults with minimal setup, so that I can get value quickly.
13. As a user, I want local-only storage for now, so that I keep control over my data.
14. As a user, I want Docker-based deployment support, so that setup is consistent across environments.
15. As a user, I want a Node.js implementation, so that it aligns with the preferred stack.
16. As a user, I want a flat output folder structure, so that it remains simple to inspect and back up.
17. As a user, I want duplicate handling based on source identifiers, so that repeated syncs stay clean.
18. As a user, I want room for future post-processing (e.g., grouping similar content), so that quality can improve without redesign.
19. As a user, I want explicit error messaging if auth/ingestion is not configured, so that I know what to fix.
20. As a user, I want ingestion approach flexibility (official API and/or browser-extension-assisted path), so that I can adapt to practical access constraints.

## Implementation Decisions

- Build a local web app with a simple sync control surface using Next.js and shadcn/ui.
- Use one-way sync only: X bookmarks are read from source and written locally; no write-back to X.
- Persist each bookmark as a single Markdown document in a flat folder, keyed by source post ID.
- Store bookmark metadata in frontmatter and rendered post content in body markdown.
- Include referenced links in metadata and human-readable body sections.
- Treat sync as best-effort: continue processing independent items even if some fail.
- Use an ingestion adapter abstraction so the tool can support different source methods (e.g., official API path and browser-assisted path) without changing downstream processing.
- Use a normalization layer to transform source payloads into one canonical internal bookmark model.
- Use an output writer module that handles upsert behavior and deterministic file generation.
- Include a sync state/checkpoint module for incremental runs and repeatability of updates.
- Include an optional post-processing stage for future grouping/similarity workflows.
- Package runtime with Docker and Node.js-compatible startup.

## Testing Decisions

- Good tests focus on externally observable behavior, not implementation internals.
- Prioritize tests around canonical model normalization, markdown rendering fidelity, and idempotent file upserts.
- Validate that repeated sync runs do not create duplicate files for the same source item.
- Validate that metadata frontmatter is complete and consistently formatted.
- Validate that referenced links are preserved and rendered in expected output sections.
- Validate best-effort behavior: partial failures are reported while successful items still persist.
- Validate UI-level sync initiation and user-visible status transitions for success/failure.
- Validate ingestion adapter contract with mocked source responses.

## Out of Scope

- Two-way sync between local files and X.
- Guaranteed perfect archival of every post variant/media edge case.
- Advanced semantic deduplication/grouping in MVP (only interface hooks or placeholders).
- Multi-user support and access control.
- Cloud-hosted storage/search backends.
- End-to-end production hardening for enterprise scale.

## Further Notes

- Authentication and data-access approach for X is still a key discovery item and may drive implementation priority between adapters.
- MVP success criteria: a user can click “Sync now” and reliably produce/update local Markdown bookmark files with useful metadata and content.
- Future enhancements can include richer local search UX, similarity clustering, and better media handling once core sync is stable.
