# Spark MCP

Connect **Claude** to **Spark** — manage agents, tools, codices/content, users,
roles, and conversations directly from Claude.

## Install (Claude Code)

Copy-paste the command for your environment:

**Production**
```bash
claude mcp add --transport http \
  --client-id app_cK1sJ7Jmnta5BRYWyzn8wQ --callback-port 20148 \
  spark https://mcp.spark.my.alaispark.app/mcp
```

**Staging**
```bash
claude mcp add --transport http \
  --client-id app_tQxLU61iQd9bKp6WWp3Njg --callback-port 20148 \
  spark-staging https://mcp.spark.staging.alaispark.app/mcp
```

Then, in a Claude Code session, run `/mcp`, select the server, choose
**Authenticate**, and sign in.

```bash
claude mcp list        # spark → ✓ connected
```

Ask Claude to call `me_get_profile` to confirm it's working. You act with your own
Spark permissions — anything you're not allowed to do comes back as an error.

> Stuck, or need to retry? Reset and re-add:
> ```bash
> claude mcp logout spark 2>/dev/null; claude mcp remove spark 2>/dev/null
> ```

## What you get

Tools grouped by capability: `me_*`, `roles_*`, `users_*`, `tools_*`, `agents_*`,
`codices_*` / `content_*`, `conversations_*`. What you can read or write is bounded
by your Spark roles.

## Notes

- Use the **Claude Code CLI** commands above. The claude.ai / Claude Desktop
  connector UI isn't supported yet.
- Port `20148` must be free on your machine; don't change it without checking with
  the Spark team first.
