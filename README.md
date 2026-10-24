# Taasky plugin

Your agent settles small things with anyone: a time for the plumber, a
swapped shift, a price for a sofa. The other side answers with their own
agent, or in a browser with no agent at all. Nothing is agreed until both
of you say yes.

This plugin gives an agent three things:

- **The Taasky MCP server**, `https://mcp.taasky.ai/mcp` (Streamable HTTP).
  No account, no key, no sign-in.
- **The `taasky` skill** ([`skills/taasky/SKILL.md`](skills/taasky/SKILL.md)):
  how to open a room, set private limits, take turns, and hand the final
  yes or no to the human, who confirms with one tap on their own page of
  the room (`human_url`).
- **The `common-ground` skill**
  ([`skills/common-ground/SKILL.md`](skills/common-ground/SKILL.md)): for
  agents of different people that each know part of a problem. They keep one list of findings,
  each agreed, disputed or open, until both sides see the question the same
  way or know exactly where they differ. The agent tells its human what it
  conceded, and the human approves the list on their page.

## Install

**Cursor and Grok Bot.** Install Taasky from the Cursor Marketplace (in Grok
Bot: Connect apps). Until it is listed, add the server by hand: in Cursor,
put the contents of [`mcp.json`](mcp.json) into `~/.cursor/mcp.json`; in
Grok Bot, ask a Bot to add a remote HTTPS MCP server named `taasky` with
the URL above.

**Claude Code.**

```
/plugin marketplace add taasky/plugin
/plugin install taasky@taasky
```

**Codex.**

```
codex plugin marketplace add taasky/plugin
codex plugin add taasky@taasky
```

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
| `.claude-plugin/plugin.json`, `.claude-plugin/marketplace.json` | Claude Code manifest and a one-plugin marketplace |
| `.agents/plugins/marketplace.json` | Codex marketplace (Codex won't load a plugin from the marketplace root, so it points at this repo by URL) |
| `mcp.json` | the remote MCP server, Agent Plugins format (`streamable-http`) |
| `.mcp.json` | the same server for Claude Code and Grok Build (`http`) |
| `skills/taasky/SKILL.md` | the skill, version in its frontmatter |
| `skills/common-ground/SKILL.md` | Common ground, version in its frontmatter (named `taasky-align` until 0.3) |
| `assets/logo.svg` | logo |

## Where the skills live

This repo is the source of both skills: change them here. docs.taasky.ai
copies `skills/taasky/SKILL.md` to
`https://docs.taasky.ai/.well-known/agent-skills/taasky/skill.md` on its own
(taasky-docs, `sync-skill.yml`), and ClawHub publishes the same file as
`taasky`.

A new version of `taasky`:

1. Merge it here, with the new `metadata.version`.
2. docs.taasky.ai picks it up within the hour.
3. The server announces it (`SKILL_VERSION` in taasky-mcp), so agents with an
   older copy offer to update.

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
