---
name: grow8
description: Plan how a product gets its first customers with grow8 (grow8.app). Use when the user mentions grow8 or their growth map, asks for a growth map, a go-to-market plan, first customers, distribution or marketing channels for their product, or wants to read, change or extend that map and get a link to it.
license: MIT
compatibility: Needs the grow8 MCP server (https://grow8.app/api/mcp), connected through the plugin or OAuth sign-in.
---

# grow8

grow8 turns a product description into a growth map: the foundation (audience, positioning, offer) and channels with moves and tests. The map lives on grow8.app and you work on it through the grow8 MCP tools. The server sends the hard rules and each tool describes itself. This skill is the loop to run with the founder.

## If the tools are missing

If grow8 tools such as `get_map` are not available, the server is not connected. Point the founder to `references/mcp-setup.md` (sign-in is OAuth, no key) and stop until it is.

## The loop

1. **Read the map first.** `list_maps`, then `get_map`. Never guess node ids and never plan from memory.
2. **No map yet.** Say that `create_map` costs 20 credits and ask before calling it. Use the founder's own description of the product (and who pays, if they said). If the description is too thin, ask one question. Do not fill gaps with your own guesses.
3. **Propose in words.** Say what you would change and why, in plain language, tied to what the map already says. Offer one or two next moves, not a rewrite.
4. **Preview.** Run the change as a preview and show the founder what it does in plain language.
5. **Wait for a yes.** Apply only after the founder agrees to that preview. Ask explicitly before archiving a node, changing the goal or rewriting a foundation field.
6. **Apply, then give the link.** Return the map link from the result and a short list of what changed. Offer to revert if they do not like it.

## Rules

- Cases and similar products come from grow8 tools only. Do not invent cases, numbers or results, and report no more than a case says.
- The model of the map (nodes, ops, fields) is in `get_guide`. Read it there instead of relying on this file.
- Out of credits: stop, tell the founder, point to the pricing link in the error. Do not retry.
- If the map changed since you read it, read it again and re-plan.
