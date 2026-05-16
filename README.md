# Robynn Claude Plugin

This plugin packages Robynn for Claude as a thin wrapper around the hosted
remote MCP server at `https://mcp.robynn.ai/mcp`.

## What It Does

- Connects Claude to the deployed Robynn MCP backend
- Adds the `robynn:robynn-cmo` skill for Robynn-first marketing routing
- Adds the optional `robynn:robynn-cmo` agent for focused CMO workflows
- Keeps plugin parity tied to the production remote MCP surface
- Avoids local CLI subprocess packaging for plugin users
- Exposes the Hermes bridge Phase 1 tools through the hosted MCP surface:
  `robynn_capabilities`, `robynn_brand_source_add`,
  `robynn_brand_rebuild`, and server-side connected-app write execution

## Architecture

The plugin uses the hosted remote MCP server directly.

- Backend URL: `https://mcp.robynn.ai/mcp`
- Auth: OAuth through the hosted Robynn MCP flow
- Local CLI dependency: none for plugin users

Local CLI-only commands are intentionally out of scope for this plugin. Plugin
behavior is determined by what `mcp.robynn.ai` exposes.

## Install And Load

Load the plugin locally with:

```bash
claude --plugin-dir /Users/madhukarkumar/Developer/interactive-cmo/robynn-claude-plugin
```

After Claude starts:

```text
/reload-plugins
/mcp
```

Expected result:

- `robynn` appears as a configured MCP server
- `robynn:robynn-cmo` appears as a plugin skill
- `robynn:robynn-cmo` appears as a selectable plugin agent
- `robynn_capabilities` appears in the Robynn tool list and reports
  `agents.cmo.run` as available

## OAuth

This plugin relies on the hosted Robynn OAuth flow at `mcp.robynn.ai`.

- Claude should authenticate through the existing hosted connector flow
- No local Robynn CLI install is required for plugin users
- No local MCP subprocess is started by this plugin

## Support And Trust

- Support: `support@robynn.ai`
- Homepage: `https://robynn.ai`
- Repository: `https://github.com/robynnai/robynn-claude-plugin`
- Trust model: the plugin is a thin wrapper over the hosted Robynn MCP service
  and uses the existing hosted OAuth flow instead of packaging a separate local
  auth path
- Data-path expectation: plugin capability parity follows the deployed
  `mcp.robynn.ai` worker, not a local CLI mirror

## Validation

Expected local validation flow:

```bash
claude plugin validate .
```

## Acceptance Prompts

1. Website audit

```text
Run a website audit for https://cognitoforms.com. Use Robynn first and make sure the website URL is passed explicitly.
```

2. Connected-app question

```text
How many HubSpot contacts do we have right now? Use Robynn first.
```

3. General CMO request

```text
Run a CMO audit v2 for https://robynn.ai. Use Robynn first and prefer a deep route.
```

## Behavior Notes

- Plugin users get the hosted MCP tool surface exposed by
  `https://mcp.robynn.ai/mcp`.
- Local CLI-only commands are not part of this plugin surface.
- Parity is determined by the deployed `mcp.robynn.ai` worker, not by local
  CLI behavior or unpublished backend arguments.
