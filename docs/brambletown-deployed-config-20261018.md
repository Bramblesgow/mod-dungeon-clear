# Dungeon Clear — Brambletown deployed configuration snapshot

Captured: 2026-10-18 (America/Chicago)
Source commit observed on the production server: `07f8e33c8676bfc821fdbbadd68be3a25db63ba3`
Configuration source: `env/dist/etc/modules/mod_dungeon_clear.conf`; compared against matching `.conf.dist`.

The deployed source is the unmodified historical upstream commit `07f8e33`; the fork's `master` includes later upstream changes. This review does not replace the fork's newer upstream source with the older deployed snapshot.

## Non-default configuration entries

```ini
DungeonClear.DungeonQueueFill.AutoClear = 1
DungeonClear.DungeonQueueFill.Enable = 1
DungeonClear.SmartRest = 1
```

All other present keys matched the deployed `.conf.dist` at capture time. Values here are documentation, **not** an installable live configuration or code patch.

## Review focus

RDF automatic queue filling and dungeon auto-clear activation; SmartRest behavior; bot logout and release lifecycle.

## Gate to future changes

Preserve upstream default branch. Implement subsequent code/config changes in a separate branch and PR, review CodeRabbit findings, compile/verify, test in game, and record deployed commit/version. No production deployment or restart is part of this baseline PR.
