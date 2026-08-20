# Spark MCP — Claude plugin marketplace

Public distribution repo for connecting **Claude** to **Spark** via the hosted
Spark MCP server. This repo contains no server code — only the plugin manifest
that points Claude at the hosted, OAuth-protected endpoint
`https://mcp.spark.my.alaispark.app/mcp`. (The server itself lives in the private spark
repo and is deployed to Cloud Run.)

## Install (Claude Code)

```bash
# 1. Add this marketplace
claude plugin marketplace add Alai-Studios/spark-mcp

# 2. Install the Spark plugin (plugin@marketplace)
claude plugin install spark@spark
```

On first use Claude runs the OAuth flow against Spark's login (Authress); sign in
and approve. Your Spark permission roles bound what the tools can do.

## Install without this marketplace

You don't strictly need a plugin — any Claude surface can add the remote server by
URL:

```bash
# Claude Code, direct
claude mcp add --transport http spark https://mcp.spark.my.alaispark.app/mcp
```

**claude.ai / Claude Desktop:** Settings → Connectors → *Add custom connector* →
`https://mcp.spark.my.alaispark.app/mcp`.

## What you get

Tools grouped by capability: `me_*`, `roles_*`, `users_*`, `tools_*`, `agents_*`,
`codices_*` / `content_*`, `conversations_*`. Reads are always available; write
tools depend on the deployment and on your roles.

## Layout

```
.claude-plugin/marketplace.json   # marketplace: lists the `spark` plugin
plugins/spark/
  .claude-plugin/plugin.json      # plugin manifest
  .mcp.json                       # remote MCP server (http) → mcp.spark.my.alaispark.app
```

To point at a non-prod deployment, change the `url` in `plugins/spark/.mcp.json`
(e.g. `https://mcp.spark.p.alaispark.app/mcp` for dev).
