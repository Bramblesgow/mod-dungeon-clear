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
