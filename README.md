# Markasso for Claude Code and Codex

The whiteboard your agents draw on. This plugin gives Claude the [Markasso](https://markasso.it) tools: it draws architecture diagrams, flowcharts and sketches, lays them out by itself, looks at the result, and hands you a markasso.it link, a `.markasso` file or an SVG. With a live link it joins a shared board and draws next to the people on it, in real time.

## Install

```bash
claude plugin marketplace add AlbertoBarrago/markasso-plugin
claude plugin install markasso@markasso
```

Or from inside a session: `/plugin install markasso --marketplace AlbertoBarrago/markasso-plugin`.

**Codex CLI:**

```bash
codex plugin marketplace add AlbertoBarrago/markasso-plugin
codex plugin add markasso@markasso
```

Codex reads the portable manifest (`plugin.json`, `mcp.json`); Claude Code reads `.claude-plugin/`. Both get the same server and skill.

The plugin runs the [`@markasso/mcp`](https://www.npmjs.com/package/@markasso/mcp) server with `npx`, so it needs Node 22 or later. Without the plugin, the same server works in any MCP client: see its [README](https://github.com/AlbertoBarrago/markasso/tree/main/mcp#readme).

## Try it

- *"Draw the architecture of this repository: services, data stores and how they talk. Give me a share link."*
- *"Turn the checkout flow in `src/checkout` into a flowchart with the decision points."*
- *"Join https://markasso.it/?live=… and add the missing cache to the diagram on the board."*

## What it includes

- **MCP server `markasso`**: create, read and edit diagrams, export PNG and SVG, share links, live sessions.
- **Skill `diagram`**: tells Claude when to reach for Markasso and how to draw a clear diagram with it.

## Live sessions and licence

Everything is free except drawing live in a shared session, which needs a [Markasso Cloud](https://markasso.it/cloud) licence. When you enable the plugin, Claude Code asks for the key: leave it empty if you do not have one. It is stored in your system's secure credential store and sent only to markasso.it.

Codex plugins have no prompt for a key, so the plugin in Codex does everything except live sessions. To draw live from Codex, add the server on its own with the key in its environment instead of the plugin: `codex mcp add markasso --env MARKASSO_LICENSE=<your key> -- npx -y @markasso/mcp@latest`.

## Privacy

Diagrams stay on your machine until you share them. `diagram_share` uploads the diagram to markasso.it to create its link; live sessions send your edits to the room you joined.

## Licence

MIT
