# grow8 skills

One plugin for Claude Code, Codex and Cursor. It installs the grow8 skill and connects the grow8 MCP server (`https://grow8.app/api/mcp`) with OAuth: you sign in once in the browser, no API key. grow8 (https://grow8.app) turns a product description into a growth map; the skill teaches an agent to read it, propose changes, preview them and return the link.

## Fastest: one prompt

Paste this to your agent:

```
Fetch and execute the instructions to set me up for grow8 from https://grow8.app/agent-setup.md
```

## Claude Code

```sh
claude plugin marketplace add grow8-app/skills
claude plugin install grow8@grow8
```

## Codex

```sh
codex plugin marketplace add grow8-app/skills
```

Then install `grow8` from the plugin list and sign in when asked.

## Cursor

Add `grow8-app/skills` as a plugin marketplace source (Cursor reads `.cursor-plugin/marketplace.json`) and install `grow8`.

## Other agents

`npx skills add grow8-app/skills -g` installs the skill only. Connect the server as described in [skills/grow8/references/mcp-setup.md](skills/grow8/references/mcp-setup.md), including the API key option for CI.

Full instructions for agents: https://grow8.app/agent-setup.md

## Prices

`create_map` costs 20 credits. A change that applies costs 1 credit per batch; a preview and a revert are free. `find_similar_products`, `search_cases` and `get_case` are free up to a daily quota by plan (Free 50, Pro 200, Studio 500), then 1 credit each. Other reads are free. Details at https://grow8.app/pricing.

## License

MIT covers the code in this repo. grow8 cases and data you get through it are covered by the [Terms of use](https://grow8.app/terms).
