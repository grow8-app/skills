# grow8 skills

The grow8 skill for AI agents, and a Claude Code plugin that also connects the grow8 MCP server. grow8 (https://grow8.app) turns a product description into a growth map; the skill teaches an agent to read it, check it against real cases, change it and return the link.

## Install

1. Switch on the "API and integrations" experiment in https://grow8.app/app/settings (Experiments), then create a key at https://grow8.app/app/settings/api. Put it in your environment:

   ```sh
   export GROW8_API_KEY=...   # in ~/.zshrc or the env your agent starts in
   ```

2. Install the skill into every agent found on your machine:

   ```sh
   npx skills add grow8-app/skills -g
   ```

3. Connect the MCP server (`https://grow8.app/api/mcp`) in your agent. Ready commands for Claude Code, Codex, Cursor and Gemini CLI are in [skills/grow8/references/mcp-setup.md](skills/grow8/references/mcp-setup.md).

`npx skills` installs only the skill files. It does not register the MCP server and does not pass the key.

## Claude Code plugin

One step instead of 2 and 3: the plugin installs the skill and registers the MCP server. The key is read from `GROW8_API_KEY`.

```
/plugin marketplace add grow8-app/skills
/plugin install grow8@grow8
```

## Prices

Reads are free. `create_map` costs 20 credits. A change that applies costs 1 credit per batch; a preview and a revert are free. The key is limited to 60 requests a minute and 300 searches a day.

## License

MIT
