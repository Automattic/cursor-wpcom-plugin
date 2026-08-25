# WordPress.com for Cursor

Connect [Cursor](https://cursor.com) to WordPress.com through the official WordPress.com Model Context Protocol (MCP) server.

## Build & Publish with WordPress

Tell Cursor what kind of WordPress.com site you want—such as a portfolio, restaurant site, blog, or store—and provide the business, audience, and page requirements. WordPress can plan the site, prepare its content and design, and launch it.

For an existing site, connect your account to draft, publish, and schedule posts; review traffic; moderate comments; manage plugins; and change settings. WordPress.com exposes more than 70 site capabilities through the integration.

The plugin connects Cursor directly to WordPress.com so you can create or manage a site through conversation. Available actions depend on your WordPress.com permissions, site plan, platform capabilities, and enabled MCP settings.

## Included Components

- `.cursor-plugin/plugin.json` describes the Cursor plugin.
- `mcp.json` connects Cursor to the official WordPress.com remote MCP server.
- `skills/edit-wordpress-block-content/SKILL.md` guides Cursor to create native, editable WordPress block content.
- `commands/wordpress-status.md` adds a read-only connection and site-listing command.

The plugin contains no executable hooks, install scripts, runtime dependencies, or bundled credentials.

## Local Installation

During development, copy this repository into Cursor's local plugin directory:

```sh
mkdir -p ~/.cursor/plugins/local/wordpress-com
rsync -a --exclude='.git/' \
  /path/to/cursor-wpcom-plugin/ \
  ~/.cursor/plugins/local/wordpress-com/
```

Cursor currently rejects local-plugin symlinks whose targets resolve outside
`~/.cursor/plugins/local`, even though Cursor's plugin documentation recommends
symlinking for local development. Re-run the `rsync` command after making local
changes, then restart Cursor or run **Developer: Reload Window**.

After Cursor reloads:

1. Open **Customize** in the Cursor sidebar.
2. Find **WordPress.com** and verify that the plugin and `wordpress-com` MCP server are enabled.
3. Start authentication when Cursor prompts you, or use the MCP server's **Connect** action.
4. Sign in to WordPress.com and approve the requested access.

After publication, install **WordPress.com** directly from Cursor's marketplace instead.

## WordPress.com Setup

WordPress.com gives you control over which MCP actions are available to connected AI clients. Enable the account and site actions you want Cursor to use at:

https://wordpress.com/me/mcp

If Cursor reports that an ability is disabled, review those settings and retry the request. Enabling an action does not bypass WordPress.com user capabilities, site permissions, plan requirements, or confirmations.

## Example Requests

```text
List my WordPress.com sites and summarize their recent posts.
```

```text
Draft a post announcing our autumn event. Match the site's existing typography and colors.
```

```text
Change the call-to-action text on my About page while preserving the rest of its layout.
```

```text
/wordpress-status
```

## Authentication and Security

The plugin connects only to the official WordPress.com MCP endpoint:

```text
https://public-api.wordpress.com/wpcom/v2/mcp/v1
```

Authentication uses the MCP OAuth browser flow. Cursor manages the resulting OAuth credentials; this repository does not read, store, or transmit credentials itself.

WordPress.com applies the authenticated user's permissions and configured MCP controls to every operation. Review proposed changes before approving write or destructive actions. Revoke access through your WordPress.com security settings when the connection is no longer needed.

## Development

Validate the JSON files before publishing:

```sh
python3 -m json.tool .cursor-plugin/plugin.json >/dev/null
python3 -m json.tool mcp.json >/dev/null
```

To troubleshoot the MCP connection, open Cursor's **Output** panel and select **MCP Logs**.

## License

GPL-2.0-or-later. See [LICENSE](LICENSE).
