---
name: grow8
description: Plan and track how a product gets its first customers with grow8 (grow8.app) - create a growth map from a product description, read and edit channels, moves and tests, check them against real cases of similar products, and give the founder a link to the map. Use when the user asks for a go-to-market or distribution plan, marketing channels for their product, or mentions grow8 or their grow8 map.
license: MIT
compatibility: Needs the grow8 MCP server (https://grow8.app/api/mcp) and a grow8 API key in the environment variable GROW8_API_KEY.
---

# grow8

grow8 turns a product description into a growth map: the foundation (audience, positioning, offer) and seven channels with moves and tests. The map lives on grow8.app. You read and change it through the grow8 MCP tools.

## Connect

1. If the tools `get_guide`, `list_maps`, `get_map` are available, use them.
2. If not, tell the user to switch on the "API and integrations" experiment in https://grow8.app/app/settings (Experiments), then create a key at https://grow8.app/app/settings/api, set `GROW8_API_KEY` in their environment, and connect the server as described in `references/mcp-setup.md`.
3. Never ask the user to paste the key into the chat, never print it, never write it into project files or commands. Refer to it only as `GROW8_API_KEY`.

## Tools

- Free reads: `get_guide`, `get_balance`, `list_maps`, `get_map`, `get_node`, `find_similar_products`, `search_cases`, `get_case`, `check_map`.
- `create_map` (`description`, `audience` optional, `lang` optional: en, es, de, fr, ru) - 20 credits, runs research. The map comes with its foundation and channels but no moves.
- `apply_map_changes` (`map_id`, `base_version`, `ops`, `preview`) - 1 credit per batch with at least one applied op. `preview: true` is free.
- `revert_change` (`map_id`, `change_id` optional) - free.

Call `get_guide` once at the start; `references/map-model.md` holds the same text.

## Workflow

1. **Find or create the map.** `list_maps`. If the user has no map for this product, say that `create_map` costs 20 credits and runs research, then call it with the user's own description of the product (`description`, and `audience` if the user named who pays). Do not invent facts about the product; ask one question if the description is too thin. A new map has no moves yet: grow them with an `open_channel` op per channel the founder wants to work on (`apply_map_changes`, previewed first like any change).
2. **Read before you change.** `get_map` and note its version. Use `get_node` for one node in full. Never guess node ids.
3. **Check against cases.** `check_map`, `search_cases`, `get_case`, `find_similar_products`. Report what the cases say, never more.
4. **Preview.** Call `apply_map_changes` with `base_version` set to the version you read and `preview: true`. It charges nothing.
5. **Show the diff in words.** Tell the founder what will change in the map, in plain language, and that applying costs 1 credit. Wait for a yes before the next step. Always ask before archiving a node, changing the goal, or rewriting a foundation field.
6. **Apply.** Run the same ops with `preview: false`.
7. **Give the link** from the result (`?focus=` points at the changed nodes) and a short list of what changed. If the founder wants it undone, `revert_change`.

## Errors

- `no_credits`: stop. Tell the founder to top up at the pricing link in the error. Previews and reads still work. Do not retry.
- `stale_map`: the map changed since you read it. Run `get_map` again and re-plan the ops.
- `rate_limited`: wait and tell the founder; do not loop.
- `not_found`: re-check the id with `list_maps` or `get_map`.
- `feature_off`: the API is not enabled for this account. Tell the founder to switch on the "API and integrations" experiment in grow8 settings.
- `map_not_ready`: the map is still being built in the web app. Tell the founder to finish its research there first.

## Do not

- Do not make up numbers, cases or results. Cases and similar products come from grow8 tools only.
- Do not rewrite the whole map to change one thing.
- Do not apply a change the founder has not seen in a preview.
- Do not print, ask for or store the API key.
