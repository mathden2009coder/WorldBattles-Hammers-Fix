# WorldBattles Hammers 0.4.5 — full 3x3 queue test build

The user's reference mod performs the 3x3 neighbor destruction synchronously in one procedure. The WorldBattles mod already queues the eight neighboring positions and uses a tool-aware destroy helper, but its tick worker was capped at two queue entries per tick. This could leave the 3x3 operation split across multiple ticks and contribute to skipped/inconsistent positions.

This patch changes the per-tick processing budget from 2 to 8 so all eight queued neighbors can be processed in the same tick, following the reference mod's one-operation 3x3 approach while retaining WorldBattles' existing tool-aware drops and item identity.

Archive integrity checked and bytecode inspected. This still requires in-game verification on Forge 1.20.1.