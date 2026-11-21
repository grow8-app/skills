# Connect grow8 MCP

Server URL: `https://grow8.app/api/mcp`. The key comes from the environment variable `GROW8_API_KEY` and is never written into a command, a file or the chat. Switch on the "API and integrations" experiment in https://grow8.app/app/settings (Experiments), then create a key at https://grow8.app/app/settings/api.

Syntax checked 2026-11-21 against each client's docs.

## Claude Code

Docs: https://code.claude.com/docs/en/mcp ("Add a remote HTTP server").

```sh
claude mcp add --transport http grow8 https://grow8.app/api/mcp --header "Authorization: Bearer $GROW8_API_KEY"
```

The shell expands the key, so Claude Code stores the expanded value in its config.

## Codex

Docs: https://developers.openai.com/codex/mcp ("Streamable HTTP servers": `bearer_token_env_var`).

```toml
# ~/.codex/config.toml
[mcp_servers.grow8]
url = "https://grow8.app/api/mcp"
bearer_token_env_var = "GROW8_API_KEY"
```

## Cursor

Docs: https://cursor.com/docs/context/mcp ("Config interpolation": `${env:NAME}` in headers).

```jsonc
// ~/.cursor/mcp.json
{
  "mcpServers": {
    "grow8": {
      "url": "https://grow8.app/api/mcp",
      "headers": { "Authorization": "Bearer ${env:GROW8_API_KEY}" }
    }
  }
}
```

## Gemini CLI

Docs: https://geminicli.com/docs/tools/mcp-server/ ("Adding an HTTP server"). Its docs describe env expansion only for the `env` block, not `headers`, so the shell fills the key in.

```sh
gemini mcp add --scope user --transport http --header "Authorization: Bearer $GROW8_API_KEY" grow8 https://grow8.app/api/mcp
```

The shell expands the key, so Gemini CLI stores the expanded value in its config.

## Skill

Docs: https://github.com/vercel-labs/skills (`-g` installs for every project).

```sh
npx skills add grow8-app/skills -g
```

This installs only the skill. It does not register the MCP server and does not pass the key. Connect the MCP server with one of the commands above.

## Claude Code plugin

Docs: https://code.claude.com/docs/en/discover-plugins ("Add a marketplace", "Install a plugin").

```
/plugin marketplace add grow8-app/skills
/plugin install grow8@grow8
```

The plugin installs the skill and registers the MCP server. It reads the key from `GROW8_API_KEY` in the environment Claude Code starts in.
