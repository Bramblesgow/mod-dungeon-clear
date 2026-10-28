# RDF Queue-Fill Recovery — isolated staging test

Split from original Brambletown PR #2. **Draft / not deployed.**

## Scope
- Refresh a pending Observed queue intent after repeated Find Group requests without starting a second job.
- Log LFG state changes and admission timeout diagnostics.
- Prompt existing AI-controlled group bots once for stock LFG rolecheck, excluding humans and self-bots.

## Verification pending
- Solo DPS RDF automatic fill without manual test command.
- Pre-grouped tank/healer bots complete rolecheck and receive needed DPS bots.
- Repeat Find Group; cancellation/requeue; queue-rejected cases; no duplicate jobs or orphan bots.
- Inspect queue diagnostics and ensure no indefinite ROLECHECK hang.
- In-game staging tests and full GTest run are **not complete**.

No AutoClear tank-selection code is included in this PR. No production deployment authorized.
