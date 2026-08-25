---
name: edit-wordpress-block-content
description: Create and edit serialized WordPress block content for posts, pages, patterns, templates, and template parts. Use when a task creates, edits, or transforms content containing WordPress block markup.
---

# Edit WordPress Block Content

## Discover Site Context

- When the target site is known, use the WordPress.com site editor context tool to discover its allowed block types before creating or editing content.
- When styling content, load the current theme presets and styles. Prefer supported theme tokens and block attributes over hard-coded values or custom CSS.
- When site context is unavailable, use core blocks and custom blocks already present in the supplied content.

## Produce Editable Content

- Keep content editable in the WordPress Block Editor or Site Editor by using registered blocks and valid serialized block markup.
- Keep block attributes and saved markup consistent.
- Preserve unfamiliar custom blocks, dynamic blocks, references, attributes, classes, and inner markup unless the request changes them.
- Preserve decorative HTML comments only when they are part of supplied content; add structural comments only as valid block delimiters.
- Use real media IDs, URLs, reusable-block references, and custom block attributes returned by WordPress.com tools or supplied by the user.

## Safe Workflow

1. Identify the target WordPress.com site with the user sites tool.
2. Read the existing content before applying an update.
3. Load block and theme context when layout or styling is involved.
4. Make the smallest change that satisfies the request while preserving unrelated blocks and metadata.
5. Create new posts and pages as drafts unless the user explicitly requests and confirms publication.
6. Return the edit and preview links supplied by WordPress.com after a successful write.
