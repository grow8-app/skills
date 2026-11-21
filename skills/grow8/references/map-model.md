# Working with a grow8 map

grow8 keeps a growth map per product. Read it, check it against real cases, change it, and give the founder the link.

## Shape of a map
- Root with a foundation (audience, positioning, offer) and seven channels: threads, email, listings, search, x, partners, ads.
- Node kinds: foundation, basis (a foundation field), channel, tactic (a move from research), own (the founder's own node). An own node right under a channel is a move; an own node under a move is a step, a small task of that move.
- Channel status: focus, testing, later. A move under test has a due date; its verdict is worked, failed or early.
- Every node has an id shown in brackets. Use these ids in ops.

## Workflow
1. get_guide (this), then list_maps and get_map. Note the Version.
2. Check: check_map shows what backs each move. search_cases and get_case read the collected cases. Never invent numbers or cases.
3. Change: apply_map_changes with base_version set to the version you read. Run it with preview true first: it shows the diff and charges nothing. Then run it again with preview false.
4. A new move's `from` is "slug#order" of the case move it copies. Read the result's notes: a move gets a case's name only if that case made the same move in the same channel and it worked or mixed. Otherwise it is the founder's own idea.
5. stale_map means the map changed since you read it: get_map again and re-plan.
6. revert_change undoes the map's latest change from any source: any key or the web app. Only the latest one can go.
7. Give the founder the link from the result.

## Ops (apply_map_changes)
add (parent, title, optional from, metric, duration), open_channel, rename, memo, archive, restore, channel_status, step_done, start_test (days), outcome (verdict, actual), basis (audience, positioning, offer), goal, progress. Up to 20 ops per call.

## Prices
- A change that applies costs 1 credit. A preview, a rejected change and a revert cost nothing.
- create_map costs credits (research). get_balance shows what is left. no_credits means stop and tell the founder.
- Reads are free. The key is limited to 60 requests a minute and 300 searches a day.
