---
name: notion-export-to-markdown
description: Turn a Notion "Markdown & CSV" export into clean Markdown, with ids stripped from names, databases as tables and pictures embedded, using TransformPipe's free converter. Use when the user is leaving Notion, backing it up, moving notes to Obsidian or Git, or asks why their Notion export has long ids in every file name.
---

# Notion export to clean Markdown

Notion's own export is Markdown, but every file and folder name carries a 32-character id, and each
database arrives as a `.csv`. TransformPipe cleans that up. It runs in the browser at
https://transformpipe.com/notion-to-markdown and is free and open source (MIT). Nothing is uploaded
unless the user signs in and saves.

The export and the upload are the user's steps. The agent guides them and works with the result.

## 1. Export from Notion

1. In Notion, open **Settings** and find **Export all workspace content** in the workspace
   settings. For one page and its subpages, use the page's `•••` menu → **Export** instead.
2. Choose **Markdown & CSV**. Turn on **Include subpages** for a page export.
3. Download the `.zip`. Do not unpack it.

## 2. Convert it

1. Open https://transformpipe.com/notion-to-markdown and drop the `.zip`. Up to 250 MB works.
2. What comes across:
   - **Pages:** every non-empty `.md` file becomes a document named after its title, id removed,
     with one title heading rather than two.
   - **Subpages:** they go into a folder of the same name, parent page first.
   - **Databases:** every `.csv` becomes a Markdown table, its first row the header.
   - **Pictures:** they are embedded in their page.
   - **Formatting:** headings, lists, to-dos, quotes, code, emphasis and web links stay as Notion
     wrote them.
3. By default the result is a **folder of pages**. Download it as a `.zip` of Markdown files, or
   sign in and save it to a TransformPipe account. There it is searchable, shareable and reachable
   from the agent through the TransformPipe MCP connector.
4. **One document** gives a single file instead: a contents list, then every page under its own
   heading, with databases last.

## 3. What to tell the user before they rely on it

- **Links between Notion pages keep their words but lose their address.** Notion links pages by
  the exported file names, which the cleaned-up files no longer have. Check pages that depended on
  internal links.
- **Links to a database's `.csv`** behave the same way.
- **PDFs and other attachments** are not read.
- **A `.zip` inside the export** is not opened.
- **Very large pictures** past the page's allowance keep their old relative path instead of being
  embedded.

Spot-check a page with a database, a page with pictures and a deeply nested page before deleting
anything in Notion.
