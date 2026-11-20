# WBX Sandbox plugin for Codex

Run code in isolated Linux microVM sandboxes straight from Codex: commands, Python and JavaScript, files, a headless browser and background jobs, with persistent named workspaces, network controls and spending limits.

This repository is a Codex plugin marketplace with one plugin, `wbx-sandbox`. It bundles:

- the remote **WBX Sandbox MCP server** (`https://sandbox.wbx.cz/mcp`, sign-in with OAuth),
- the **sandbox-workflows** skill – when to use a quick command, a background job or a named sandbox, and how to keep cost and side effects under control.

You need a WBX Sandbox account: <https://sandbox.wbx.cz> (start free, no card required).

## What Codex can do with it

[WBX Sandbox](https://sandbox.wbx.cz) gives the agent an isolated Linux computer of its own: a
Firecracker microVM with its own kernel, disk and network policy, on servers in the EU. Nothing
runs on your machine. Through the MCP server Codex can:

- **create sandboxes** from templates (Python, data analysis, browser, Node.js and more), with
  full internet, an allowlist of destinations or no network, and optionally a public IPv6 address
- **run commands and code** (Python, JavaScript, bash) and **read, write, list and delete files**
- **serve a web app** and get its HTTPS URL, protected by an access token
- **keep a named workspace** – sandboxes from the assistant fall asleep after 10 minutes without
  commands instead of being destroyed; files are kept and the next command wakes them up
- **hand over longer work** as background jobs or batches with a price limit, wait for them on the
  server, read a compact log digest with recognised test results, download result files and get
  the job's execution receipt
- **check spending limits** and the available compute classes
- **see and control a Linux desktop** (beta, only for teams where Desktop & Computer Use is
  enabled on request)

All tools: [MCP server and tools](https://sandbox.wbx.cz/docs/mcp) ·
Pricing: <https://sandbox.wbx.cz/pricing>

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

- Website: <https://sandbox.wbx.cz> · Documentation: <https://sandbox.wbx.cz/docs>
- Support: <https://sandbox.wbx.cz/support>
- Privacy: <https://sandbox.wbx.cz/privacy> · Terms: <https://sandbox.wbx.cz/terms>

## License

MIT – see [LICENSE](LICENSE).
