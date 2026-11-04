---
name: publish-markdown
description: Save a Markdown document the agent wrote and share it as a readable web page with a link, through the TransformPipe MCP connector. Use when the user says "save this", "publish it", "give me a link", "share it with someone", "make it private", or wants to find a document saved earlier.
---

# Publish Markdown as a page

This skill keeps what the agent writes and turns it into a page people can open. It works through
the TransformPipe MCP server at `https://transformpipe.com/api/mcp`. Sign-in is OAuth, so the
connector needs only that URL, and there is no API key.

If no `tp_` tools are available, tell the user to add the connector first. In Claude it is listed
in the connector directory at https://claude.ai/directory/tp. Other clients that support remote MCP
servers with OAuth can add the URL above directly.

## Save

- Call `tp_save_document` with the complete Markdown as `markdown` and a short, searchable `name`
  ("Q3 plan", "Migration spec: billing"), not "Document" or the first line.
- To file it, pass `folder` as a folder id or a path such as `Projects/Billing`. Call
  `tp_list_folders` to find one, or `tp_create_folder` to make one.
- Without `share`, the document is private. Saving privately needs no confirmation.

## Share

Sharing publishes. Ask the user before making anything public, and say who will be able to read it.

- **Anyone with the link:** `tp_share_document` with `mode: "link"`.
- **Named people only:** `mode: "people"` with `emails`. Each new address gets an email with the
  link and has to sign in to read it.
- **Stop sharing:** `mode: "private"`. The old link stops working at once.

`link` and `people` need `confirm: true`. The first call without it changes nothing and answers
with what would be disclosed. Show that to the user, and call again with `confirm: true` only after
they agree. Give the user the URL from the response.

## Change a saved document

- Use `tp_update_document` with the document's `id` and the complete new `markdown`. It keeps the
  id and the link, so people who already have the link see the new text.
- The previous text is kept as a revision. `tp_document_versions` lists the revisions.
- If the document is shared, the update needs `confirm: true`, because its readers will see the
  change. Say so before you send it.
- Do not use `tp_save_document` to change a document: that creates a second one with a new link.

## Find something saved earlier

- `tp_list_documents` with `query` searches titles and content, and `folder` narrows to a folder.
- `tp_get_document` returns the text (`as: "markdown"` or `"html"`).
- `tp_summarize_document` gives a short summary of a long document.

## Paste into other tools

`tp_convert_from_markdown` returns Markdown as `html`, `confluence` (storage format), `jira` (wiki
markup) or `slack` (mrkdwn), for pasting into those tools. It saves nothing.

## Delete

`tp_delete_document` always needs `confirm: true`. Confirm with the user first. A deleted document
stays in the Trash for 14 days, and `tp_restore_document` brings it back.

## Limits

- 4 MB per document.
- 5,000 documents and 250 MB per account.
- When a limit is reached the save is refused. Nothing is deleted to make room.
