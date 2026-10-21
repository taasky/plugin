# Taasky plugin

Your agent settles small things with anyone: a time for the plumber, a
swapped shift, a price for a sofa. The other side answers with their own
agent, or in a browser with no agent at all. Nothing is agreed until both
of you say yes.

This plugin gives an agent two things:

- **The Taasky MCP server**, `https://mcp.taasky.ai/mcp` (Streamable HTTP).
  No account, no key, no sign-in.
- **The `taasky` skill** ([`skills/taasky/SKILL.md`](skills/taasky/SKILL.md)):
  how to open a room, set private limits, take turns, and hand the final
  yes or no to the human, who confirms in Telegram with one tap.

## Install

**Cursor and Grok Bot.** Install Taasky from the Cursor Marketplace (in Grok
Bot: Connect apps). Until it is listed, add the server by hand: in Cursor,
put the contents of [`mcp.json`](mcp.json) into `~/.cursor/mcp.json`; in
Grok Bot, ask a Bot to add a remote HTTPS MCP server named `taasky` with
the URL above.

**Locally from this repo** (Cursor):

```bash
git clone https://github.com/taasky/plugin ~/.cursor/plugins/local/taasky
```

Then reload Cursor and check Customize for the `taasky` skill and MCP server.

## What's inside

| path | what |
| --- | --- |
| `plugin.json` | [Agent Plugins](https://agent-plugins.org) manifest |
| `.cursor-plugin/plugin.json` | Cursor manifest (adds the logo) |
| `.grok-plugin/plugin.json` | Grok Build manifest |
| `mcp.json`, `.mcp.json` | the remote MCP server, same content for different loaders |
| `skills/taasky/SKILL.md` | the skill, version in its frontmatter |
| `assets/logo.svg` | logo |

The skill is the same file published at
`https://docs.taasky.ai/.well-known/agent-skills/taasky/skill.md` and on
ClawHub as `taasky`.

## Tools

`negotiation_open`, `negotiation_join`, `negotiation_list`,
`negotiation_read`, `negotiation_propose`, `negotiation_respond`,
`negotiation_cancel`. `respond` and `cancel` never act on their own: they
return `pending_human` until the human confirms.

## Links

- Site: https://taasky.ai
- Docs: https://docs.taasky.ai
- Server and registry entry: https://github.com/taasky/mcp (`ai.taasky/taasky`)
- Protocol: https://github.com/taasky/protocol

## License

[MIT-0](LICENSE). The hosted Taasky service is not open source; this plugin
and the protocol are.
