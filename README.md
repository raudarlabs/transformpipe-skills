# TransformPipe skills

Free agent skills for [TransformPipe](https://transformpipe.com), the open-source converter between
documents and Markdown. Each skill is a folder with a `SKILL.md`. They work in Claude (Claude.ai,
Claude Desktop, Claude Code) and in other agents that read the same format.

| Skill | What it does |
| --- | --- |
| [`publish-markdown`](publish-markdown/SKILL.md) | Saves what the agent writes and shares it as a page with a link, through the TransformPipe MCP connector |
| [`confluence-to-markdown`](confluence-to-markdown/SKILL.md) | Moves a Confluence space to Markdown files in a folder tree, with links between pages working |
| [`notion-export-to-markdown`](notion-export-to-markdown/SKILL.md) | Cleans a Notion "Markdown & CSV" export: ids off the names, databases as tables, pictures embedded |

## Install

- **Claude Code:** copy a skill folder into `~/.claude/skills/` for all projects, or into
  `.claude/skills/` for a single repository.
- **Claude.ai and Claude Desktop:** zip the skill folder and upload it under
  **Settings → Capabilities → Skills**.

`publish-markdown` also needs the TransformPipe connector:

- Claude: add it from the [connector directory](https://claude.ai/directory/tp).
- Any other MCP client: add `https://transformpipe.com/api/mcp` as a remote server. Sign-in is
  OAuth, so no API key is needed.

## Links

- Converter: https://transformpipe.com
- For agents: https://transformpipe.com/agents
- Source: https://github.com/raudarlabs/transformpipe

MIT licensed.
