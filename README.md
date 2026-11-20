# WBX Sandbox plugin for Codex

Run code in isolated Linux microVM sandboxes straight from Codex: commands, Python and JavaScript, files, a headless browser and background jobs, with persistent named workspaces, network controls and spending limits.

This repository is a Codex plugin marketplace with one plugin, `wbx-sandbox`. It bundles:

- the remote **WBX Sandbox MCP server** (`https://sandbox.wbx.cz/mcp`, sign-in with OAuth),
- the **sandbox-workflows** skill – when to use a quick command, a background job or a named sandbox, and how to keep cost and side effects under control.

You need a WBX Sandbox account: <https://sandbox.wbx.cz>.

## Install

Add the marketplace:

```bash
codex plugin marketplace add WBX-Sandbox/codex-plugin
```

Then open Codex, run `/plugins`, select the **WBX Sandbox** marketplace and install the `wbx-sandbox` plugin. Codex asks you to sign in to your WBX Sandbox account the first time the MCP server is used.

Update later with:

```bash
codex plugin marketplace upgrade wbx-sandbox
```

### ChatGPT workspaces

Workspace admins can import this repository as a plugin marketplace in the admin console (Plugins → Import marketplace) with the URL `https://github.com/WBX-Sandbox/codex-plugin`.

### Without the plugin

Any MCP client can connect to the server directly:

```json
{
  "mcpServers": {
    "wbx-sandbox": { "type": "http", "url": "https://sandbox.wbx.cz/mcp" }
  }
}
```

## Try it

- “Run this project's tests in a WBX sandbox.”
- “Make a small web page in a sandbox and give me a link.”
- “Start a background job that processes data.csv and show its summary.”

## Layout

```
.agents/plugins/marketplace.json        marketplace entry
plugins/wbx-sandbox/
  .codex-plugin/plugin.json             plugin manifest
  .mcp.json                             remote MCP server
  skills/sandbox-workflows/SKILL.md     usage guidance for the agent
  assets/logo.png
```

## Links

- Website and documentation: <https://sandbox.wbx.cz>
- Support: <https://sandbox.wbx.cz/support>
- Privacy: <https://sandbox.wbx.cz/privacy> · Terms: <https://sandbox.wbx.cz/terms>

## License

MIT – see [LICENSE](LICENSE).
