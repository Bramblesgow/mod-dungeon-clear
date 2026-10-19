# Dungeon Clear — Brambletown deployed configuration snapshot

Captured: 2026-10-18 (America/Chicago)
Module checkout HEAD observed on the server: `07f8e33c8676bfc821fdbbadd68be3a25db63ba3`
Configuration checked on disk: `env/dist/etc/modules/mod_dungeon_clear.conf`; compared with the installed `mod_dungeon_clear.conf.dist` in the same directory, not the source-tree template.

The server's module checkout points to historical upstream commit `07f8e33`; the fork's `master` includes later upstream changes. The built worldserver revision and effective in-memory configuration were not independently verified. This documentation does not replace newer fork source with the older checkout.

## Non-default configuration entries

```ini
DungeonClear.DungeonQueueFill.AutoClear = 1
DungeonClear.DungeonQueueFill.Enable = 1
DungeonClear.SmartRest = 1
```

On 2026-10-18, these were the only differences among the 103 present `DungeonClear.*` entries when compared with the installed `.conf.dist`. In particular, `DungeonClear.DungeonQueueFill.LogoutOnRelease = 1` is present and matches the installed default; it is not a non-default override. The source checkout's `conf/mod_dungeon_clear.conf.dist` contains additional settings and must not be used as the installed-default baseline.

Values here document files on disk; they are **not** an installable live configuration or code patch, and do not demonstrate runtime behavior.

## Review focus

RDF automatic queue filling and dungeon auto-clear activation; SmartRest behavior; bot logout and release lifecycle.

## Gate to future changes

Preserve the upstream default branch. Implement subsequent code/config changes in a separate branch and PR, review CodeRabbit findings, compile/verify, test in-game, and record the deployed commit/version. No production deployment or restart is part of this baseline PR.
