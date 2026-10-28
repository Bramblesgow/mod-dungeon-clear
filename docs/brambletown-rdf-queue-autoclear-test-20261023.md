# AutoClear Pre-Grouped Tank — isolated staging test

Split from original Brambletown PR #2. **Draft / not deployed.**

## Scope
- Select an eligible AI-controlled tank from the final RDF group, not only newly provisioned queue-fill slots.
- Require the player and bot tank to be in the same dungeon instance; exclude humans and self-bots.
- Do not record AutoClear as issued if the bot refuses the action.
- Add tank-eligibility regression assertions.

## Verification pending
- Human DPS with pre-grouped bot tank: AutoClear starts after the dungeon forms.
- Newly provisioned bot tank continues to work.
- Human and self-bot tanks are never controlled by AutoClear.
- Multiple simultaneous instances do not cross-activate AutoClear.
- In-game staging tests and full GTest run are **not complete**.

No queue observer, rolecheck, or admission recovery changes are included. No production deployment authorized.

## Additional defect: AutoClear does not restart after full-party wipe (observed October 27)
- After a dungeon group wipe and recovery, the AI tank remained inactive until the player manually issued `.dc on`.
- Initial AutoClear handoff records `_autoClearIssued = true`. The current queue-fill implementation does not automatically clear that latch after a wipe. This observation suggests a lifecycle gap but does not by itself establish the entire root cause.
- Investigate whether the formed job is still active after the wipe, how the tank DC run state transitions, and what existing wipe/resurrection events can safely trigger a restart.

### Required behavior and regression tests
- When AutoClear was automatically enabled for the run, restart the AI tank's Dungeon Clear routine **after a confirmed full wipe and party recovery**, without requiring `.dc on`.
- Wait until the group is alive/recovered, back in the appropriate instance, and not in combat before retrying; avoid repeated commands during the wipe.
- Preserve manual `.dc off` opt-out; do not override manual tank control, real players, self-bots, normal encounter pauses, or partially dead groups.
- Verify a second wipe also recovers, and verify no restarts after group disbanding, leaving the instance, or AutoClear being disabled.
- Capture logs and a reproducible in-game scenario. **Implementation and test validation pending; no wipe-recovery fix is claimed in this draft.**
