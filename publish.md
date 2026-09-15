# Publish

Read `config.md` beside `SKILL.md`. Branch on `destination` only.

After any successful publish, remind: Status stays Draft or In review until a human Reviewer (not the author) completes Ground.

## local

1. Save Markdown under `local_dir` (create if needed). Short filename from the title. Overwrite same-session drafts when retrying.
2. Tell the user the file path.

## google-docs

1. Discover connectors:

```
GetDynamicTools with pattern "google|docs|drive"
```

2. **Available:** create a Doc with the one-pager title. Use `google_docs_folder_url` when set; otherwise ask once or use Drive default. Tell the user the Doc URL.
3. **Unavailable:** save a Markdown fallback under `local_dir` if set, else `one-pagers/`, and tell the user:

> Google Docs is not connected. To publish to Docs:
> 1. Open Cursor Settings, then MCP
> 2. Add a Google Docs or Google Drive connector
> 3. Authorize with your Google account
> 4. Re-run /to-onepager to publish
>
> A local Markdown copy was saved for manual paste.

## confluence

1. Discover connectors:

```
GetDynamicTools with pattern "confluence|atlassian|wiki"
```

2. **Available:** create a page in `confluence_folder_url`. Title = one-pager title. Body in HTML. Owner, Reviewer, and Recommendation owners use mention nodes when accountIds are resolved:

```html
<span data-type="mention" data-user-id="ACCOUNT_ID">@Display Name</span>
```

Resolve accountId via `atlassianUserInfo` (for "me") or Atlassian search / `discover` + `executeRead`. Ask if unresolved; never invent an ID.

Local Markdown copies: if `atlassian_site` is set, link `[Display Name]({atlassian_site}/wiki/people/ACCOUNT_ID)`; otherwise use the display name only.

Tell the user the page URL.

3. **Unavailable:** save a Markdown fallback under `local_dir` if set, else `one-pagers/`, and tell the user:

> Confluence is not connected. To publish to Confluence:
> 1. Open Cursor Settings, then MCP
> 2. Add a Confluence connector (Atlassian MCP)
> 3. Authorize with your Atlassian account
> 4. Re-run /to-onepager to publish
>
> A local Markdown copy was saved for manual paste.
> Configured folder: {confluence_folder_url}
