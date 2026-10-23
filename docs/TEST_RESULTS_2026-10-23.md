# Dungeon Clear - October 23, 2026 integration observation

This was a smoke/integration check during a combined NPC Services, Junk-to-Gold and Custom Login release. **No Dungeon Clear source change was made or deployed** in this maintenance.

DungeonClear.Enable, RDF fill, AutoClear and LogoutOnRelease were enabled. During I07 the RDF group formed while the fill job was still provisioning; the job logged that its tank was matched into another group and released. No automatic `dc on` handoff was recorded by that job. Manual `.dc on` was supplied; subsequent path/combat logs were observed and the owner marked I07 Pass.

[Open investigation](https://github.com/Bramblesgow/mod-brambletown-services/issues/10) records the exact log, source paths, player-owned bot distinction and reproduction work. It is tracked on the NPC Services board because this fork has Issues disabled. This is not established as a regression against production. Determine ownership/intended behavior before changing group adoption or handoff logic; never control unrelated real-player groups.

Original production Dungeon Clear configuration was preserved byte-for-byte. This session was not a full dungeon completion/pathfinding regression campaign.

## Shared session and deployment record

Owner-completed sheet: `Brambletown_Combined_Test_Sheet_2026-10-23(1).pdf`. Corrected user marks: **65 Pass, 7 Deferred, 2 Blocked, 23 Not run** across 97 cases. This is the user-form tally, not a claim that all operator/restoration cases were unexecuted: operator evidence and subsequent deployment are reconciled separately. S03 and E06 were explicitly corrected to Pass after submission.

Combined isolated test binary SHA-256: `8d2fa8f0c0593d02b455b34a471450fff4fdb4b6b7c1af53f8393fcc6964bcdf`.
Production build from the same tested gameplay source, rebuilt with production configuration paths: `ac4d29bd37f436f495f8211ae4d3eb291ef181a8c43926a3e995497eb2f3f483`.

Released October 23, 2026 after explicit owner approval. Production controller recorded success at **11:48 AM America/Chicago (CDT)**. Auth/world ports responded, world console responded, and the inspected error log was empty. All **35 production configuration files remained byte-for-byte unchanged**; original authserver retained. Production characters/starter receipts and normal loot rates preserved; no cloned test data, guaranteed-drop fixtures or test configuration were imported.

Production rollback binaries, database dumps, configuration backup, migration output and deployment manifest are retained on the authorized server under `rollout-20261023/`. Test evidence is retained under `combined-runtime-20261023/evidence/`. Live startup checks are operational checks, not a substitute for later human gameplay confirmation.
