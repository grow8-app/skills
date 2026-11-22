# Connect grow8 MCP

Server URL: `https://grow8.app/api/mcp`. The default is OAuth: add the server, the client opens a browser, the founder signs in to grow8 and approves. No key, no environment variable.

Setup prompt for an agent: `Fetch and execute the instructions to set me up for grow8 from https://grow8.app/agent-setup.md`.

## Plugin (recommended)

Installs the skill and registers the server in one step.

```sh
# Claude Code
claude plugin marketplace add grow8-app/skills
claude plugin install grow8@grow8

# Codex
codex plugin marketplace add grow8-app/skills
```

Cursor: add `grow8-app/skills` as a plugin marketplace source and install `grow8`.

## Server only

```sh
# Claude Code
claude mcp add --transport http grow8 https://grow8.app/api/mcp

# Codex
codex mcp add grow8 --url https://grow8.app/api/mcp
```

```jsonc
// Cursor: ~/.cursor/mcp.json
{ "mcpServers": { "grow8": { "url": "https://grow8.app/api/mcp" } } }
```

Then sign in when the client asks (`/mcp` in Claude Code, `codex mcp login grow8` in Codex).

## Skill only

```sh
npx skills add grow8-app/skills -g
```

This installs the skill files without the server. Connect the server separately.

## API key for CI

For headless runs where a browser sign-in is not possible, create a key at https://grow8.app/app/settings/api and keep it in the environment as `GROW8_API_KEY`. Never paste it into the chat or write it into files. The client sends it as `Authorization: Bearer $GROW8_API_KEY`.

```sh
claude mcp add --transport http grow8 https://grow8.app/api/mcp --header "Authorization: Bearer $GROW8_API_KEY"
```

```toml
# ~/.codex/config.toml
[mcp_servers.grow8]
url = "https://grow8.app/api/mcp"
bearer_token_env_var = "GROW8_API_KEY"
```

A key client can apply changes without a preview; OAuth clients must preview first.
