---
name: wordpress-status
description: Verify your WordPress.com connection and see which sites are available, without making any changes
---

# WordPress.com connection and sites

Call only the WordPress.com MCP tool `wpcom-user-sites`. This command is strictly read-only: do not call other tools or change any WordPress.com data or settings.

Treat the tool's live schema and response as authoritative. Request the first page of up to 10 sites, ordered newest-first using the tool's supported update sort. If the user supplied a site name, domain, or URL, apply the tool's supported search input.

Do not recreate or infer the server's authentication states, error taxonomy, field meanings, or remediation. If the tool returns a structured error, preserve its message and any server-provided guidance in a concise response.

If Cursor reports that the locally installed plugin's MCP cannot run in the current Cloud Agent environment, report **Local execution required**. Tell the user to start a new task, choose **This Mac** from the environment menu below the prompt, and rerun `/wordpress-status`. Do not describe this environment limitation as a WordPress.com connection failure.

## Present the result

- Use `pagination.total_sites` for the accessible-site total, when returned.
- Show at most 10 rows with `Site`, `Updated`, and `Visibility` columns.
- Display `primary_domain` as the site label and link it to `site_url`. If either field is missing, show only the returned value or `—`.
- Format `last_updated` as a compact relative value such as `Today` or `2d ago`; show `—` when missing. Do not describe it as publishing activity.
- Map `is_private: false` to `Public` and `is_private: true` to `Private`; show `—` when missing.
- Do not infer or add site titles, URLs, visibility, launch state, environment, or other metadata.
- Do not add a `Recents` heading or a pagination footer.
- A successful site-list request proves only that this read is available. Do not claim that other WordPress.com actions are enabled.

For a successful read, use this shape and omit the sites summary when `pagination.total_sites` was not returned:

```markdown
## WordPress.com — Site Status

**Connection**: Connected\
**Sites**: N · [View all](https://my.wordpress.com/sites)

| Site | Updated | Visibility |
| ---- | ------- | ---------- |
| [primary-domain.example](https://site-url.example) | 2d ago | Public |
```

For an error returned by the tool, use:

```markdown
## WordPress.com — Site Status

**Connection**: Could not verify\
**Detail**: [Preserved server error and guidance]
```

Do not dump raw tool responses or mention unrelated integrations.
