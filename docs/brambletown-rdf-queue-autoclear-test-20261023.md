# Brambletown — RDF QueueFill / AutoClear regression test (2026-10-23)

## Scope
Branch: `fix/rdf-queue-state-and-autoclear-tank-20261023` in `Bramblesgow/mod-dungeon-clear`. Not deployed to the live worldserver. This test is for a staging build only.

## Observed production symptoms
- 2026-10-23 12:53 CDT: Gnomadin's observed RDF queue never reached the tracked QUEUED state; job timed out at 60 s. A second Find Group click was refused as an existing in-flight fill. Subsequent manual `.dc dungeonqueuefill test Gnomadin` formed a party.
- 2026-10-23 afternoon: repeat no-AutoClear report. Gnomadin was later seen in a normal group with Protpnome and Holypnome. There was no new fill job in the current log segment. Exact failed rolecheck state is unknown.
- Pre-change AutoClear selected only a provisioned tank slot. A pre-grouped playerbot tank is not in that slot list, so AutoClear would never be issued in that case.

## Code changes
1. A repeated Find Group attempt refreshes the existing **Observed** queue-key/timeout instead of being discarded. Does not restart jobs once bot provisioning begins.
2. Records each observed core queue-state transition, the group/player state and selected-dungeon count at admission timeout. Does not synthesize QUEUED state or admit an invalid queue.
3. While a preformed party is in LFG rolecheck, prompts existing playerbots once using the stock `lfg role check` action. Never sends the action for a human or self-bot. Human role selections remain required.
4. Once RDF group forms, AutoClear finds an eligible AI-controlled tank in the **final party** (whether pre-grouped or newly provisioned) and confirms the tank and player are on the same dungeon **instance** before issuing `dc on`. Never drives a real human/self-bot.
5. Checks the action return; retries on subsequent ticks if `dc on` refuses (rather than falsely recording success).

## Verification
- [ ] Solo human DPS, RDF: auto-fill and AutoClear occur normally without using the `.dc ... test` command.
- [ ] Human DPS + pre-grouped tank bot + healer bot: rolecheck completes, two DPS bots join, pre-grouped tank receives AutoClear, and the party runs the dungeon.
- [ ] Human DPS + existing tank bot, rolecheck repeated once: no second queue-fill job, no stuck observation, matching still works.
- [ ] Human tank + queued bots: never auto-issue `dc on` to the human; normal RDF should remain available.
- [ ] Human self-bot tank: verify no unwanted human takeover.
- [ ] Human cancels/re-queues after completion: no stale job or orphan pool bot.
- [ ] Rejected queue (deserter/cooldown): no bots provisioned; log now reports group/player LFG state at timeout.
- [ ] Observe `.dc dungeonqueuefill status`, `Playerbots.log` QUEUEFILL lines and in-dungeon tank commands.
- [ ] Confirm no regression to release behavior; note upstream `e6524b1` changes release semantics and is *not* included in this branch.

## Test status
- C++ implementation syntax compilation: passed on the current server's compiler/include configuration.
- Pure AutoClear tank eligibility assertions: passed.
- In-game isolated test: NOT RUN.
- Full dungeon_clear_tests target: NOT RUN (active CMake build has BUILD_TESTING=OFF).
- Production deployment / restart: NOT PERFORMED.
